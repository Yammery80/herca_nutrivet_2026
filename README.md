# NutriVet Pro 🌿

Sistema de gestión para veterinaria / distribuidora de alimentos balanceados.

## Estructura del proyecto

```
nutrivet/
├── public/
│   └── index.html      ← Toda la aplicación (sin dependencias externas de build)
├── netlify.toml        ← Configuración para Netlify
├── firebase.json       ← Configuración para Firebase Hosting
├── .firebaserc         ← ID de tu proyecto Firebase
└── README.md
```

---

## 🚀 Despliegue en Netlify

### Opción A — Arrastrar y soltar (más fácil, sin cuenta GitHub)

1. Ve a **https://app.netlify.com/drop**
2. Arrastra la carpeta **`public/`** al área de drop
3. ¡Listo! Netlify te da una URL tipo `https://algo-random.netlify.app`
4. Para tener tu propio dominio: Site settings → Domain management → Add custom domain

### Opción B — Desde GitHub (recomendado para actualizaciones automáticas)

```bash
# 1. Sube el proyecto a GitHub
git init
git add .
git commit -m "NutriVet Pro v1.0"
git remote add origin https://github.com/TU-USUARIO/nutrivet-pro.git
git push -u origin main

# 2. En Netlify: "Add new site" → "Import from Git" → selecciona el repo
# Build settings:
#   Publish directory: public
#   (Sin build command, es HTML puro)
```

---

## 🔥 Despliegue en Firebase Hosting

### Paso 1 — Instalar Firebase CLI

```bash
npm install -g firebase-tools
```

### Paso 2 — Iniciar sesión

```bash
firebase login
```

### Paso 3 — Configurar tu proyecto

Edita `.firebaserc` y reemplaza `TU-PROYECTO-FIREBASE-ID` con el ID de tu proyecto en Firebase Console (https://console.firebase.google.com).

```json
{
  "projects": {
    "default": "nutrivet-pro-abc12"   ← tu ID aquí
  }
}
```

### Paso 4 — Desplegar

```bash
cd nutrivet/
firebase deploy --only hosting
```

La URL quedará como: `https://nutrivet-pro-abc12.web.app`

---

## 📱 Características

- **Cotizaciones** primero — acceso directo desde la barra lateral
  - 3 modos: por kg totales / por kg de maíz / por presupuesto
  - Margen de ganancia con slider
  - Guardar, enviar por WhatsApp, convertir a venta
- **Dashboard** con gráfica de ventas y top fórmulas
- **Fórmulas nutricionales** por especie y etapa productiva
- **Calculadora** de ingredientes
- **Ventas** con cambio de estado y remisiones
- **Clientes** con RFC y historial
- **Reportes** exportables

## 🛠 Siguiente paso — Base de datos Firebase

Para guardar datos en la nube (en lugar de solo en el navegador), puedes agregar Firebase Firestore:

```html
<!-- Agrega en el <head> de index.html -->
<script type="module">
  import { initializeApp } from "https://www.gstatic.com/firebasejs/10.0.0/firebase-app.js";
  import { getFirestore } from "https://www.gstatic.com/firebasejs/10.0.0/firebase-firestore.js";

  const firebaseConfig = {
    apiKey: "TU-API-KEY",
    authDomain: "TU-PROYECTO.firebaseapp.com",
    projectId: "TU-PROYECTO-ID",
  };

  const app = initializeApp(firebaseConfig);
  const db = getFirestore(app);
  window._db = db; // disponible globalmente
</script>
```

Solicita a Claude que agregue la sincronización con Firestore cuando estés listo.
