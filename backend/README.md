# MiCasita SUS Backend

API REST para recolección de datos de usabilidad SUS de la app MiCasita.

## Instalación local

```bash
npm install
cp .env.example .env
# Editar .env con tus credenciales de PostgreSQL
npm run dev
```

La tabla `sus_sessions` se crea automáticamente al iniciar el servidor (IF NOT EXISTS).

## Variables de entorno

| Variable | Descripción |
|---|---|
| `DATABASE_URL` | Cadena de conexión PostgreSQL |
| `PORT` | Puerto del servidor (default: 3000) |
| `FRONTEND_URL` | URL del frontend para CORS |

## Endpoints

| Método | Ruta | Descripción |
|---|---|---|
| GET | `/api/health` | Estado del servidor |
| GET | `/api/sessions` | Listar todas las sesiones |
| POST | `/api/sessions` | Crear sesión (calcula SUS Score) |
| DELETE | `/api/sessions/:id` | Eliminar sesión |
| GET | `/api/stats` | Estadísticas agregadas |
| GET | `/api/sessions/export/csv` | Exportar todo como CSV |

## Deploy en Railway

1. Ir a [railway.app](https://railway.app) → New Project
2. Add service → Database → PostgreSQL (Railway crea la DB y genera `DATABASE_URL`)
3. Add service → GitHub repo → seleccionar carpeta `/backend`
4. En el servicio backend → Variables → agregar:
   - `DATABASE_URL` = (copiar del plugin PostgreSQL de Railway)
   - `PORT` = `3000`
   - `FRONTEND_URL` = `https://tu-app.netlify.app`
5. Railway detecta `package.json` y ejecuta `npm start` automáticamente
6. La tabla se crea sola al arrancar — no necesitas correr migraciones
7. Copiar la URL pública del backend (ej: `https://micasita-sus.railway.app`)
