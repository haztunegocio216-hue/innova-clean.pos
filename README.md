# innova-clean-pos

PWA de Punto de Venta para InnovaClean.

## Estructura

```
innova-clean-pos/
├── index.html          ← App principal (todo en un archivo)
├── manifest.json       ← Configuración PWA
├── sw.js               ← Service Worker (offline)
├── vercel.json         ← Deploy en Vercel
├── generate-icons.html ← Generador de íconos PWA
├── icons/              ← Carpeta para íconos (ver abajo)
└── README.md
```

## Íconos PWA

1. Abre `generate-icons.html` en tu navegador
2. Se descargarán automáticamente los íconos: `icon-72.png`, `icon-96.png`, `icon-128.png`, `icon-192.png`, `icon-512.png`
3. Crea la carpeta `icons/` y mueve ahí los archivos descargados

## Supabase — Tablas requeridas

### `ic_productos`
| columna | tipo |
|---------|------|
| id | int8 PK |
| nombre | text |
| categoria | text |
| precio | numeric |
| costo | numeric |
| stock | int4 |
| stock_min | int4 |
| sku | text |
| descripcion | text |
| created_at | timestamptz |

### `ic_pedidos`
| columna | tipo |
|---------|------|
| id | int8 PK |
| fecha | timestamptz |
| cliente_id | int8 FK → ic_clientes |
| turno_id | int8 FK → ic_turnos |
| subtotal | numeric |
| descuento | numeric |
| total | numeric |
| forma_pago | text |
| nota | text |
| estado | text |
| items | text (JSON) |

### `ic_clientes`
| columna | tipo |
|---------|------|
| id | int8 PK |
| nombre | text |
| telefono | text |
| email | text |
| direccion | text |
| notas | text |
| total_compras | numeric |
| ultima_compra | timestamptz |
| created_at | timestamptz |

### `ic_turnos`
| columna | tipo |
|---------|------|
| id | int8 PK |
| cajero | text |
| fondo | numeric |
| apertura | timestamptz |
| cierre | timestamptz |
| estado | text |
| total_ventas | int4 |
| total_monto | numeric |
| observaciones | text |
| created_at | timestamptz |

## Deploy en Vercel

```bash
# Instala Vercel CLI
npm i -g vercel

# Desde la carpeta del proyecto
vercel

# O conecta el repo de GitHub en vercel.com → Import Project
```

## Deploy en GitHub Pages

```bash
git init
git add .
git commit -m "Initial commit - InnovaClean POS"
git remote add origin https://github.com/TU_USUARIO/innova-clean-pos.git
git push -u origin main
```

Luego en Settings → Pages → Source: `main` branch, `/ (root)`.

## Módulos

- **Ventas** — Catálogo de productos, carrito, descuentos, formas de pago, cambio
- **Inventario** — CRUD productos, filtros por categoría y stock
- **Historial** — Todos los pedidos con filtros de fecha y estado
- **Corte de Caja** — Apertura/cierre de turnos, resumen
- **Clientes** — CRUD clientes, búsqueda
- **Reportes** — Estadísticas con gráficas (ventas 7 días, top productos, formas de pago)
- **Ticket PDF** — Generación de ticket y envío por WhatsApp
