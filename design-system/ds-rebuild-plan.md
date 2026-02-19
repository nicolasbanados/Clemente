# Plan de Reconstrucción del Design System de LunarCrush en Figma

**Autor:** Equipo de Diseño de Producto, LunarCrush  
**Fecha:** 19 de febrero de 2026  
**Versión:** 1.0  

---

## 1. Resumen Ejecutivo

Este documento presenta un plan de trabajo exhaustivo para la reconstrucción completa del design system de LunarCrush.com en Figma. El plan se basa en el análisis de 14 screenshots de alta fidelidad que cubren todas las áreas clave de la plataforma (Home, Topic Pages, Account, AI Chat, Integrations y Content Feeds), así como en un informe de auditoría previo que identificó tokens, componentes e inconsistencias.

La reconstrucción se organiza en **cinco fases secuenciales** que siguen el principio de atomicidad: desde los tokens primitivos hasta los patrones de página completos. El tiempo total estimado es de **16 a 23 días laborables** para un diseñador trabajando a tiempo completo. El resultado final será una librería de Figma publicada que funcione como la única fuente de verdad del producto.

| Fase | Nombre | Estimación | Dependencia |
| :---: | :--- | :---: | :--- |
| 1 | Fundamentos (Tokens y Primitivos) | 2-3 días | Ninguna |
| 2 | Componentes Atómicos | 3-4 días | Fase 1 |
| 3 | Componentes Modulares (Moléculas) | 5-7 días | Fase 2 |
| 4 | Organismos y Patrones de Página | 4-6 días | Fase 3 |
| 5 | Documentación, QA y Publicación | 2-3 días | Fase 4 |
| | **Total** | **16-23 días** | |

---

## 2. Filosofía y Principios Rectores

La estrategia se centra en la **velocidad de ejecución y la iteración progresiva**. En lugar de buscar la perfección en una única fase, el plan está diseñado para construir una base funcional lo más rápido posible, permitiendo que el sistema se utilice y se valide en etapas tempranas.

> **Objetivo Principal:** Reemplazar el sistema de diseño actual con una nueva librería en Figma que sea la única fuente de verdad (Single Source of Truth) para todos los elementos de la interfaz de LunarCrush, eliminando inconsistencias y acelerando el flujo de trabajo de diseño.

Los principios que guían la construcción son los siguientes:

**Atomicidad.** Cada componente se construye a partir de elementos más pequeños ya definidos. Nada se diseña "en el aire"; todo hereda de los tokens y componentes de las fases anteriores.

**Consistencia sobre originalidad.** El objetivo no es rediseñar la plataforma, sino sistematizar lo que ya existe. Los componentes deben reflejar fielmente la interfaz actual, corrigiendo únicamente las inconsistencias documentadas en el audit report.

**Auto Layout nativo.** Todos los componentes deben construirse con Auto Layout de Figma para garantizar que se adapten a diferentes contenidos y tamaños de pantalla sin necesidad de ajustes manuales.

**Variables de Figma.** Se utilizarán las Figma Variables (no solo estilos) para los tokens de color, espaciado y tipografía, permitiendo la futura implementación de temas (por ejemplo, un posible modo claro) y la exportación directa a código.

**Nomenclatura estandarizada.** Todos los componentes seguirán una convención de nombres clara y jerárquica, por ejemplo: `Navigation / Sidebar / Item / Active`.

---

## 3. Inventario Completo de Componentes Detectados

A partir del análisis de los 14 screenshots, se ha identificado el siguiente inventario exhaustivo de componentes. Este inventario es la base sobre la cual se estructura el plan de construcción.

### 3.1 Navegación

| ID | Componente | Descripción | Pantallas donde aparece |
| :---: | :--- | :--- | :--- |
| N-01 | **Sidebar Navigation** | Barra vertical izquierda con logo, iconos de sección (Discover, Integrations, AI Agents, Collections, Developers), notificaciones y avatar de usuario. | Todas |
| N-02 | **Top Header Nav** | Barra horizontal superior con categorías en formato pill (Crypto, Stocks, Prediction Markets, Finance, Technology, NBA, NHL, UFC, PGA, More), toggle de tema y búsqueda. | Home, Topic Pages |
| N-03 | **Sub-nav Tabs** | Pestañas horizontales debajo del título de página (Summary, Coins, Metrics, Creators, Alerts, Feeds). | Home, Topic Pages |
| N-04 | **Page Header** | Encabezado de página con icono de asset, nombre, ticker, menú contextual (tres puntos) y precio destacado. | Topic Pages (Bitcoin, Ethereum) |

### 3.2 Datos y Tablas

| ID | Componente | Descripción | Pantallas donde aparece |
| :---: | :--- | :--- | :--- |
| D-01 | **Data Table — Coins** | Tabla con columnas: ranking, icono, nombre, ticker, sparkline, precio, cambios porcentuales (1h, 24h, 7d), market cap. Headers ordenables. | Home/Coins |
| D-02 | **Data Table — Creators** | Tabla con columnas: avatar, nombre, handle, network badges, CreatorRank, engagements, mentions. | Home/Creators |
| D-03 | **Data Table — Prediction Markets** | Tabla con columnas: nombre, estado (icono color), precios, volumen total, volumen 24h, normal, fecha de expiración. | Home/Summary, Topic/Summary |
| D-04 | **Data Table — Seats** | Tabla de gestión de usuarios con columnas: Email, Tokens, API, Collections, Agents, Action. | Account |
| D-05 | **Recently Added Coins** | Mini-tabla con nombre, categoría y precio de monedas recién añadidas. | Home/Summary |
| D-06 | **Table Pagination** | Controles de paginación con flechas, número de página actual y rango total (e.g., "1-100 of 5,000"). | Home/Coins, Home/Creators |

### 3.3 Cards y Contenedores

| ID | Componente | Descripción | Pantallas donde aparece |
| :---: | :--- | :--- | :--- |
| C-01 | **Metric Card** | Card compacta con título de métrica, valor numérico grande, indicador de cambio (color-coded) y sparkline. Variantes: Price, AltRank, Galaxy Score, Engagements, Mentions, Market Cap, Market Dominance, Trading Volume, Circulating Supply. | Home/Summary, Topic/Summary |
| C-02 | **Mindshare Card** | Card con porcentaje de mindshare, título, descripción y color de acento (verde, púrpura, naranja). Aparece en grupos de 3 dentro de la sección "What's Up". | Home/Summary, Topic/Summary |
| C-03 | **News Card** | Card con imagen de portada, título de noticia, fuente (nombre + avatar), icono de red social y timestamp. | Home/Summary, Topic/Summary, Feeds |
| C-04 | **Post Card** | Card con contenido de post social (imagen o texto), autor (avatar + nombre + handle), métricas de engagement y timestamp. | Home/Summary, Topic/Summary, Feeds |
| C-05 | **Alert Card** | Card horizontal con icono de asset, nombre + ticker, descripción de la alerta, timestamp y sparkline mini a la derecha. | Home/Alerts, Topic/Alerts |
| C-06 | **Sector Card** | Card grande para carrusel con logo de sector, nombre y porcentaje de cambio. | Home/Summary |
| C-07 | **Creator Card** | Card de carrusel con avatar circular, nombre, handle, badges de red social y métricas resumidas. | Home/Summary, Topic/Summary |
| C-08 | **Usage Card** | Card de cuenta con título, valor actual / límite, progress bar y botón de acción (Manage, Add Tokens, API Usage). | Account |
| C-09 | **Subscription Card** | Card con nombre del plan (Enterprise), sponsor, y badge de estado (Active). | Account |
| C-10 | **Connector Card** | Card con logo de servicio (Claude), título y descripción de la integración. | Integrations |
| C-11 | **Summary Stats Card** | Card con periodo de tiempo (1 Day, 1 Week, etc.), valor de cambio y porcentaje. Aparece en fila horizontal. | Home/Metrics, Topic/Metrics |
| C-12 | **Stats Card (estática)** | Card con label descriptivo y valor grande (Average Price, 1-Year Price High, 1-Year Price Low). | Topic/Metrics |

### 3.4 Gráficos y Visualizaciones

| ID | Componente | Descripción | Pantallas donde aparece |
| :---: | :--- | :--- | :--- |
| V-01 | **Line Chart (grande)** | Gráfico de líneas con eje X temporal, tooltip con valor, línea vertical de referencia "24H" y área sombreada. | Home/Metrics, Topic/Metrics |
| V-02 | **Sparkline (mini)** | Gráfico de líneas miniatura embebido en tablas y cards. Variantes: línea (verde/rojo), área, barras. | Data Tables, Metric Cards, Alert Cards |
| V-03 | **Word Cloud** | Nube de palabras con tamaños y colores variables representando trending topics. | Home/Summary, Topic/Summary |
| V-04 | **Social Breakdown Bar** | Barra horizontal apilada mostrando distribución por red social (X 68%, TikTok 9%, YouTube 18%, etc.) con iconos. | Home/Metrics |
| V-05 | **Chart Metric Toggles** | Grupo de pills/botones para seleccionar la métrica del gráfico (Price, Engagements, Mentions, Creators, More). | Home/Metrics, Topic/Metrics |
| V-06 | **Time Range Selector** | Grupo de pills para seleccionar el rango temporal (1D, 1W, 1M, 3M, 6M, 1Y, ALL) con botones de alerta y expansión. | Home/Metrics, Topic/Metrics |

### 3.5 Inputs y Controles

| ID | Componente | Descripción | Pantallas donde aparece |
| :---: | :--- | :--- | :--- |
| I-01 | **"Ask anything" Bar** | Barra de búsqueda/prompt persistente con placeholder "Ask anything" y botón "HISTORY". Variantes: flotante (sticky) y contextual (intercalada en contenido). | Todas |
| I-02 | **Read-only Input** | Campo de texto de solo lectura con iconos de acción (settings, copy). Para API keys y URLs. | Integrations |
| I-03 | **Standard Form Input** | Campo de texto editable para formularios (email, contraseñas, etc.). | Account (implícito) |

### 3.6 Feedback y Estado

| ID | Componente | Descripción | Pantallas donde aparece |
| :---: | :--- | :--- | :--- |
| F-01 | **Status Badge** | Etiqueta pequeña indicando estado. Variantes: "Active" (verde), "Enterprise" (verde), cambio positivo/negativo. | Account, Data Tables |
| F-02 | **Change Indicator** | Texto con flecha y color indicando cambio positivo (verde, ↑) o negativo (rojo, ↓) con valor absoluto y porcentaje. | Metric Cards, Data Tables, Hero Metrics |
| F-03 | **Progress Bar** | Barra horizontal fina indicando uso relativo (e.g., 2/1K). | Usage Cards |
| F-04 | **Notification Badge** | Punto rojo sobre icono indicando notificaciones pendientes. | Sidebar |
| F-05 | **Thinking Spinner** | Indicador de carga con texto "Thinking..." para respuestas del AI. | AI Chat |

### 3.7 AI Chat

| ID | Componente | Descripción | Pantallas donde aparece |
| :---: | :--- | :--- | :--- |
| A-01 | **User Chat Bubble** | Burbuja de mensaje del usuario con fondo gradiente púrpura, avatar y texto. | AI Chat |
| A-02 | **System Chat Bubble** | Contenedor de respuesta del sistema con pasos de razonamiento, tool calls y contenido renderizado (headings, tablas, blockquotes, links). | AI Chat |
| A-03 | **Tool Call Indicator** | Elemento inline mostrando icono, nombre de herramienta y parámetros (e.g., "Topic: avax, interval: 1w"). | AI Chat |
| A-04 | **Rendered Content Block** | Bloque de contenido HTML/Markdown renderizado dentro del chat, incluyendo tablas, listas, headings y links. | AI Chat |

### 3.8 Layout y Estructura

| ID | Componente | Descripción | Pantallas donde aparece |
| :---: | :--- | :--- | :--- |
| L-01 | **Horizontal Carousel** | Contenedor con scroll horizontal para cards (Top Creators, Top News, Top Sectors, Top Posts). | Home/Summary, Topic/Summary |
| L-02 | **Section Header** | Título de sección con link "View More →" o flecha de navegación. | Múltiples secciones |
| L-03 | **Two-Column Feed Layout** | Layout de dos columnas para el feed de contenido (News y Posts). | Feeds |
| L-04 | **"What's Up" Section** | Sección con texto resumen generado por AI y 3 Mindshare Cards. | Home/Summary, Topic/Summary |
| L-05 | **Hero Metric** | Valor numérico destacado (precio, engagements) con label, cambio absoluto y porcentaje. | Topic/Summary, Home/Metrics, Topic/Metrics |

### 3.9 Elementos Misceláneos

| ID | Componente | Descripción | Pantallas donde aparece |
| :---: | :--- | :--- | :--- |
| M-01 | **Social Profile Row** | Fila con icono de red social, nombre de plataforma, handle del usuario y botón de eliminar (trash). | Account |
| M-02 | **Settings Row** | Fila con label descriptivo, valor actual (opcional) y flecha de navegación (→). | Account |
| M-03 | **Avatar** | Imagen circular. Tamaños: pequeño (24px), mediano (32-40px), grande (48-64px). Variantes: usuario, moneda/asset. | Múltiples |
| M-04 | **Coin Icon** | Icono circular con logo de criptomoneda. | Data Tables, Cards, Page Headers |
| M-05 | **Network Icon Badge** | Icono pequeño de red social (X/Twitter, TikTok, YouTube, Reddit) usado como badge. | Creator Tables, Post Cards |
| M-06 | **Dark/Light Toggle** | Toggle de tema en la barra superior. | Top Header Nav |
| M-07 | **Search Icon Button** | Botón de icono de lupa para búsqueda global. | Top Header Nav |
| M-08 | **Favorite Star Button** | Botón de estrella para marcar favoritos. | Top Header Nav |
| M-09 | **More Menu (⋮)** | Botón de menú contextual con tres puntos verticales. | Page Headers |
| M-10 | **Link with Arrow (→)** | Texto con flecha indicando navegación (e.g., "Connect a Profile →", "View More →"). | Account, Section Headers |
| M-11 | **Ghost Button** | Botón con borde y sin relleno (e.g., "Logout", "Manage", "Add Tokens"). | Account, Usage Cards |
| M-12 | **Primary Button** | Botón con relleno sólido (púrpura o acento). | Formularios, CTAs |
| M-13 | **Text Button / Link** | Texto clickeable sin borde ni fondo (e.g., "View purchase history", "View invoices"). | Account |

---

## 4. Especificación Detallada de Tokens

### 4.1 Paleta de Colores

La paleta se organiza en dos niveles: **primitivos** (valores crudos) y **semánticos** (roles funcionales que referencian primitivos).

**Colores Primitivos (Variables de Figma — Colección "Color Primitives")**

| Token | Hex | Uso Principal |
| :--- | :--- | :--- |
| `gray/950` | `#0D1117` | Fondo principal de la aplicación |
| `gray/900` (Midnight Ledger) | `#101C2D` | Fondo de cards y superficies elevadas |
| `gray/800` | `#161B22` | Fondo de inputs, bordes sutiles |
| `gray/700` | `#1C2128` | Superficie alternativa, hover de filas |
| `gray/500` | `#8B949E` | Texto secundario, metadata |
| `gray/400` | `#B2B2B2` | Texto de cuerpo, labels |
| `gray/50` | `#FFFFFF` | Texto de headings, valores destacados |
| `purple/500` | `#6E3CF5` | Color primario de marca |
| `purple/400` | `#8A2BE2` | Variante de acento, hover |
| `green/500` | `#27C869` | Cambio positivo, estado activo |
| `red/500` | `#E93953` | Cambio negativo, alertas, errores |
| `orange/500` | `#F0A030` | Acento terciario (mindshare cards, alertas) |
| `cyan/500` | `#2D9CDB` | Acento para links y datos en chat |

**Gradientes (Colección "Color Primitives")**

| Token | Definición | Uso Principal |
| :--- | :--- | :--- |
| `Cosmic Gradient` | Lineal de `#6E3CF5` a `#2D9CDB` | CTAs primarios, burbujas de chat del usuario |
| `Nebula Gradient` | Lineal de `#0F1A2A` a `#1F2A3A` | Fondos de paneles y cards especiales |

**Colores Semánticos (Variables de Figma — Colección "Semantic Colors")**

| Token Semántico | Referencia Primitiva | Uso |
| :--- | :--- | :--- |
| `bg/primary` | `gray/950` | Fondo principal |
| `bg/surface` | `gray/900` | Fondo de cards |
| `bg/surface-alt` | `gray/800` | Fondo de inputs, filas alternadas |
| `bg/elevated` | `gray/700` | Hover, tooltips |
| `text/primary` | `gray/50` | Headings, valores |
| `text/secondary` | `gray/400` | Cuerpo de texto |
| `text/tertiary` | `gray/500` | Metadata, timestamps |
| `accent/primary` | `purple/500` | Botones, estados activos, links |
| `accent/primary-hover` | `purple/400` | Hover de elementos primarios |
| `feedback/positive` | `green/500` | Cambios positivos, badges activos |
| `feedback/negative` | `red/500` | Cambios negativos, errores |
| `feedback/warning` | `orange/500` | Alertas, mindshare cards |
| `feedback/info` | `cyan/500` | Links informativos, datos en chat |

### 4.2 Tipografía

La escala tipográfica se basa en dos familias: **FAKT-TT** como fuente principal de interfaz y **Roboto Mono** para datos numéricos y código.

| Token | Familia | Peso | Tamaño | Altura de Línea | Uso |
| :--- | :--- | :--- | :---: | :---: | :--- |
| `display/lg` | FAKT-TT | Semi Bold | 48px | 56px | Precios hero (e.g., $66,884.42) |
| `display/md` | FAKT-TT | Semi Bold | 36px | 44px | Valores de métricas hero (e.g., 558.58M) |
| `heading/lg` | FAKT-TT | Semi Bold | 24px | 32px | Títulos de página (e.g., "Cryptocurrencies") |
| `heading/md` | FAKT-TT | Medium | 20px | 28px | Títulos de sección (e.g., "Leading Coins") |
| `heading/sm` | FAKT-TT | Medium | 16px | 24px | Subtítulos, nombres de cards |
| `body/lg` | FAKT-TT | Normal | 16px | 24px | Texto de cuerpo principal, descripciones |
| `body/md` | FAKT-TT | Normal | 14px | 20px | Texto de cuerpo estándar, filas de tabla |
| `body/sm` | FAKT-TT | Normal | 12px | 16px | Metadata, timestamps, labels de cards |
| `caption` | FAKT-TT | Normal | 11px | 14px | Notas al pie, textos auxiliares |
| `label/md` | FAKT-TT | Medium | 14px | 20px | Labels de botones, tabs, badges |
| `label/sm` | FAKT-TT | Medium | 12px | 16px | Labels pequeños, pills |
| `data/lg` | Roboto Mono | Medium | 24px | 32px | Valores numéricos grandes en cards |
| `data/md` | Roboto Mono | Normal | 14px | 20px | Valores en tablas, precios |
| `data/sm` | Roboto Mono | Normal | 12px | 16px | Cambios porcentuales, valores secundarios |
| `code` | Roboto Mono | Normal | 13px | 18px | Bloques de código, API keys |

### 4.3 Espaciado

La escala de espaciado se basa en múltiplos de 4px para mantener un ritmo visual consistente.

| Token | Valor | Uso Típico |
| :--- | :---: | :--- |
| `space/2` | 2px | Separación mínima entre elementos inline |
| `space/4` | 4px | Padding interno de badges, gap entre iconos y texto |
| `space/8` | 8px | Gap entre elementos en una fila, padding de pills |
| `space/12` | 12px | Padding interno de inputs, gap entre cards |
| `space/16` | 16px | Padding interno de cards, margen entre secciones menores |
| `space/20` | 20px | Margen vertical entre subsecciones |
| `space/24` | 24px | Gutter del grid, margen entre secciones |
| `space/32` | 32px | Margen entre secciones principales |
| `space/48` | 48px | Margen entre bloques de página |
| `space/64` | 64px | Ancho de la sidebar colapsada |

### 4.4 Bordes y Radios

| Token | Valor | Uso |
| :--- | :--- | :--- |
| `radius/sm` | 4px | Badges, elementos pequeños |
| `radius/md` | 8px | Cards, inputs, botones |
| `radius/lg` | 12px | Cards grandes, modales |
| `radius/pill` | 999px | Pills de navegación, tags de categoría |
| `radius/circle` | 50% | Avatares, iconos de moneda |
| `border/default` | 1px solid `gray/700` | Bordes de cards y separadores |
| `border/subtle` | 1px solid `gray/800` | Bordes de inputs, divisores de tabla |

---

## 5. Plan de Ejecución por Fases

### Fase 1: Fundamentos (Tokens y Primitivos)

**Objetivo:** Definir y documentar en Figma todas las variables de diseño fundamentales. Esta es la base sobre la cual se construirá absolutamente todo.

**Dependencias:** Ninguna. Es el punto de partida.

**Estimación:** 2-3 días.

**Entregables detallados:**

La primera tarea consiste en crear el archivo de Figma con la estructura de páginas correcta. Se recomienda una página por cada nivel del sistema: "Cover", "Tokens", "Atoms", "Molecules", "Organisms", "Patterns" y "Documentation". Dentro de la página "Tokens", se deben crear las siguientes colecciones de variables:

En **colores**, se crearán dos colecciones de Figma Variables: "Color Primitives" con todos los valores hex listados en la sección 4.1 (incluyendo los gradientes Cosmic y Nebula), y "Semantic Colors" con los tokens semánticos que referencian a los primitivos. Adicionalmente, se crearán los estilos de color de Figma correspondientes para compatibilidad con versiones anteriores del flujo de trabajo.

En **tipografía**, se crearán todos los estilos de texto listados en la sección 4.2. Cada estilo debe estar completamente definido con familia, peso, tamaño, altura de línea y letter-spacing. Se recomienda crear un frame de referencia visual con todos los estilos aplicados a texto de ejemplo.

En **espaciado**, se creará una colección de variables numéricas con todos los valores de la sección 4.3. Se construirá un componente `Spacer` con variantes para cada valor, útil para insertar espaciado en frames con Auto Layout.

En **bordes y efectos**, se crearán los estilos de efecto de Figma para sombras y los estilos de grid para los layouts de página. Los radios de esquina se documentarán como variables numéricas.

En **iconografía**, se realizará la auditoría de todos los iconos visibles en los screenshots. El set mínimo incluye: LunarCrush logo, Discover, Integrations, AI Agents, Collections, Developers, Search, Notifications, Settings, Trash, Copy, Chevron (up/down/right), Arrow right, Star (favorite), More (three dots), Close, Plus, External link, y los iconos de redes sociales (X/Twitter, TikTok, YouTube, Reddit). Todos se construirán como componentes de Figma a 24x24px con 1.5px de stroke weight, siguiendo las recomendaciones del audit report para unificar el estilo.

**Criterio de completitud:** La fase se considera terminada cuando cualquier componente posterior puede construirse utilizando exclusivamente los tokens y primitivos definidos, sin necesidad de valores hardcodeados.

### Fase 2: Componentes Atómicos

**Objetivo:** Construir los componentes más básicos e indivisibles de la interfaz. Estos son los bloques de construcción para todo lo demás.

**Dependencias:** Fase 1 completada en su totalidad.

**Estimación:** 3-4 días.

**Entregables detallados:**

| Componente | Variantes | Estados | Propiedades Expuestas |
| :--- | :--- | :--- | :--- |
| **Button** | `Primary`, `Secondary` (outlined), `Ghost`, `Destructive`, `Icon-only` | `Default`, `Hover`, `Pressed`, `Disabled` | `Label` (texto), `Left Icon` (boolean), `Right Icon` (boolean), `Size` (sm/md/lg) |
| **Input** | `Default`, `With Left Icon`, `With Right Icon`, `With Both Icons` | `Default`, `Hover`, `Focused`, `Error`, `Disabled`, `Read-only` | `Placeholder`, `Value`, `Label` (boolean), `Helper Text` (boolean) |
| **Badge** | `Status` (Active, Enterprise), `Notification` (dot), `Network` (X, TikTok, YouTube, Reddit), `Change` (positive/negative) | `Default` | `Label`, `Color` (semantic) |
| **Avatar** | `User`, `Coin`, `Placeholder` | `Default` | `Size` (sm/md/lg/xl), `Image` (instance swap), `Badge` (boolean) |
| **Tag / Pill** | `Category` (Crypto, Stocks, etc.), `Metric Toggle` (Price, Engagements), `Time Range` (1D, 1W, etc.) | `Active`, `Inactive`, `Hover` | `Label` |
| **Toggle** | `Theme Toggle`, `Form Switch` | `On`, `Off` | — |
| **Progress Bar** | `Linear`, `Thin` | `Default` | `Progress` (0-100%), `Color` (semantic) |
| **Divider** | `Horizontal`, `Vertical` | — | `Color`, `Thickness` |
| **Change Indicator** | `Positive`, `Negative`, `Neutral` | — | `Value`, `Percentage`, `Show Arrow` (boolean) |
| **Sparkline** | `Line` (green), `Line` (red), `Area`, `Bar` | — | `Data` (visual placeholder), `Color` |
| **Link** | `Default`, `With Arrow`, `External` | `Default`, `Hover` | `Label`, `Icon` (boolean) |

Cada componente debe construirse con Auto Layout, utilizar exclusivamente los tokens de la Fase 1, y documentarse con una descripción breve en el panel de componentes de Figma.

### Fase 3: Componentes Modulares (Moléculas)

**Objetivo:** Combinar los componentes atómicos para crear elementos de interfaz más complejos y reutilizables que aparecen en múltiples contextos de la plataforma.

**Dependencias:** Fase 2 completada.

**Estimación:** 5-7 días.

**Entregables detallados:**

**Metric Card (C-01).** Componente compuesto por: título (`body/sm`), valor numérico (`data/lg`), Change Indicator y Sparkline. Se necesitan variantes para cada métrica visible: Price, AltRank, Galaxy Score, Engagements, Mentions, Market Cap, Market Dominance, Trading Volume, Circulating Supply. Todas las variantes comparten la misma estructura pero difieren en el contenido de ejemplo.

**Mindshare Card (C-02).** Componente con: porcentaje destacado, título, texto descriptivo y color de acento configurable. Se necesitan tres variantes de color (verde, púrpura, naranja) correspondientes a los tres tipos de mindshare observados en las secciones "What's Up".

**Content Cards (C-03, C-04).** Se construirá un componente base `ContentCard` con Auto Layout vertical que incluya: slot de media (imagen), slot de header (fuente/autor), slot de body (título/texto) y slot de footer (métricas). A partir de este base, se crearán las variantes `NewsCard` y `PostCard` mediante instance swapping y propiedades booleanas para mostrar/ocultar elementos.

**Alert Card (C-05).** Componente horizontal con: Avatar (coin icon), textos (nombre + ticker, descripción), timestamp y Sparkline alineada a la derecha.

**Sector Card (C-06).** Card grande para carrusel con logo de sector centrado, nombre y porcentaje de cambio. Fondo con gradiente sutil.

**Creator Card (C-07).** Card de carrusel con Avatar (grande), nombre, handle, Network Badges y métricas resumidas.

**Usage Card (C-08).** Card con título, valor actual / límite (`data/lg`), Progress Bar y Button (Ghost). Variantes para: Daily Tokens, API Rate Limit, Collections, Agents, Seats.

**Subscription Card (C-09).** Card con nombre del plan, texto de sponsor y Status Badge.

**Connector Card (C-10).** Card con imagen/logo, título y descripción.

**Summary Stats Card (C-11).** Card con label de periodo, valor de cambio y porcentaje. Diseñada para aparecer en fila horizontal de 5.

**Stats Card (C-12).** Card estática con label descriptivo y valor grande.

**Navigation Items.** Tres componentes: `SidebarItem` (icono + label, estados Active/Inactive/Hover), `TopNavPill` (texto, estados Active/Inactive), `SubNavTab` (texto con underline, estados Active/Inactive).

**Table Row Items.** Componentes de fila para cada tipo de tabla: `CoinRow` (con todas las celdas de D-01), `CreatorRow` (con todas las celdas de D-02), `PredictionMarketRow` (D-03), `SeatRow` (D-04), `RecentCoinRow` (D-05). Cada fila debe construirse con Auto Layout horizontal y celdas de ancho fijo o proporcional.

**Chat Components.** `UserBubble` (fondo Cosmic Gradient, avatar, texto), `SystemBubble` (fondo surface, con slots para thinking state, tool calls y rendered content), `ToolCallIndicator` (icono + nombre + params en formato inline).

**"Ask anything" Bar (I-01).** Componente de input especial con placeholder "Ask anything", botón "HISTORY" y variantes: `floating` (con sombra, posición sticky) y `inline` (integrada en el contenido).

**Social Profile Row (M-01).** Fila con Network Icon Badge, nombre de plataforma, handle y botón de eliminar.

**Settings Row (M-02).** Fila con label, valor opcional y Link with Arrow.

### Fase 4: Organismos y Patrones de Página

**Objetivo:** Ensamblar los componentes modulares en secciones completas de la interfaz y crear las plantillas de página que representan cada vista de la plataforma.

**Dependencias:** Fase 3 completada.

**Estimación:** 4-6 días.

**Entregables detallados:**

**Organismos de navegación.** Se ensamblarán tres organismos principales: la `Sidebar` completa (logo + SidebarItems + notificaciones + avatar), el `TopHeader` completo (star + TopNavPills + toggle + search) y el `PageHeader` (coin icon + título + ticker + more menu + SubNavTabs).

**Data Tables completas.** Se construirán las tablas completas para cada contexto: `CoinsTable` (header sortable + CoinRows + Pagination), `CreatorsTable` (header + CreatorRows + Pagination), `PredictionMarketsTable` (header + PredictionMarketRows), `SeatsTable` (header + SeatRows + Add User button). Cada tabla debe usar Auto Layout vertical y permitir agregar o quitar filas fácilmente.

**Chart Section.** Se creará el organismo completo de gráficos que incluye: Hero Metric (valor grande + change indicator), Line Chart (placeholder visual con ejes y tooltip), Chart Metric Toggles (fila de pills) y Time Range Selector (fila de pills + botones). Este organismo se reutiliza tanto en Home/Metrics como en Topic/Metrics.

**Horizontal Carousels.** Se creará un componente `Carousel` genérico que acepte cualquier tipo de card como contenido. Se instanciarán variantes específicas para: Top Creators (CreatorCards), Top News (NewsCards), Top Posts (PostCards) y Top Sectors (SectorCards).

**"What's Up" Section.** Organismo que combina un bloque de texto generado por AI con una fila de 3 Mindshare Cards.

**Global Metrics Grid.** Grid de Metric Cards organizado en filas, tal como aparece en las páginas de Summary.

**Alerts List.** Lista vertical de Alert Cards.

**Feeds Layout.** Layout de dos columnas con Content Cards (News y Posts) intercaladas con barras "Ask anything".

**Trending Topics Section.** Contenedor con Section Header y Word Cloud.

**Plantillas de página completas.** Se crearán las siguientes plantillas ensamblando los organismos anteriores:

La plantilla **Home / Topic Summary** incluye: TopHeader, PageHeader con SubNavTabs, What's Up Section, Global Metrics Grid, Alerts (preview), Prediction Markets Table (preview), Top Creators Carousel, Trending Topics, Top News Carousel, Top Posts Carousel y Ask anything Bar (floating).

La plantilla **Home / Topic Coins** incluye: TopHeader, PageHeader, filtros de tabla, CoinsTable completa con paginación y Ask anything Bar (floating).

La plantilla **Home / Topic Metrics** incluye: TopHeader, PageHeader, Hero Metric, Chart Section completa, Summary Stats Cards (fila de 5), Stats Cards (fila de 3), Social Breakdown Bar, News Carousel y Posts Carousel.

La plantilla **Home / Topic Creators** incluye: TopHeader, PageHeader, CreatorsTable completa con paginación.

La plantilla **Home / Topic Alerts** incluye: TopHeader, PageHeader, Alerts List completa.

La plantilla **Home / Topic Feeds** incluye: TopHeader, PageHeader, Feeds Layout de dos columnas.

La plantilla **Account** incluye: Sidebar, perfil de usuario, Subscription Card, Usage Cards (Daily Tokens, API, Collections, Agents, Seats), Social Profile Rows, Settings Rows, Support links y botón Logout.

La plantilla **AI Chat** incluye: Sidebar, área de chat con UserBubbles y SystemBubbles, y Ask anything Bar (bottom).

La plantilla **Integrations** incluye: Sidebar, título y descripción, Read-only Inputs (API Key, MCP Server Link) y Connector Cards.

### Fase 5: Documentación, QA y Publicación

**Objetivo:** Finalizar la librería, realizar control de calidad, documentar el uso de cada componente y publicar para el equipo.

**Dependencias:** Fase 4 completada.

**Estimación:** 2-3 días.

**Entregables detallados:**

**Control de calidad.** Se revisará cada componente para verificar que utiliza exclusivamente tokens definidos (sin valores hardcodeados), que el Auto Layout funciona correctamente al cambiar contenido, que las variantes y propiedades están correctamente configuradas, y que la nomenclatura sigue la convención establecida.

**Página de documentación en Figma.** Se creará una página "Documentation" dentro del archivo con frames organizados que muestren: la paleta de colores completa con nombres de tokens, la escala tipográfica con ejemplos, la escala de espaciado visualizada, todos los iconos con sus nombres, y cada componente con sus variantes, estados y guías de uso (Do's y Don'ts).

**Kit de UI.** Se creará una página "UI Kit" con todos los componentes organizados visualmente para referencia rápida, permitiendo a los diseñadores encontrar y copiar componentes fácilmente.

**Publicación de la librería.** Se publicará la librería de Figma para que esté disponible en todos los archivos de diseño del equipo. Se configurarán las descripciones de componentes y las etiquetas de búsqueda.

**Sesión de handover.** Se preparará una presentación breve para el equipo de desarrollo explicando la estructura del sistema, cómo acceder a los tokens y especificaciones, y cómo se mapean los componentes de Figma a los componentes de código.

---

## 6. Diagrama de Dependencias

El siguiente diagrama muestra la relación secuencial entre las fases y cómo los entregables de cada una alimentan a la siguiente:

```
┌─────────────────────────────────────────────────────────────────┐
│  FASE 1: Fundamentos                                           │
│  Colores → Tipografía → Espaciado → Iconos → Efectos          │
│  (2-3 días)                                                    │
└───────────────────────────┬─────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────────┐
│  FASE 2: Átomos                                                │
│  Button → Input → Badge → Avatar → Tag/Pill → Toggle →        │
│  Progress Bar → Divider → Change Indicator → Sparkline → Link  │
│  (3-4 días)                                                    │
└───────────────────────────┬─────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────────┐
│  FASE 3: Moléculas                                             │
│  Metric Card → Content Cards → Alert Card → Usage Card →      │
│  Nav Items → Table Rows → Chat Bubbles → Ask Bar →            │
│  Social Row → Settings Row                                     │
│  (5-7 días)                                                    │
└───────────────────────────┬─────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────────┐
│  FASE 4: Organismos y Patrones                                 │
│  Sidebar → TopHeader → Data Tables → Chart Section →           │
│  Carousels → Page Sections → Page Templates (×8)               │
│  (4-6 días)                                                    │
└───────────────────────────┬─────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────────┐
│  FASE 5: Documentación y Publicación                           │
│  QA → Docs → UI Kit → Publicación → Handover                  │
│  (2-3 días)                                                    │
└─────────────────────────────────────────────────────────────────┘
```

---

## 7. Inconsistencias a Corregir Durante la Construcción

El audit report identificó varias inconsistencias que deben resolverse activamente durante la construcción del nuevo sistema. Estas correcciones no son una fase separada, sino que se integran en el trabajo de cada fase correspondiente.

| Inconsistencia | Fase de Corrección | Acción Específica |
| :--- | :---: | :--- |
| Barras "Ask anything" redundantes (contextual + global) | Fase 3 | Diseñar un único componente con dos variantes claras (`floating` y `inline`) y documentar cuándo usar cada una. |
| Iconografía con stroke weights inconsistentes | Fase 1 | Unificar todos los iconos a 1.5px de stroke weight y corner rounding consistente. |
| Botón "HISTORY" con estilos variables | Fase 2 | Definir un único estilo para el botón HISTORY como variante del componente Button (`Ghost/Small`). |
| Padding inconsistente entre Mindshare Cards y Metric Cards | Fase 3 | Estandarizar el padding interno de todas las cards a `space/16` (16px). |
| Indicadores de clickabilidad ausentes en títulos | Fase 3 | Agregar un indicador visual (chevron o cambio de color) a todos los títulos y datos clickeables, documentando el patrón. |

---

## 8. Estructura de Archivos en Figma

Se recomienda la siguiente estructura de páginas dentro del archivo principal de la librería:

| Página | Contenido |
| :--- | :--- |
| **Cover** | Portada del archivo con nombre del proyecto, versión, fecha y equipo. |
| **Changelog** | Registro de cambios por versión. |
| **Tokens** | Visualización de todos los tokens: colores, tipografía, espaciado, iconos, efectos. |
| **Atoms** | Todos los componentes atómicos (Fase 2). |
| **Molecules** | Todos los componentes modulares (Fase 3). |
| **Organisms** | Todos los organismos y secciones ensambladas (Fase 4). |
| **Templates** | Plantillas de página completas (Fase 4). |
| **Documentation** | Guías de uso, Do's y Don'ts, especificaciones (Fase 5). |
| **UI Kit** | Vista rápida de todos los componentes para referencia (Fase 5). |

---

## 9. Recomendaciones para Maximizar Velocidad

**Comenzar con los componentes de mayor reutilización.** Dentro de cada fase, priorizar los componentes que se usan en más pantallas. Por ejemplo, el `Button`, el `Badge` y el `Avatar` aparecen en prácticamente todas las vistas y deben construirse primero.

**Usar Component Properties agresivamente.** En lugar de crear múltiples componentes separados, usar las propiedades de componente de Figma (text, boolean, instance swap, variant) para reducir el número de componentes manteniendo la flexibilidad.

**No perfeccionar los placeholders de gráficos.** Los gráficos (Line Chart, Word Cloud) son elementos visuales complejos que en Figma funcionan como placeholders. No invertir tiempo excesivo en hacerlos pixel-perfect; basta con que comuniquen la estructura y el espacio que ocupan.

**Validar con screenshots reales.** Al final de cada fase, comparar los componentes construidos contra los screenshots originales para detectar omisiones o desviaciones antes de avanzar a la siguiente fase.

**Iterar sobre el sistema en uso.** Una vez completada la Fase 3, el sistema ya es lo suficientemente maduro para comenzar a usarse en diseños reales. Los refinamientos de las Fases 4 y 5 pueden hacerse en paralelo con el trabajo de diseño de producto.

---

*Este plan de trabajo ha sido elaborado para el equipo de Diseño de Producto de LunarCrush. Está diseñado como un documento vivo que puede ajustarse según las necesidades y prioridades del proyecto.*
