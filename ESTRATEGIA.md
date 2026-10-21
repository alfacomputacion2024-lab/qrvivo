# 💰 Estrategia de Negocio — QR Vivo

## 1. Propuesta de valor central

> **"Cambia el destino de tus QR sin reimprimir nunca — tú mismo, desde tu móvil, sin llamar a nadie."**

Tres pilares:
1. **Autogestión total** — el cliente edita destino, colores, logo y descargas él solo, 24/7. *Soporte = por si acaso, no porque lo necesites.* Esto además protege la rentabilidad (soporte ≈ 0 h).
2. **Diseño incluido** — plantillas profesionales (carta, cartel, tarjeta). Ventaja del fundador diseñador: la competencia extranjera no diseña.
3. **Cercanía local y español** — venta presencial y soporte humano; QR Tiger/Flowcode/Bitly no visitan el barrio.

## 2. Por qué dinámico = dinero

| | QR estático | QR dinámico |
|---|---|---|
| Destino cambiante | No (reimprimir) | **Sí, 10 segundos desde el panel** |
| Analítica | No | **Sí: escaneos, hora, dispositivo** |
| Coste para el cliente | "Gratis" | **8 $/mes** (ahorra ≈300 €/reimpresión) |

El cliente no paga "un QR": paga **dejar de reimprimir y saber cuánta gente escanea**.

## 3. Estructura de precios (acordada: 9 $ → 8 $)

| Plan | Precio | Límites y contenido |
|---|---|---|
| **Gratis** | 0 $ | QRs estáticos ilimitados + **2 QRs dinámicos** + 100 escaneos/mes + **1 plantilla premium de cortesía** + marca QR Vivo |
| **Negocio** ⭐ | 8 $/mes | Todo ilimitado · sin marca · colores y logo · SVG gran formato · todas las plantillas premium · edición autónoma 24/7 · soporte prioritario ES |
| **Agencia/Imprenta** | 29 $/mes | Marca blanca (panel y QRs con su logo) · subcuentas · CSV masivo · atención comercial |

### Lógica del freemium "exclusivo pero limitado"
- El gratis **sí regala 1 plantilla premium** → el usuario prueba la joya y ve la calidad de pago.
- Los límites son de **cantidad** (2 QRs, 100 escaneos), nunca de calidad percibida.
- La marca "QR Vivo" en el gratis es el motor de conversión orgánica (cada QR impreso es publicidad).

### Edición Fundadores (exclusividad real)
- **Primeros 50 negocios: 8 $/mes para siempre** (precio normal subirá a **12 $**).
- Incluye plantilla personalizada lista para editar.
- Cuándo subir el precio: soporte >3 h/semana con >25 clientes → **12 $ para nuevos**, fundadores intactos.

### Extras de conversión
- **Garantía 30 días**: "si no ahorras en reimpresiones, te devolvemos lo pagado".
- Plan **anual 77 $** (2 meses gratis) → caja por adelantado, menos gestión. Cobrar siempre en **USD**.

## 4. Rentabilidad (hosting y compañías)

### Costes fijos
| Concepto | Coste |
|---|---|
| Cloudflare Workers (redirección + contador) — gratis hasta 100.000 escaneos/día | **0 $** |
| Cloudflare D1 (base de datos) — gratis hasta 5 GB | **0 $** |
| Dominio .com | ≈1,2 $/mes |
| Lemon Squeezy / Paddle (pagos + impuestos) | 0 $ fijo (c por transacción) |
| MailerLite (email) — gratis <1.000 suscriptores | 0 $ |
| **Total fijo** | **≈1,2 $/mes** |

### Margen por cliente
```
8,00 $ − 5 % Lemon Squeezy (0,40 $) − 0,50 $ fijo = 7,10 $ netos
```
**Punto de equilibrio: 1 cliente.** A escala: si superan los límites gratis, Workers de pago cuesta 5 $/mes (sigue rentable desde el cliente 2).

## 5. Competencia

| Competencia | Qué hace | Nuestra ventaja |
|---|---|---|
| QR Tiger, Flowcode, Beaconstac, Bitly QR | SaaS genérico, 5-30 $/mes, en inglés | Vertical local + venta presencial + soporte en español + diseño incluido |
| Generadores gratuitos (varios) | QR estático sin analytics | El dinámico requiere servidor → es lo que se cobra; gratis es nuestro imán |
| "Un primo que sabe de esto" | QR fijo hecho a mano | Panel autogestionable + analítica + profesionalidad visual |

**No competimos en precio ni en features totales: competimos en cercanía, servicio y diseño.**

## 6. Nichos (orden de facilidad de venta)

1. **Restaurantes/cafés/bars** — menús; entienden al instante, renuevan siempre.
2. **Imprentas** — canal B2B: imprimen para muchos clientes ⇒ multiplicador.
3. **Inmobiliarias** — QR por cartel; cambian al bajar precio.
4. **Agencias/diseñadores** — ponen QR en materiales de clientes (red natural del fundador).
5. **Museos/rutas turísticas** — QR por punto de interés.

## 7. Riesgos y mitigación

| Riesgo | Mitigación |
|---|---|
| Mercado concurrido | Nicho vertical + servicio cercano; no competir en precio |
| QR usado para phishing | Botón de reporte + bloqueo de dominios; reputación del dominio |
| Caída del servicio = QRs muertos | Cloudflare (muy fiable) + plan de emergencia (código de respaldo) |
| Soporte que se come las horas | **Autogestión como promesa central**; docs cortos en vídeo |
| Nadie paga | Validación en Fase 1 con pre-pagos ANTES de construir |

## 8. Diferenciadores de marketing (resumen para copy)

- *"El QR que nunca caduca"*
- *"Tú lo cambias en 10 segundos, sin llamar a nadie"*
- *"Ahórrate 300 € de reimpresión por 8 $"*
- *"Si sabes usar WhatsApp, sabes usar QR Vivo"*
- *"Primeros 50: precio de fundador para siempre"*
