# QR Vivo — Códigos QR dinámicos para negocios locales

> **Un QR impreso hoy, válido mañana, cambiado por ti en 10 segundos.**
> El cliente modifica todo por sí solo, sin interactuar con nadie.

## 📌 Estado actual

| Fase | Estado |
|---|---|
| Landing de validación | ✅ Publicada — https://alfacomputacion2024-lab.github.io/qrvivo/ |
| Validación con clientes | ⬜ Pendiente (10 visitas + 20 WhatsApp) |
| MVP (panel + redirección) | ⬜ Pendiente |
| Primeros 5 clientes pagando | ⬜ Pendiente |

## 💡 Qué es

SaaS que permite crear **QRs dinámicos**: el QR guarda una dirección corta nuestra que redirige al destino que elija el dueño del negocio. Así puede **cambiar el enlace sin reimprimir** el papel y además **mide los escaneos**.

**Problema que resuelve**: un restaurante que imprime 300 menús y cambia la carta debe reimprimir todo (≈300 €). Con QR Vivo solo cambia el enlace desde el móvil.

## 🎯 Posicionamiento

1. **Autogestión total** — *"Si sabes usar WhatsApp, sabes usar QR Vivo"*. Todo se edita solo desde el panel, 24/7, sin llamar a nadie.
2. **Diseño incluido** — plantillas profesionales de carta, cartel y tarjeta (diferencial de nuestro fundador diseñador frente a competencia extranjera).
3. **Servicio cercano y en español** — la competencia grande (QR Tiger, Flowcode) no visita tu barrio.

## 💰 Precios

| Plan | Precio | Contenido |
|---|---|---|
| **Gratis** | 0 $ | QRs estáticos ilimitados + 2 dinámicos + 100 escaneos/mes + 1 plantilla premium de cortesía (con marca QR Vivo) |
| **Negocio** ⭐ | **8 $/mes** | Ilimitado, sin marca, colores/logo, SVG, plantillas premium, edición autónoma 24/7, soporte prioritario |
| **Agencia/Imprenta** | 29 $/mes | Marca blanca, subcuentas, CSV masivo |

- **Edición Fundadores**: primeros 50 negocios pagan **8 $ para siempre** (luego 12 $) + plantilla personalizada lista para editar.
- **Garantía 30 días**: si no ahorra en reimpresiones, se devuelve el pago.

## 📂 Estructura del repo

```
landing-qr/           ← carpeta local (repo remoto: qrvivo)
├── index.html        ← landing de una sola página (hero, logos, demo QR real, precios, FAQ, CTA)
├── README.md         ← este archivo (visión general)
├── PLAN.md           ← plan de acción de lanzamiento por fases + scripts + KPIs
├── ESTRATEGIA.md     ← modelo de negocio, freemium, rentabilidad y competencia
└── MVP.md            ← arquitectura técnica del producto mínimo
```

## 🔗 Enlaces

- **Landing en vivo**: https://alfacomputacion2024-lab.github.io/qrvivo/
- **Repo**: https://github.com/alfacomputacion2024-lab/qrvivo
- Correo de contacto (pendiente): hola@[dominio-por-definir]

## 🚀 Cómo actualizar la landing

```bash
# Edita index.html, y luego:
git add index.html
git commit -m "Descripción del cambio"
git push
```
GitHub Pages se redespliega solo en ~1 minuto.
