# 🚀 Cómo ejecutar el proyecto en VS Code

## Requisitos previos

Instala estas herramientas si no las tienes:

| Herramienta | Versión mínima | Descarga |
|-------------|---------------|---------|
| Node.js     | 20.x LTS      | https://nodejs.org |
| Angular CLI | 19.x          | `npm install -g @angular/cli` |
| VS Code     | cualquiera    | https://code.visualstudio.com |

---

## Pasos para correr el proyecto

### 1. Extrae el ZIP

```
foro-cnpcyf/
├── src/
├── angular.json
├── package.json
├── tsconfig.json
├── tailwind.config.ts
└── foro-cnpcyf.code-workspace   ← abre este en VS Code
```

### 2. Abre en VS Code

Haz doble clic en **`foro-cnpcyf.code-workspace`**
_(o desde VS Code: File → Open Workspace from File)_

### 3. Instala dependencias

Abre la terminal integrada en VS Code (`Ctrl+\``) y ejecuta:

```bash
npm install
```

> Tarda ~1-2 min la primera vez.

### 4. Lanza el servidor

```bash
ng serve --open
```

El navegador se abrirá automáticamente en **http://localhost:4200**

---

## Extensiones recomendadas para VS Code

VS Code te las sugerirá automáticamente al abrir el workspace.
Acéptalas todas para tener:

- **Angular Language Service** — autocompletado en templates HTML
- **Tailwind CSS IntelliSense** — sugerencias de clases inline
- **Prettier** — formateo automático al guardar
- **ESLint** — errores de código en tiempo real

---

## Rutas disponibles

| URL | Página |
|-----|--------|
| http://localhost:4200/ | → redirige a Inicio |
| http://localhost:4200/inicio | Página principal |
| http://localhost:4200/programa | Agenda del foro |
| http://localhost:4200/ponentes | Speakers |
| http://localhost:4200/ubicacion | Mapa y hoteles |
| http://localhost:4200/registro | Formulario de registro |
| http://localhost:4200/emergencia | Números de emergencia |

---

## Configuración de Tailwind v4 (ya incluida)

Tailwind v4 usa un plugin de **Vite** en lugar de PostCSS.
Angular 19+ usa Vite internamente, así que ya funciona sin configuración extra.

Si necesitas añadir la config manualmente en un proyecto nuevo:

```ts
// vite.config.ts (si lo necesitas exponer)
import { defineConfig } from 'vite';
import tailwindcss from '@tailwindcss/vite';

export default defineConfig({
  plugins: [tailwindcss()],
});
```

Los colores y tokens están definidos en `src/styles.css` con `@theme { }`.

---

## Estructura atómica

```
src/app/
├── shared/
│   ├── atoms/          ← ButtonComponent, IconComponent, BadgeComponent...
│   ├── molecules/      ← SpeakerCardComponent, ScheduleItemComponent...
│   ├── organisms/      ← NavbarComponent, FooterComponent, RegistrationFormComponent...
│   └── templates/      ← MainLayoutComponent (navbar + router-outlet + footer)
└── pages/              ← InicioComponent, ProgramaComponent, etc.
```

Para agregar un nuevo componente atómico:
```bash
ng g c shared/atoms/mi-atom --standalone
```
