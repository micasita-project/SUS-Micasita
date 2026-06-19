# MiCasita SUS — Frontend

Formulario de evaluación SUS y dashboard de resultados para MiCasita (OE4-I1).  
Sitio estático — un único archivo `index.html`, sin dependencias de build.

---

## Uso local

Abrir con Live Server (extensión VS Code) en `http://127.0.0.1:5500`.  
**No abrir como `file://`** — los navegadores bloquean peticiones fetch desde ese protocolo.

---

## Configurar la URL del backend

En `index.html` buscar la constante `API_URL` (~línea 530):

```js
const API_URL = (() => {
  const h = location.hostname;
  if (h === 'localhost' || h === '127.0.0.1' || location.protocol === 'file:')
    return 'http://localhost:3000';
  return 'https://TU-BACKEND.up.railway.app'; // <-- reemplazar con URL de Railway
})();
```

Reemplazar `https://TU-BACKEND.up.railway.app` con la URL real del backend en Railway  
**antes de hacer push** al repo de frontend.

---

## Deploy en Netlify

1. Subir este repositorio a GitHub
2. [netlify.com](https://netlify.com) → **Add new site** → Import from Git
3. Configuración de build:
   - **Build command**: *(dejar vacío)*
   - **Publish directory**: `.` (raíz del repo, donde está `index.html`)
4. Deploy → Netlify genera una URL (ej. `https://micasita-sus.netlify.app`)
5. Copiar esa URL y agregarla a la variable `FRONTEND_URL` del backend en Railway

---

## Estructura

```
frontend/
└── index.html    # App completa (formulario + dashboard + registros)
```
