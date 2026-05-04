# Foro Nacional CNPCyF — Angular 21 + Tailwind v4

Proyecto refactorizado en **Diseño Atómico** con Angular 21 (standalone) y Tailwind CSS v4.

---

## 🗂 Estructura de Carpetas

```
src/
├── main.ts
├── styles.css                          ← Tailwind v4 CSS-first + utilidades globales
└── app/
    ├── app.component.ts                ← Shell mínimo
    ├── app.config.ts                   ← Bootstrap standalone
    ├── app.routes.ts                   ← Rutas lazy-loaded
    │
    ├── core/
    │   └── tokens/
    │       └── design-tokens.ts        ← Colores, tipografía, nav links centralizados
    │
    └── shared/
        │
        ├── atoms/                      ── Unidades mínimas, sin dependencias propias
        │   ├── button/
        │   │   └── button.component.ts         (variantes: primary, secondary, ghost, gold)
        │   ├── icon/
        │   │   └── icon.component.ts           (wrapper Material Symbols)
        │   ├── badge/
        │   │   └── badge.component.ts          (gold, secondary, navy)
        │   ├── input-field/
        │   │   └── input-field.component.ts    (ControlValueAccessor, Registry style)
        │   └── section-label/
        │       └── section-label.component.ts  (eyebrow gold labels)
        │
        ├── molecules/                  ── Combinaciones de átomos
        │   ├── nav-link/
        │   │   └── nav-link.component.ts       (RouterLinkActive automático)
        │   ├── speaker-card/
        │   │   └── speaker-card.component.ts   (hover animation, gold accent)
        │   ├── schedule-item/
        │   │   └── schedule-item.component.ts  (agenda row con badge tipado)
        │   ├── emergency-contact/
        │   │   └── emergency-contact.component.ts
        │   └── hotel-card/
        │       └── hotel-card.component.ts
        │
        ├── organisms/                  ── Secciones completas reutilizables
        │   ├── navbar/
        │   │   └── navbar.component.ts         (signal() para mobile menu)
        │   ├── footer/
        │   │   └── footer.component.ts
        │   ├── hero-section/
        │   │   └── hero-section.component.ts   (genérico, acepta ng-content)
        │   ├── cta-banner/
        │   │   └── cta-banner.component.ts     (reutilizado en 4 páginas)
        │   ├── speakers-grid/
        │   │   └── speakers-grid.component.ts  (grid + featured speaker)
        │   └── registration-form/
        │       └── registration-form.component.ts (ReactiveFormsModule)
        │
        └── templates/
            └── main-layout/
                └── main-layout.component.ts    ← navbar + router-outlet + footer
```

---

## 📦 Páginas

| Ruta           | Componente              | Descripción                         |
|----------------|-------------------------|-------------------------------------|
| `/inicio`      | `InicioComponent`       | Hero + ejes temáticos + stats + CTA |
| `/programa`    | `ProgramaComponent`     | Agenda con signal() para tabs días  |
| `/ponentes`    | `PonentesComponent`     | Grid de ponentes + destacado        |
| `/ubicacion`   | `UbicacionComponent`    | Mapa + transporte + hoteles         |
| `/registro`    | `RegistroComponent`     | Hero + formulario reactivo          |
| `/emergencia`  | `EmergenciaComponent`   | Bento grid + FAB móvil              |

---

## 🚀 Setup

```bash
# 1. Instalar dependencias
npm install

# 2. Configurar Tailwind v4 en angular.json / vite.config.ts
# (Tailwind v4 usa plugin de Vite: @tailwindcss/vite)

# 3. Ejecutar en desarrollo
ng serve
```

### Tailwind v4 con Angular (vite.config.ts)
```ts
import { defineConfig } from 'vite';
import tailwindcss from '@tailwindcss/vite';

export default defineConfig({
  plugins: [tailwindcss()],
});
```

### En `styles.css` (ya incluido):
```css
@import "tailwindcss";
```

---

## 🎨 Design System — "The Modern Registry"

| Token          | Valor       | Uso                                     |
|----------------|-------------|-----------------------------------------|
| `brand-navy`   | `#09172d`   | Fondos primarios, nav dark              |
| `brand-gold`   | `#c0a271`   | Acento único, estados activos           |
| `surface`      | `#fbf8fb`   | Fondo base (galería limpia)             |
| `font-headline`| Noto Serif  | Títulos, headers                        |
| `font-body`    | Work Sans   | Cuerpo, navegación                      |

### Reglas del sistema:
- ✅ **Pillar accent**: única línea vertical permitida (4px, gold izquierda)
- ✅ **Glassmorphism**: nav con `backdrop-blur` + fondo semi-transparente  
- ✅ **Sin bordes 1px** para separar secciones (solo color shift)
- ✅ **Sombras ambient**: blur 24px, opacidad 6%, color tintado

---

## 📐 Convenciones Angular 21

- Todo **standalone** (sin NgModules)
- **`signal()`** para estado local reactivo
- **Lazy loading** con `loadComponent()` en rutas
- **`@for` y `@if`** (nueva sintaxis de control flow)
- **`withViewTransitions()`** para transiciones de página nativas
- Tipado estricto con interfaces de datos en cada componente
