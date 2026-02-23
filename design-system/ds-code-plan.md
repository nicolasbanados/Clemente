# Plan de Implementación: Design System de LunarCrush en Código

**Autor:** Manus AI (para el equipo de Producto de LunarCrush)
**Fecha:** 23 de febrero de 2026
**Versión:** 1.0

---

## 1. Resumen Ejecutivo

Este documento presenta un plan de trabajo detallado y accionable para la construcción del design system de LunarCrush en código, utilizando **shadcn/ui** y **Tailwind CSS**. El plan está diseñado para sincronizarse directamente con la reconstrucción del design system en Figma, detallada en `ds-rebuild-plan.md`, y aborda las inconsistencias identificadas en el `audit-report.md`.

La filosofía central es tratar el design system no como una dependencia externa, sino como **código fuente que vive dentro del proyecto**. Esto proporciona máxima flexibilidad, control y optimización a largo plazo. El plan se estructura en fases que reflejan la metodología de diseño atómico, asegurando una base sólida y escalable, desde los tokens de diseño hasta los componentes de página completos.

El objetivo es crear una base de código que sea una **extensión directa y viva de la librería de Figma**, permitiendo a los desarrolladores construir interfaces de usuario consistentes, de alta calidad y de manera eficiente. Se prioriza la creación de una capa de tokens robusta, la composición de componentes y la documentación clara para facilitar la adopción y el mantenimiento.

| Fase | Nombre | Foco Principal |
| :---: | :--- | :--- |
| 1 | Configuración y Fundamentos (Tokens) | Estructura del proyecto, configuración de Tailwind y traducción de tokens de Figma a CSS variables. |
| 2 | Componentes Primitivos y Compuestos | Integración, personalización y creación de abstracciones específicas del producto. |
| 3 | Bloques y Patrones (Organismos) | Ensamblaje de componentes en secciones reutilizables de la interfaz. |
| 4 | Resolución de Inconsistencias | Aplicación de correcciones definidas en el audit report. |
| 5 | Documentación y Mantenimiento | Documentación de componentes, guías de uso y estrategia de sincronización continua. |

---

## 2. Filosofía y Principios Rectores

La implementación del design system en código se guiará por los siguientes principios, basados en las mejores prácticas de la industria para 2026 [1].

*   **shadcn/ui como Código Fuente, no como Dependencia.** Los componentes de shadcn/ui se añadirán directamente al repositorio. Esto nos da control total sobre su API, comportamiento y actualizaciones. No se realizarán actualizaciones ciegas; cada cambio será intencional.

*   **Abstracción Específica del Producto.** Se evitará el uso directo de los componentes de `ui` en la aplicación. En su lugar, se crearán componentes intermedios (`components/primitives`) que encapsulen la lógica y estilos base, añadiendo una capa de personalización y control.

*   **Tokens de Diseño como Ùnica Fuente de Verdad.** Todos los estilos (colores, tipografía, espaciado, radios) se definirán como CSS variables en un archivo global (`globals.css`), directamente traducidos desde las Figma Variables. Los componentes consumirán estas variables, no valores estáticos. Esto asegura que cualquier cambio en un token se propague consistentemente por toda la aplicación [2].

*   **Composición de Bloques, no de Pantallas.** El enfoque de construcción se centrará en crear "bloques" de UI reutilizables y de mayor nivel (ej. `PricingCard`, `PageHeader`) en lugar de ensamblar pantallas desde cero con componentes atómicos. Esto acelera el desarrollo y garantiza la consistencia.

*   **Documentación como Requisito.** Dado que el sistema vive en el código, la documentación es obligatoria. Cada componente y bloque deberá tener una justificación clara de su propósito y uso, preferiblemente a través de herramientas como Storybook o, como mínimo, en archivos `README.md`.

---

## 3. Estructura de Archivos Recomendada

Para mantener la claridad y la escalabilidad, se propone la siguiente estructura de directorios dentro de la carpeta `src` del proyecto. Esta organización separa claramente los componentes base de shadcn/ui, nuestras abstracciones personalizadas y los bloques de UI complejos.

```
/src
├── lib/
│   └── utils.ts       # Utilidad cn() de Tailwind Merge
├── styles/
│   └── globals.css    # Archivo central de tokens (CSS Variables)
└── components/
    ├── ui/              # Componentes crudos de shadcn/ui (No modificar)
    ├── primitives/      # Abstracciones propias sobre /ui (ej. AppButton)
    └── blocks/          # Componentes de negocio compuestos (ej. MetricCard)
```

*   **`/ui`**: Contendrá los componentes tal como los instala la CLI de shadcn/ui. Actúan como nuestra librería de primitivos base. La regla es no importarlos directamente en las páginas de la aplicación.
*   **`/primitives`**: Aquí se crearán wrappers o adaptadores sobre los componentes de `/ui`. Por ejemplo, un componente `AppButton.tsx` que importa el `Button` de `/ui` y le aplica las clases de fuente, tracking y variantes específicas de LunarCrush. La aplicación consumirá `AppButton`, no `Button`.
*   **`/blocks`**: Contendrá componentes más grandes que resuelven un problema de UI específico y se componen de mùltiples primitivos. Por ejemplo, `MetricCard.tsx` estaría aquí y usaría `Card`, `h3`, `p`, y un `Sparkline` de los primitivos.

---

## 4. Fase 1: Configuración y Fundamentos (Tokens)

**Objetivo:** Traducir la base del design system de Figma (tokens) a una configuración funcional en el código con Tailwind CSS y CSS variables.

### 4.1. Configuración de `tailwind.config.js`

Se configurará Tailwind para extender el tema por defecto con nuestras definiciones de CSS variables, en lugar de sobreescribirlo. Se añadirán las familias de fuentes y se asegurará que el modo oscuro esté habilitado vía `class`.

```javascript
// tailwind.config.js
/** @type {import('tailwindcss').Config} */
module.exports = {
  darkMode: ["class"],
  content: [
    './pages/**/*.{ts,tsx}',
    './components/**/*.{ts,tsx}',
    './app/**/*.{ts,tsx}',
    './src/**/*.{ts,tsx}',
	],
  theme: {
    container: { ... },
    extend: {
      colors: {
        border: "hsl(var(--border))",
        input: "hsl(var(--input))",
        ring: "hsl(var(--ring))",
        background: "hsl(var(--background))",
        foreground: "hsl(var(--foreground))",
        primary: { DEFAULT: "hsl(var(--primary))", foreground: "hsl(var(--primary-foreground))" },
        secondary: { DEFAULT: "hsl(var(--secondary))", foreground: "hsl(var(--secondary-foreground))" },
        destructive: { DEFAULT: "hsl(var(--destructive))", foreground: "hsl(var(--destructive-foreground))" },
        positive: { DEFAULT: "hsl(var(--positive))", foreground: "hsl(var(--positive-foreground))" },
        muted: { DEFAULT: "hsl(var(--muted))", foreground: "hsl(var(--muted-foreground))" },
        accent: { DEFAULT: "hsl(var(--accent))", foreground: "hsl(var(--accent-foreground))" },
        // ... etc
      },
      borderRadius: {
        lg: "var(--radius-lg)",
        md: "var(--radius)",
        sm: "var(--radius-sm)",
      },
      fontFamily: {
        sans: ["var(--font-sans)", "sans-serif"],
        mono: ["var(--font-mono)", "monospace"],
      },
      // ... keyframes, animation
    },
  },
  plugins: [require("tailwindcss-animate")],
}
```

### 4.2. Mapeo de Tokens Figma a CSS

El archivo `src/styles/globals.css` será la ùnica fuente de verdad para todos los tokens de diseño. Se traducirán los tokens del plan de Figma (`ds-rebuild-plan.md`) a variables CSS en formato HSL, como recomienda shadcn/ui [3].

La siguiente tabla resume el mapeo directo:

| Token Figma (Primitivo) | Valor Hex | Variable CSS (`.dark`) | Valor HSL |
| :--- | :--- | :--- | :--- |
| `gray/950` | `#0D1117` | `--background` | `210 22% 7%` |
| `gray/900` | `#101C2D` | `--card` | `215 48% 12%` |
| `gray/800` | `#161B22` | `--secondary` / `--muted` | `216 19% 11%` |
| `gray/50` | `#FFFFFF` | `--foreground` | `0 0% 100%` |
| `purple/500` | `#6E3CF5` | `--primary` | `256 90% 60%` |
| `green/500` | `#27C869` | `--positive` | `145 63% 47%` |
| `red/500` | `#E93953` | `--destructive` | `350 80% 57%` |
| `radius/lg` | 12px | `--radius-lg` | `1rem` (asumiendo 12px) |
| `radius/md` | 8px | `--radius` | `0.75rem` (asumiendo 12px) |
| `radius/sm` | 4px | `--radius-sm` | `0.5rem` (asumiendo 12px) |

Se definirán también las variables para los gradientes `Cosmic Gradient` y `Nebula Gradient` para ser usados en clases de utilidad personalizadas.

### 4.3. Tipografía

Se configurarán las fuentes **FAKT-TT** y **Roboto Mono** en el layout principal de la aplicación (ej. `app/layout.tsx` en Next.js) para que estén disponibles globalmente a través de las variables `--font-sans` y `--font-mono`.

---

## 5. Fase 2: Componentes Primitivos y Compuestos

**Objetivo:** Instalar los componentes base de shadcn/ui y crear sobre ellos las abstracciones personalizadas que se alinien con el inventario de componentes de Figma.

El proceso será iterativo por cada componente del inventario (`ds-rebuild-plan.md`):

1.  **Instalar** el componente base de shadcn/ui en `/components/ui`.
2.  **Crear** un componente wrapper en `/components/primitives` o `/components/blocks`.
3.  **Personalizar** el wrapper para que coincida con los estilos y variantes de LunarCrush.

La siguiente tabla detalla la estrategia para los componentes clave:

| Componente Figma (ID) | shadcn/ui Base | Directorio Destino | Estrategia de Implementación |
| :--- | :--- | :--- | :--- |
| **Button** (M-11, M-12) | `button` | `/primitives` | Crear `AppButton` que use `FAKT-TT` por defecto. Definir variantes `primary`, `ghost`, `destructive` que mapeen a los colores CSS. |
| **Avatar** (M-03) | `avatar` | `/primitives` | Crear `AppAvatar` con las variantes de tamaño (sm, md, lg) definidas en Figma. |
| **Badge** (F-01) | `badge` | `/primitives` | Crear `AppBadge` con variantes semánticas: `positive`, `negative`, `active`, `enterprise`. |
| **Input** (I-01, I-02, I-03) | `input` | `/primitives` | Crear `AppInput` que aplique los estilos de borde y fondo de `--input`. |
| **Card** (C-01 a C-12) | `card` | `/primitives` | Crear `AppCard` que use `bg-card` y `rounded-lg` por defecto. |
| **Metric Card** (C-01) | `card`, `h3`, `p` | `/blocks` | Ensamblar `MetricCard` usando `AppCard` y primitivos de texto. Expondrá props para título, valor, indicador y sparkline. |
| **Data Table** (D-01 a D-04) | `table` | `/blocks` | Crear `DataTable` genérico que use los componentes de tabla de shadcn/ui (`Table`, `TableHeader`, `TableRow`, etc.) estilados segùn el tema. |
| **Tabs** (N-03) | `tabs` | `/primitives` | Crear `AppTabs` que personalice el indicador activo para que sea un `underline` pùrpura. |

---

## 6. Fase 3: Bloques y Patrones (Organismos)

**Objetivo:** Ensamblar los componentes de las fases anteriores en secciones de UI completas y reutilizables.

*   **Navegación (`Sidebar`, `TopHeader`, `PageHeader`):** Se construirán como componentes en `/blocks` que compongan los `Navigation Items` (primitivos) y otros elementos como el `Avatar` de usuario y el `Input` de búsqueda.
*   **Tablas de Datos Completas (`CoinsTable`, `CreatorsTable`):** Se crearán componentes en `/blocks` que usen el `DataTable` genérico y le pasen las definiciones de columnas y los datos específicos para cada contexto, incluyendo la paginación (`pagination`).
*   **Sección de Gráficos (`ChartSection`):** Este bloque en `/blocks` combinará el `Line Chart` (usando una librería como `recharts` o `visx`), los `Chart Metric Toggles` (`AppTabs`) y el `Time Range Selector` (`ToggleGroup`).

---

## 7. Fase 4: Resolución de Inconsistencias

**Objetivo:** Abordar explícitamente las inconsistencias del `audit-report.md` durante la construcción.

| Inconsistencia | Acción Específica en Código |
| :--- | :--- |
| Barras "Ask anything" redundantes | Crear un ùnico componente `AskBar` en `/blocks` con variantes `floating` y `inline` controladas por props. |
| Iconografía inconsistente | Usar una ùnica librería de iconos (ej. `lucide-react`) y definir un tamaño y `stroke-width` base en un componente `Icon` wrapper. |
| Botón "HISTORY" variable | Definir una variante específica `history` en el componente `AppButton` para unificar su estilo. |
| Padding inconsistente en Cards | El componente `AppCard` en `/primitives` tendrá un padding por defecto (`p-4` o `p-6`) que se aplicará a todas las cards. |

---

## 8. Fase 5: Documentación y Mantenimiento

**Objetivo:** Asegurar la adopción, consistencia y longevidad del design system en código.

*   **Storybook:** Se recomienda encarecidamente la implementación de **Storybook**. Permite desarrollar y documentar componentes de forma aislada. Cada componente en `/primitives` y `/blocks` debería tener su propia "historia" que muestre todas sus variantes y estados.

*   **Guías de Uso:** La documentación de cada componente debe incluir no solo sus `props`, sino también cuándo y cómo usarlo. Se pueden añadir archivos `README.md` junto a los componentes complejos para explicar su propósito.

*   **Sincronización con Figma:** El mantenimiento de la paridad entre Figma y el código es crucial. Se debe establecer un proceso claro:
    1.  Cualquier cambio en el design system **debe comenzar en Figma**.
    2.  Una vez aprobado en Figma, el cambio se traduce a las variables CSS en `globals.css` y a los componentes correspondientes.
    3.  Se debe mantener un `CHANGELOG.md` para comunicar las actualizaciones del design system al equipo de desarrollo.

---

## 9. Referencias

[1] Vaibhav Gupta, "Shadcn UI Best Practices for 2026," _Medium_, Feb 2, 2026. [https://medium.com/write-a-catalyst/shadcn-ui-best-practices-for-2026-444efd204f44](https://medium.com/write-a-catalyst/shadcn-ui-best-practices-for-2026-444efd204f44)

[2] Perpetual, "Accelerating Themeable Design Systems with shadcn/ui," _Perpetual Blog_, Jan 30, 2026. [https://www.perpetualny.com/blog/accelerating-themeable-design-systems-with-shadcn-ui-a-step-by-step-guide](https://www.perpetualny.com/blog/accelerating-themeable-design-systems-with-shadcn-ui-a-step-by-step-guide)

[3] shadcn/ui, "Theming," _shadcn/ui Docs_. [https://ui.shadcn.com/docs/theming](https://ui.shadcn.com/docs/theming)
