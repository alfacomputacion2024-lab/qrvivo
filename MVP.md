# 🛠️ MVP Técnico — QR Vivo

Objetivo: **panel de edición autónoma + redirección medible**, en ≤2 semanas, coste ~0 $.

## 1. Arquitectura

```
                ┌────────────────────────────────────────────┐
 Impreso  ───▶  │  qr.dominio.com/:codigo   (Cloudflare)     │
 (papel)        │  Worker:                                    │
                │   1) SELECT destino FROM qr WHERE codigo=?  │──▶ 302 → destino final
                │   2) INSERT scan (ts, device, país)         │
                └────────────────────────────────────────────┘
                                     ▲
 Navegador (móvil/PC) ──▶  Panel web (edición autónoma) ──► D1 (datos)
                                   │
                            Lemon Squeezy (suscripción)
```

### Piezas y tiers gratuitos
| Pieza | Elección | Tier inicial |
|---|---|---|
| Redirección + contador | **Cloudflare Workers** | Free (100k req/día) |
| Base de datos | **Cloudflare D1** (SQLite edge) | Free (5 GB) |
| Auth de usuarios | **Supabase Auth** (o Cloudflare Access) | Free |
| Panel (UI) | Estático en Pages + API del Worker (mínimo) o **Softr/Airtable** si no-code | Free |
| Pagos | **Lemon Squeezy** (maneja impuestos) | 5 % + 0,50 $/transacción |
| Email transaccional | Resend / MailerLite | Free |
| Landing | GitHub Pages (ya activa) | Free |
| Dominio | qr[marca].com (o tjz.link — subdominio de un link corto propio) | ≈12 $/año |

> Todos los límites del plan gratis se implementan **en el Worker/DB** (2 QRs dinámicos, 100 escaneos), no en la UI.

## 2. Modelo de datos (D1)

```sql
CREATE TABLE usuarios (
  id            TEXT PRIMARY KEY,      -- sub de Supabase Auth
  email         TEXT NOT NULL,
  plan          TEXT DEFAULT 'free',   -- free | negocio | agencia
  stripe_ref    TEXT,                  -- Lemon Squeezy customer id
  fundador      INTEGER DEFAULT 0,     -- 1 = precio 8 $ vitalicio
  creado        DATETIME DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE qr (
  id            TEXT PRIMARY KEY,      -- id corto
  usuario_id    TEXT NOT NULL REFERENCES usuarios(id),
  codigo        TEXT UNIQUE NOT NULL,  -- slug imprimible: nonna-menu
  destino       TEXT NOT NULL,         -- URL final (editable)
  nombre        TEXT,                  -- "Menú La Pizzería Nonna"
  activo        INTEGER DEFAULT 1,
  creado        DATETIME DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE escaneos (
  id            INTEGER PRIMARY KEY AUTOINCREMENT,
  qr_id         TEXT NOT NULL REFERENCES qr(id),
  ts            DATETIME DEFAULT CURRENT_TIMESTAMP,
  device        TEXT,                  -- mobile | desktop
  pais          TEXT,                  -- por IP (opcional v2)
  referer       TEXT
);
CREATE INDEX idx_escaneos_qr_ts ON escaneos(qr_id, ts);
```

## 3. Endpoints del Worker

| Método | Ruta | Función |
|---|---|---|
| `GET` | `/:codigo` | Busca destino → `INSERT` escaneo → `302`. Si no existe → landing. |
| `POST` | `/api/qr` | Crea QR (respeta límites del plan) |
| `PATCH` | `/api/qr/:id` | **Cambia destino / nombre / activo** (la función estrella) |
| `DELETE` | `/:id` | Elimina QR |
| `GET` | `/api/qr/:id/stats` | Escaneos por día + % móvil (JSON para el panel) |
| `POST` | `/api/webhook/lemonsqueezy` | Activa plan al pagar |

### Lógica de límites (free)
- `free`: máx. 2 QRs activos; al superar 100 escaneos/mes el Worker responde con página "límite alcanzado → sube a Negocio".
- `negocio`/`agencia`: sin límites.

## 4. Panel de edición autónoma (v1)

Pantallas mínimas:
1. **Login** (email + magic link de Supabase)
2. **Mis QRs**: lista con nombre, código, escaneos/mes → botón **"Cambiar destino"** (modal con input + Guardar) + Descargar PNG + Borrar
3. **Estadísticas**: gráfica de escaneos últimos 30 días + % móvil
4. **Cuenta**: plan, upgrade con Lemon Squeezy (checkout hosted)

Regla de diseño: **cualquier cambio ≤3 toques desde el móvil.** La promesa "si sabes usar WhatsApp…" se verifica con 5 usuarios reales intentándolo sin ayuda.

### QR PNG
Generar en el cliente con librería JS (qrious/qr-code-styling) → descarga. Ahorra backend y da libertad de color/logo en v2.

## 5. Fases de desarrollo

| Fase | Semana | Entregable |
|---|---|---|
| **v0.5** | S2 | Worker con redirección + conteo + tabla; 10 QRs de prueba impresos y funcionando |
| **v1.0** | S3 | Auth + panel (lista, editar destino, stats, PNG) + límites free + Lemon Squeezy checkout |
| **v1.1** | S5 | Formulario landing conectado + email transaccional + página de éxito |
| **v2.0** | Mes 2-3 | Colores/logo en QR, plantillas premium, dominio corto, CSV |
| **v2.5** | Mes 3-4 | Subcuentas/marca blanca (plan Agencia 29 $), alertas de escaneo por email |

## 6. Operación y costes umbrales

- **0-100.000 escaneos/día** → tier gratis (de sobra para ~50 clientes).
- Si supera → Workers Paid **5 $/mes** (rentable desde el cliente 2).
- Backups D1: `wrangler d1 export` semanal al empezar a cobrar.
- **Plan de emergencia**: si cae el Worker, los QR impresos apuntan a un dominio con página alternativa (regla DNS de respaldo documentada).

## 7. Seguridad / cumplimiento

- Redirect sanitizado: solo `https://` permitido; lista negra de categorías maliciosas.
- Botón "reportar QR" público → bloqueo manual.
- Rate limit por IP en el panel (bcrypt/magic link, sin contraseñas guardadas).
- Aviso de privacidad mínimo en landing (recopila email de la lista de espera).
