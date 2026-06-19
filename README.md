# MiCasita SUS — Evaluación de Usabilidad OE4 · UPC 2026

Proyecto fullstack para recolección y análisis de datos SUS (System Usability Scale) de la app MiCasita.

```
SUS-Micasita/
├── backend/          ← Node.js + Express + PostgreSQL (deploy Railway)
│   ├── server.js
│   ├── package.json
│   ├── .env.example
│   └── README.md
├── frontend/         ← index.html único (deploy Netlify)
│   └── index.html
└── README.md
```

---

## Deploy Backend en Railway

1. Ir a [railway.app](https://railway.app) → **New Project**
2. **Add service → Database → PostgreSQL**
   Railway crea la base de datos y genera automáticamente la variable `DATABASE_URL`
3. **Add service → GitHub repo** → seleccionar la carpeta `/backend`
   (Si el repo tiene ambas carpetas, en Railway puedes configurar el Root Directory como `backend`)
4. En el servicio backend → **Variables** → agregar:
   ```
   DATABASE_URL  = (copiar del plugin PostgreSQL de Railway)
   PORT          = 3000
   FRONTEND_URL  = https://tu-app.netlify.app
   ```
5. Railway detecta `package.json` y ejecuta `npm start` automáticamente
6. **La tabla `sus_sessions` se crea sola al iniciar** — no se necesitan migraciones manuales
7. Copiar la URL pública del backend (ej: `https://micasita-sus-production.railway.app`)

---

## Deploy Frontend en Netlify

1. Editar `frontend/index.html` — cambiar la línea:
   ```js
   const API_URL = 'https://TU-APP.railway.app'
   ```
   por la URL real del backend obtenida en Railway
2. Ir a [app.netlify.com](https://app.netlify.com) → **Add new site → Deploy manually**
3. Arrastrar la carpeta `/frontend` al área de drop
4. La URL queda disponible en segundos

---

## Desarrollo local

### Backend
```bash
cd backend
npm install
cp .env.example .env
# Editar .env con tus credenciales de PostgreSQL local
npm run dev
# Servidor en http://localhost:3000
# La tabla se crea automáticamente
```

### Frontend
```
Abrir frontend/index.html con Live Server en VS Code
Asegurarse de que API_URL apunte a http://localhost:3000
```

---

## Endpoints API

| Método | Ruta | Descripción |
|---|---|---|
| GET | `/api/health` | Estado del servidor |
| GET | `/api/sessions` | Listar sesiones (JSON) |
| POST | `/api/sessions` | Crear sesión (calcula SUS Score en backend) |
| DELETE | `/api/sessions/:id` | Eliminar sesión |
| GET | `/api/stats` | Estadísticas agregadas (KPIs + promedios Q + por transporte) |
| GET | `/api/sessions/export/csv` | Exportar todo como CSV con BOM para Excel |
