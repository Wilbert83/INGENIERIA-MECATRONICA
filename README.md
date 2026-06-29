# 📚 Prontuario de Ingeniería Mecatrónica — UNAM FI

[![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat-square&logo=html5&logoColor=white)](https://developer.mozilla.org/es/docs/Web/HTML)
[![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat-square&logo=css3&logoColor=white)](https://developer.mozilla.org/es/docs/Web/CSS)
[![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black)](https://developer.mozilla.org/es/docs/Web/JavaScript)
[![GitHub Pages](https://img.shields.io/badge/GitHub%20Pages-222222?style=flat-square&logo=github&logoColor=white)](https://pages.github.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green?style=flat-square)](LICENSE)
[![Estado](https://img.shields.io/badge/estado-en%20desarrollo-orange?style=flat-square)]()

> Sitio web personal de apuntes y prontuario de la **Licenciatura en Ingeniería Mecatrónica**, UNAM Facultad de Ingeniería (DIMEI), Plan de Estudios 2016. Organizado por semestre y materia — 10 semestres, 52+ asignaturas — con sistema de temas, colores de identidad por materia y TOC interactivo generado automáticamente desde exportaciones de Word.

🌐 **Demo en vivo:** <https://wilbert83.github.io/INGENIERIA-MECATRONICA/>

---

## ✨ Características

| Característica | Detalle |
|---|---|
| 📖 **Cobertura curricular** | 10 semestres × 52 materias del Plan 2016 |
| 🌗 **Tema oscuro / claro** | Persistido en `localStorage`, sin flash al navegar |
| 🎨 **16 colores de acento** | Selector en la barra de navegación + botón aleatorio 🎲 |
| 🏷️ **Color de identidad por materia** | Cada asignatura tiene su color propio, configurable por `<meta>` |
| 📑 **TOC colapsable** | Generado automáticamente desde los headings del Word exportado |
| 👁️ **Auto-highlight en scroll** | `IntersectionObserver` marca la sección visible en el índice |
| 📄 **Template de materia** | Un solo archivo HTML que procesa cualquier exportación de Word |
| ⚡ **Sin dependencias** | 100 % vanilla HTML / CSS / JS — sin frameworks, sin `npm` |
| 🚀 **GitHub Pages ready** | Archivos estáticos, sin servidor ni build step |

---

## 🗂 Estructura del repositorio

```
INGENIERIA-MECATRONICA/
│
├── index.html                    ← Índice principal (semestres y materias)
├── favicon.png                   ← Logo IM
├── README.md
├── materia-template.html         ← Plantilla reutilizable para cada materia
│
├── s1/                           ← Primer Semestre
│   ├── algebra/
│   │   ├── index.html            ← Apunte de Álgebra (Word exportado + template)
│   │   └── index_archivos/       ← Imágenes generadas por Word
│   ├── calculo-geometria-analitica/
│   ├── redaccion-exposicion/
│   ├── quimica/
│   └── fundamentos-programacion/
│
├── s2/ … s9/                     ← Mismo patrón para cada semestre
│
└── s10/                          ← Décimo Semestre (optativas)
    ├── recursos-necesidades-mexico/
    ├── opt/                      ← Optativas de Ingeniería Aplicada
    └── ext/                      ← Optativas de Otras Carreras
```

Cada `sN/nombre-materia/index.html` se convierte automáticamente en una URL de GitHub Pages:

```
s1/algebra/index.html  →  https://wilbert83.github.io/INGENIERIA-MECATRONICA/s1/algebra/
```

---

## 🛠 Tecnologías

| Capa | Detalle |
|---|---|
| **Markup** | HTML5 semántico |
| **Estilos** | CSS3 — Custom Properties, `color-mix()`, Flexbox, CSS Grid |
| **Lógica** | Vanilla JS ES6+ — `IntersectionObserver`, `localStorage`, `details`/`summary` |
| **Tipografía** | Google Fonts: Space Grotesk · JetBrains Mono · Inter |
| **Despliegue** | GitHub Pages (rama `main`, carpeta raíz) |

> El proyecto no tiene ninguna dependencia de npm, pip ni ningún package manager. No requiere build step.

---

## 📋 Flujo de trabajo: Word → HTML → GitHub

### 1 — Redactar en Word

Usa los estilos de párrafo nativos de Word:

| Estilo Word | Equivalente HTML | Uso |
|---|---|---|
| Título 1 | `<h2>` | Nombre de la materia (oculto en el template) |
| Título 2 | `<h3>` | Tema principal (`1. Trigonometría`) |
| Título 3 | `<h4>` | Subtema (`1.1 Definición de...`) |
| Título 4 | `<h5>` | Apartado de sección |
| Título 5 | `<h6>` | Sub-apartado |
| Normal | `<p>` | Texto del apunte |

### 2 — Exportar desde Word

```
Archivo → Guardar como → Página Web, filtrada (.htm)
```

Esto genera un `.htm` + carpeta `nombre_archivos/` con las imágenes.

### 3 — Integrar en el template

1. Copia `materia-template.html` a `sN/nombre-materia/index.html`
2. Cambia los 5 `<meta>` del encabezado:

```html
<meta name="SEMESTRE"  content="Primer Semestre">
<meta name="MATERIA"   content="Álgebra">
<meta name="CLAVE"     content="1120">
<meta name="CREDITOS"  content="8">
<meta name="COLOR"     content="#C62828">   <!-- color de identidad -->
```

3. Pega el contenido de `<div class=WordSection1>…</div>` del `.htm` exportado dentro de `<div id="word-content">` del template.
4. Mueve la carpeta de imágenes junto al `index.html`.

El JavaScript del template hace automáticamente:
- Extrae el objetivo al hero
- Limpia estilos inline de Word
- Genera el TOC colapsable
- Activa el seguimiento de sección al hacer scroll

### 4 — Publicar en GitHub

```bash
# Añadir la nueva materia
git add s1/algebra/
git commit -m "feat: agregar apunte de Álgebra — S1"
git push

# Actualizar el índice principal (cambiar status de la materia)
git add index.html
git commit -m "feat: activar enlace a Álgebra en el índice"
git push
```

### 5 — Activar una materia en el índice

En `index.html`, localiza la materia en el array `PLAN` y cambia su `status`:

```js
// Pendiente (sin enlace):
{ name: "Álgebra", slug: "algebra", status: "pendiente" }

// En progreso (badge ámbar):
{ name: "Álgebra", slug: "algebra", status: "progreso"  }

// Publicada (enlace activo + badge verde):
{ name: "Álgebra", slug: "algebra", status: "disponible" }
```

---

## 🚀 Despliegue en GitHub Pages

Solo se hace una vez:

1. Ir a `github.com/Wilbert83/INGENIERIA-MECATRONICA`
2. **Settings → Pages**
3. Source: **Deploy from a branch** · Branch: **main** · Folder: **/ (root)**
4. Guardar — en 1-2 minutos el sitio estará en:
   `https://wilbert83.github.io/INGENIERIA-MECATRONICA/`

---

## 📐 Rutas relativas (regla de oro)

Desde cualquier página de materia (`sN/nombre/index.html`):

```
../../index.html    →  índice principal
../../favicon.png   →  logo
imagenes/foto.png   →  imagen local de la materia
```

Siempre **dos niveles arriba** (`../../`) porque todas las materias están a `sN/nombre/`.

---

## 👤 Autor

**Wilbert Miguel Nahuatlato**  
Ingeniero Mecatrónico · UNAM Facultad de Ingeniería · DIMEI · Plan 2016  
GitHub: [@Wilbert83](https://github.com/Wilbert83)

---

## 📄 Licencia

[MIT](LICENSE) — libre para usar, modificar y compartir con atribución.
