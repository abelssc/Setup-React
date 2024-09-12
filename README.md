# Crea carpetas para un proyecto completo de react

* Primero debes haber ejecutado vite; npm create vite@latest
* Asegúrate de que estás en la raíz del proyecto y el archivo setup.js está en la misma carpeta que package.json
* Asegúrate de que tu archivo package.json tenga "type": "module"
* Ejecuta el siguiente comando en la terminal node setup.js

![files](files.png)

```js
import { fileURLToPath } from 'url';
import { dirname, join, extname } from 'path';
import { existsSync, mkdirSync, writeFileSync } from 'fs';

// Obtener la ruta del archivo actual
const __filename = fileURLToPath(import.meta.url);
const __dirname = dirname(__filename);

// Lista de carpetas y archivos a crear
const directories = [
  '.env.production',
  '.env',
  'src/routes',
  'src/routes/Routes.jsx',
  'src/services',
  'src/styles',
  'src/styles/index.css',
  'src/utils',
  'src/utils/helpers.js',
  'src/assets',
  'src/components',
  'src/components/layouts',
  'src/components/common',
  'src/config',
  'src/config/axios.js',
  'src/context',
  'src/hooks',
  'src/pages',
];

// Función para crear carpetas y archivos
directories.forEach((item) => {
  const fullPath = join(__dirname, item);
  
  // Si es una carpeta (sin extensión), crearla
  if (!extname(fullPath)) {
    if (!existsSync(fullPath)) {
      mkdirSync(fullPath, { recursive: true });
      console.log(`Carpeta creada: ${fullPath}`);
    }
  } 
  // Si es un archivo (con extensión), crearlo
  else {
    const dirName = dirname(fullPath);
    if (!existsSync(dirName)) {
      mkdirSync(dirName, { recursive: true });
    }
    if (!existsSync(fullPath)) {
      writeFileSync(fullPath, '');
      console.log(`Archivo creado: ${fullPath}`);
    }
  }
});
  
  console.log('Carpetas y archivos creados exitosamente.');
```
