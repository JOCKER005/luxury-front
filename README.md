<<<<<<< HEAD
# nesha-front
=======
# Luxe Joyería — Full Stack

E-commerce de joyería con React (frontend) + FastAPI Python (backend) + Mercado Pago.

## Estructura del proyecto

```
luxe-joyeria/
├── backend/               ← API Python (FastAPI)
│   ├── main.py            ← Endpoints: productos, pagos, admin, Excel
│   ├── models.py          ← Tablas SQLAlchemy
│   ├── schemas.py         ← Validación Pydantic
│   ├── database.py        ← Conexión SQLite / PostgreSQL
│   ├── requirements.txt
│   └── .env.example
│
└── frontend/              ← React + Vite + Tailwind
    ├── src/
    │   ├── App.tsx
    │   ├── main.tsx
    │   ├── index.css
    │   ├── lib/
    │   │   ├── api.ts     ← Cliente HTTP al backend
    │   │   └── utils.ts
    │   ├── hooks/
    │   │   └── useProducts.ts   ← React Query hooks
    │   ├── context/
    │   │   └── cart-context.tsx ← Carrito global
    │   ├── components/
    │   │   ├── cart/CartDrawer.tsx
    │   │   ├── layout/Navbar.tsx
    │   │   ├── layout/Footer.tsx
    │   │   └── ui/ProductCard.tsx
    │   └── pages/
    │       ├── Home.tsx
    │       ├── Catalog.tsx
    │       ├── ProductDetail.tsx
    │       ├── Checkout.tsx
    │       ├── Admin.tsx
    │       └── not-found.tsx
    ├── index.html
    ├── vite.config.ts
    ├── tsconfig.json
    ├── package.json
    └── .env.example
```

---

## Setup Local (Desarrollo)

### 1. Backend

```bash
cd backend

# Crear entorno virtual
python -m venv venv
source venv/bin/activate          # Mac/Linux
# venv\Scripts\activate           # Windows

# Instalar dependencias
pip install -r requirements.txt

# Configurar variables de entorno
cp .env.example .env
# Editar .env con tu MP_ACCESS_TOKEN real

# Levantar servidor
uvicorn main:app --reload --port 8000
```

La API estará en `http://localhost:8000`  
Docs interactivos: `http://localhost:8000/docs`

### 2. Frontend

```bash
cd frontend

# Instalar dependencias
npm install

# Configurar variables de entorno
cp .env.example .env
# VITE_API_URL=http://localhost:8000
# VITE_ADMIN_SECRET=luxe-admin-secret-2024
# VITE_MP_PRODUCTION=false   ← sandbox

# Levantar dev server
npm run dev
```

El frontend estará en `http://localhost:5173`

---

## Deploy en Railway (Producción)

### Backend en Railway

1. Crear nuevo proyecto en [railway.app](https://railway.app)
2. "New Service" → "GitHub Repo" (o "Empty Service" + deploy desde CLI)
3. Agregar un servicio **PostgreSQL** — Railway inyecta `DATABASE_URL` automáticamente
4. Variables de entorno del servicio backend:

```
MP_ACCESS_TOKEN=APP_USR-tu-token-real
ADMIN_SECRET=tu-clave-secreta-segura
```

5. Start command: `uvicorn main:app --host 0.0.0.0 --port $PORT`

### Frontend en Vercel / Netlify

```bash
cd frontend
npm run build        # genera dist/
```

Variables de entorno en Vercel:
```
VITE_API_URL=https://tu-backend.railway.app
VITE_ADMIN_SECRET=tu-clave-secreta-segura
VITE_MP_PRODUCTION=true
```

---

## Panel Admin

Acceder en `/admin` (sin login por ahora, protegido por `ADMIN_SECRET` en headers).

Funcionalidades:
- ✅ Crear / editar / activar / destacar productos
- ✅ Ver y gestionar órdenes en tiempo real
- ✅ Cambiar estado de órdenes manualmente
- ✅ Exportar Libro Diario en Excel (.xlsx) con filtro por fecha

---

## Webhook de Mercado Pago

En tu cuenta de Mercado Pago, configurar el webhook apuntando a:

```
https://tu-backend.railway.app/api/payments/webhook
```

Esto actualiza automáticamente el estado de las órdenes y descuenta el stock cuando un pago es aprobado.

---

## Variables de entorno — Referencia completa

### Backend `.env`
| Variable | Descripción |
|---|---|
| `MP_ACCESS_TOKEN` | Access Token de Mercado Pago (Production) |
| `DATABASE_URL` | URL de la base de datos (SQLite o PostgreSQL) |
| `ADMIN_SECRET` | Clave secreta para el panel admin |

### Frontend `.env`
| Variable | Descripción |
|---|---|
| `VITE_API_URL` | URL del backend FastAPI |
| `VITE_ADMIN_SECRET` | Debe coincidir con `ADMIN_SECRET` del backend |
| `VITE_MP_PRODUCTION` | `true` para pagos reales, `false` para sandbox |
>>>>>>> b329276 (readme)
