# Fisiourense API

API backend para la integración de Gemini AI en el sitio web de Fisiourense.

## 🚀 Despliegue en Vercel

### Paso 1: Instalar Vercel CLI (opcional)

```bash
npm install -g vercel
```

### Paso 2: Desplegar el proyecto

**Opción A: Desde la línea de comandos**

1. Abre una terminal en esta carpeta (`fisiourense-api`)
2. Ejecuta:
   ```bash
   vercel
   ```
3. Sigue las instrucciones:
   - Login con tu cuenta de Vercel
   - Confirma el nombre del proyecto
   - Selecciona tu scope/team

**Opción B: Desde el Dashboard de Vercel (Recomendado)**

1. Ve a [vercel.com](https://vercel.com)
2. Haz clic en "Add New" → "Project"
3. Importa este repositorio o sube la carpeta `fisiourense-api`
4. Vercel detectará automáticamente la configuración
5. Haz clic en "Deploy"

### Paso 3: Configurar la variable de entorno

**IMPORTANTE:** Debes configurar la API key de Gemini en Vercel.

1. Ve a tu proyecto en Vercel
2. Settings → Environment Variables
3. Añade:
   - **Name**: `GEMINI_API_KEY`
   - **Value**: Tu clave API de Gemini (obtenerla en [Google AI Studio](https://aistudio.google.com/app/apikey))
   - **Environment**: Production, Preview, Development
4. Guarda y redeploy el proyecto

### Paso 4: Obtener la URL de tu API

Después del despliegue, Vercel te dará una URL como:
```
https://fisiourense-api.vercel.app
```

Tu endpoint de API será:
```
https://fisiourense-api.vercel.app/api/analyze
```

### Paso 5: Actualizar el dominio en CORS

1. Abre `api/analyze.js`
2. En la línea 6, actualiza los dominios permitidos:
   ```javascript
   const allowedOrigins = [
     'https://tudominio.com',        // ← Cambia esto
     'https://www.tudominio.com',    // ← Y esto
     'http://localhost:3000',
   ];
   ```
3. Guarda y redeploy

## 🔧 Configuración del Frontend

Después de desplegar la API, actualiza el archivo `js/main.js` en tu sitio web de Hostinger:

```javascript
// Línea 319 aproximadamente
const response = await fetch('https://TU-PROYECTO.vercel.app/api/analyze', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ userInput: userInput }),
});
```

Reemplaza `TU-PROYECTO` con la URL real de tu despliegue en Vercel.

## 📝 Estructura del Proyecto

```
fisiourense-api/
├── api/
│   └── analyze.js      # Función serverless con Gemini
├── package.json        # Configuración del proyecto
├── vercel.json         # Configuración de Vercel
└── README.md           # Este archivo
```

## 🧪 Probar la API

Puedes probar tu API con curl:

```bash
curl -X POST https://TU-PROYECTO.vercel.app/api/analyze \
  -H "Content-Type: application/json" \
  -d '{"userInput": "Me duele la espalda baja"}'
```

O con Postman/Thunder Client.

## 🔒 Seguridad

- ✅ La API key nunca se expone en el frontend
- ✅ CORS configurado para permitir solo dominios específicos
- ✅ Validación de métodos HTTP
- ✅ Variables de entorno en Vercel

## 📞 Soporte

Si tienes problemas:
1. Verifica que la variable `GEMINI_API_KEY` está configurada en Vercel
2. Revisa los logs en el Dashboard de Vercel
3. Asegúrate de que los dominios CORS están correctamente configurados
