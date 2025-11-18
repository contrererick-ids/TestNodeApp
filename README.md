# TestNodeApp - GitHub Actions con Contenedores

![Node.js](https://img.shields.io/badge/Node.js-16-green)
![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-CI%2FCD-blue)
![Docker](https://img.shields.io/badge/Container-node:16-blue)

## 📋 Descripción

Este repositorio demuestra la implementación de **GitHub Actions con contenedores Docker** para ejecutar pipelines de CI/CD. El proyecto utiliza una aplicación Node.js simple que emplea la librería `moment` para ilustrar cómo configurar workflows automatizados que se ejecutan dentro de contenedores.

## 🎯 Objetivo

El objetivo principal es demostrar:

- ✅ Configuración de GitHub Actions con contenedores Docker
- ✅ Ejecución de aplicaciones Node.js en entornos containerizados
- ✅ Gestión de dependencias en pipelines de CI/CD
- ✅ Automatización de pruebas y validaciones en cada push

## 🏗️ Estructura del Proyecto

```
TestNodeApp/
├── .github/
│   └── workflows/
│       └── build.yml          # Workflow de GitHub Actions
├── node_modules/              # Dependencias (generado)
├── app.js                     # Aplicación principal
├── package-lock.json          # Lock file de dependencias
├── package.json               # Configuración del proyecto
└── README.md                  # Este archivo
```

## 📦 Aplicación (app.js)

La aplicación Node.js realiza operaciones básicas:

```javascript
const moment = require('moment');
let i = 5;
let j = 10;
console.log("Iniciando...");
console.log('La suma de es: ' + (5+10));

let fecha = moment().format('LL');
console.log('Y la fecha es: ' + fecha);
```

**Funcionalidades:**
- Suma de dos números
- Formateo de fecha actual usando `moment.js`
- Demostración de uso de dependencias npm

## ⚙️ GitHub Actions Workflow

### Archivo: `.github/workflows/build.yml`

```yaml
on: push
jobs:
  build-node:
    runs-on: ubuntu-latest
    container: node:16
    steps:
      - run: echo "TESTING"
      - run: node --version
      - run: npm --version
      - uses: actions/checkout@v3
      - run: npm install
      - run: node app.js
```

### 🔍 Explicación del Workflow

| Step | Comando | Descripción |
|------|---------|-------------|
| **1** | `echo "TESTING"` | Imprime mensaje de inicio |
| **2** | `node --version` | Verifica versión de Node.js |
| **3** | `npm --version` | Verifica versión de npm |
| **4** | `actions/checkout@v3` | Clona el repositorio |
| **5** | `npm install` | ⚠️ **CRÍTICO**: Instala dependencias |
| **6** | `node app.js` | Ejecuta la aplicación |

### 🐳 Características del Contenedor

- **Imagen base**: `node:16`
- **Runner**: `ubuntu-latest`
- **Trigger**: Se ejecuta en cada `push`

## ⚠️ Problema Común y Solución

### Error: `MODULE_NOT_FOUND`

```bash
Error: Cannot find module 'moment'
code: 'MODULE_NOT_FOUND'
```

**Causa**: No se instalaron las dependencias antes de ejecutar la aplicación.

**Solución**: Asegurarse de incluir `npm install` en el workflow antes de `node app.js`.

## 🚀 Cómo Usar Este Repositorio

### 1. Clonar el repositorio
```bash
git clone https://github.com/tu-usuario/TestNodeApp.git
cd TestNodeApp
```

### 2. Instalar dependencias localmente
```bash
npm install
```

### 3. Ejecutar la aplicación
```bash
node app.js
```

### 4. Push para activar GitHub Actions
```bash
git add .
git commit -m "Test GitHub Actions"
git push origin main
```

## 📊 Dependencias

```json
{
  "dependencies": {
    "moment": "^2.29.x"
  }
}
```

## 🔑 Conceptos Clave

### GitHub Actions con Contenedores

1. **Aislamiento**: Cada job se ejecuta en un contenedor limpio
2. **Reproducibilidad**: Mismo entorno en cada ejecución
3. **Portabilidad**: Funciona igual localmente y en la nube
4. **Escalabilidad**: Fácil de replicar y modificar

### Ventajas de Usar Contenedores

- ✅ Entorno consistente y predecible
- ✅ No contamina el sistema host
- ✅ Fácil cambio de versiones de Node.js
- ✅ Mejor gestión de dependencias del sistema

## 📝 Notas Importantes

- El contenedor se destruye después de cada ejecución
- Las dependencias deben instalarse en cada run
- Los archivos generados no persisten entre ejecuciones
- El código fuente se obtiene mediante `actions/checkout`

## 🎓 Aprendizajes

Este proyecto enseña:

1. Configuración básica de GitHub Actions
2. Uso de contenedores en workflows
3. Gestión de dependencias en CI/CD
4. Debugging de errores comunes en pipelines
5. Best practices para automatización

## 🤝 Contribuir

Las contribuciones son bienvenidas. Por favor:

1. Fork el proyecto
2. Crea una rama (`git checkout -b feature/nueva-funcionalidad`)
3. Commit tus cambios (`git commit -m 'Agrega nueva funcionalidad'`)
4. Push a la rama (`git push origin feature/nueva-funcionalidad`)
5. Abre un Pull Request

## 📄 Licencia

Este proyecto es de código abierto y está disponible para fines educativos.

---

**Desarrollado con fines educativos para demostrar GitHub Actions con contenedores** 🚀
