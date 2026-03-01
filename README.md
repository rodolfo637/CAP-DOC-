# 📋 Gestión CAP — Sistema de Gestión Documental

**Zona 1131 — Dirección General de Cultura y Educación**

Sistema web de gestión documental para administración de documentación educativa entre zonas de inspección de la Provincia de Buenos Aires.

## 🚀 Stack

- **Frontend:** HTML5 + CSS3 + JavaScript ES Modules (Vanilla)
- **Backend:** Firebase (Auth + Firestore + Storage)
- **Hosting:** Firebase Hosting / GitHub Pages
- **CI/CD:** GitHub Actions
- **Diseño:** Playfair Display + DM Sans | Navy (#0f1d36) + Gold (#c8a951)

## 📁 Estructura

```
gestion-cap/
├── .github/workflows/deploy.yml   # CI/CD → Firebase
├── css/styles.css                  # Estilos globales
├── js/
│   ├── firebase-config.js          # Config Firebase (credenciales)
│   ├── firebase-config_example.js  # Template sin credenciales
│   ├── app-shell.js                # Sidebar, toast, utilidades
│   └── auth.js                     # Módulo autenticación
├── index.html                      # Login
├── panel.html                      # Dashboard
├── nueva-carga.html                # Formulario de carga
├── enviados.html                   # Documentos enviados
├── recibidos.html                  # Bandeja de recibidos
├── detalle.html                    # Detalle y revisión
├── firebase.json                   # Config hosting
├── firestore.rules                 # Reglas Firestore
├── storage.rules                   # Reglas Storage
└── README.md
```

## 🔐 Roles

| Rol | Permisos |
|-----|----------|
| **admin** | Acceso total |
| **inspector** | Revisar/aprobar/rechazar docs de su zona |
| **regional** | Revisar docs de todas las zonas |
| **secretario** | Cargar y enviar documentos |
| **director** | Cargar y enviar documentos |

## ⚙️ Setup Inicial

### 1. Firebase Console
1. Ir a [console.firebase.google.com](https://console.firebase.google.com/)
2. Activar **Authentication** (Email/Password), **Firestore** y **Storage**

### 2. Crear usuario admin
En **Authentication** crear un usuario. Luego en **Firestore → `usuarios/{uid}`**:
```json
{
  "nombre": "Administrador",
  "email": "admin@educacion.gob.ar",
  "rol": "admin",
  "zona": "1131",
  "activo": true
}
```

### 3. Deploy reglas
```bash
npm install -g firebase-tools
firebase login
firebase deploy --only firestore:rules,storage
```

### 4. Índices Firestore
Crear índices compuestos (se generan automáticamente al ejecutar queries):
- `documentos`: `creadoPor` + `fechaCreacion` DESC
- `documentos`: `destinatarioZona` + `fechaCreacion` DESC

## 🌐 Deploy

### GitHub Pages
```bash
git init && git add . && git commit -m "v1.0"
git remote add origin https://github.com/tu-usuario/gestion-cap.git
git push -u origin main
```
Settings → Pages → Source: main branch

### Firebase Hosting
```bash
firebase deploy --only hosting
```

## 📱 Zonas: 1101, 1111, 1121, 1131, 1141, 1151, 1161, 1171, 1181, 1191

---
Desarrollado por **Devimpulso** 🇦🇷
