# 📚 Prontuario de Ingeniería Mecatrónica

[![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat-square&logo=html5&logoColor=white)](https://developer.mozilla.org/es/docs/Web/HTML)
[![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat-square&logo=css3&logoColor=white)](https://developer.mozilla.org/es/docs/Web/CSS)
[![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black)](https://developer.mozilla.org/es/docs/Web/JavaScript)
[![GitHub Pages](https://img.shields.io/badge/GitHub%20Pages-222222?style=flat-square&logo=github&logoColor=white)](https://wilbert83.github.io/INGENIERIA-MECATRONICA/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green?style=flat-square)](LICENSE)
[![Estado](https://img.shields.io/badge/estado-activo-brightgreen?style=flat-square)]()

> Sitio web personal de apuntes y prontuario de **Ingeniería Mecatrónica** — Plan 2016.  
Apuntes organizados por semestre, materia y área, con integración de IA (NotebookLM),  
con sistema de temas, colores de identidad por materia y TOC interactivo generado automáticamente desde exportaciones de Word.

🌐 **Demo en vivo:** <https://wilbert83.github.io/INGENIERIA-MECATRONICA/>

---

## ✨ Características

| Característica | Detalle |
|---|---|
| 📖 **Cobertura curricular** | 87 materias · 10 semestres · Plan 2016 |
| 🎨 **Identidad visual por materia** | Cada asignatura tiene su color y emoji únicos |
| 🌗 **Tema oscuro / claro** | Persistido en `localStorage`, sin flash al navegar |
| 🎨 **26 colores de acento** | Selector visual + botón 🎲 aleatorio |
| 🎧 **Integración NotebookLM** | Botones de Audio Overview y guía de estudio por materia |
| 👁️ **Auto-highlight en scroll** | `IntersectionObserver` marca la sección activa en el índice lateral |
| 🔍 **Búsqueda global** | Busca en nombres de materias y lista de temas clave |
| 🏛 **Página 404 personalizada** | Mismo sistema de temas y colores que el sitio principal |
| ⚡ **Sin dependencias** | 100 % vanilla HTML/CSS/JS — sin frameworks, sin `npm`, sin build step |
| 🚀 **GitHub Pages ready** | Archivos estáticos, despliegue desde rama `main` |

---

## 🗂 Estructura del repositorio

```
INGENIERIA-MECATRONICA/
│
├── index.html                    ← Índice principal (semestres + materias)
├── 404.html                      ← Página de error personalizada
├── README.md
├── .gitignore
│
├── s1/                           ← Primer Semestre
│   ├── algebra/
│   │   ├── index.html            ← Apunte de Álgebra (Word exportado + template)
│   │   └── index_archivos/       ← Imágenes exportadas por Word
│   ├── calculo-geometria-analitica/
│   ├── redaccion-exposicion/
│   ├── quimica/
│   ├── fundamentos-programacion/
│   └── ...
│
├── s2/ … s9/                     ← Mismo patrón para cada semestre
│
└── s10/                          ← Décimo Semestre (optativas)
    ├── opt/                      ← Optativas de Ingeniería Aplicada
    └── ext/                      ← Optativas de Otras Carreras
```

Cada `sN/nombre-materia/index.html` se convierte automáticamente en una URL:

```
s1/algebra/index.html  →  https://wilbert83.github.io/INGENIERIA-MECATRONICA/s1/algebra/
```

---

## 🔄 Flujo de trabajo: Word → HTML → GitHub

### 1 — Redactar en Word

Usa los estilos de párrafo nativos de Word. La plantilla los mapea así:

| Estilo Word | HTML | Resultado visual |
|---|---|---|
| Título 1 | `<h2>` | Nombre de la materia (oculto — va al hero) |
| Título 2 | `<h3>` | Bloque de tema principal (fondo sólido con color de materia) |
| Título 3 | `<h4>` | Subtema (fondo semitransparente) |
| Título 4 | `<h5>` | Apartado con línea inferior |
| Normal | `<p>` | Texto del apunte |
| Cursiva/negrita | `<em>` | Término clave → generador de flashcards |

### 2 — Exportar desde Word

```
Archivo → Guardar como → Página Web, filtrada (.htm)
```

Genera un `.htm` + carpeta `nombre_archivos/` con las imágenes.

### 3 — Integrar en la plantilla

1. Copiar `materia-template.html` a `sN/nombre-materia/index.html`
2. Cambiar los 7 `<meta>` del encabezado:

```html
<meta name="MATERIA"   content="Álgebra">
<meta name="SEMESTRE"  content="Primer Semestre">
<meta name="CLAVE"     content="1120">
<meta name="CREDITOS"  content="8">
<meta name="COLOR"     content="#C62828">
<meta name="AUDIO"     content="">   <!-- NotebookLM Audio Overview URL -->
<meta name="GUIA"      content="">   <!-- NotebookLM notebook / PDF URL -->
```

3. Pegar el contenido de `<div class=WordSection1>…</div>` del `.htm` dentro de `<div id="word-content">`.
4. Mover la carpeta `nombre_archivos/` junto al `index.html`.

El JavaScript de la plantilla hace automáticamente:
- Extrae el objetivo del curso al hero
- Limpia estilos inline de Word
- Genera el TOC colapsable con triángulos ▶
- Muestra botones de audio y guía si los meta tienen URL

### 4 — Activar la materia en el índice principal

En `index.html`, localizar la materia en el array `PLAN` y cambiar su `status`:

```js
// Pendiente (sin enlace, punto gris):
{ emoji:"🔢", name: "Álgebra", slug: "algebra", status: "pendiente" }

// En progreso (badge ámbar):
{ emoji:"🔢", name: "Álgebra", slug: "algebra", status: "progreso" }

// Publicada (enlace activo + badge verde):
{ emoji:"🔢", name: "Álgebra", slug: "algebra", status: "disponible" }
```

Para agregar NotebookLM y temas de búsqueda:

```js
{ emoji:"🔢", name: "Álgebra", slug: "algebra", status: "disponible",
  audio: "https://notebooklm.google.com/...",
  guia:  "https://notebooklm.google.com/...",
  temas: ["trigonometria", "polinomios", "matrices", "sistemas de ecuaciones"] }
```

### 5 — Publicar

```bash
git add s1/algebra/
git commit -m "feat: agregar apunte de Álgebra — S1"

git add index.html
git commit -m "feat: activar enlace de Álgebra en el índice"

git push
```

---

## 🚀 Activar GitHub Pages (una sola vez)

1. Ir al repositorio en GitHub `github.com/Wilbert83/INGENIERIA-MECATRONICA`
2. **Settings → Pages**
3. Source: **Deploy from a branch** · Branch: **main** · Folder: **/ (root)**
4. Guardar — en 1-2 minutos el sitio estará en:
   `https://wilbert83.github.io/INGENIERIA-MECATRONICA/`

---

## 📐 Rutas relativas

Desde cualquier página de materia (`sN/nombre/index.html`):

| Destino | Ruta |
|---|---|
| Índice principal | `../../index.html` |
| Favicon | `../../favicon.png` |
| Imagen local | `index_archivos/imagen.png` |

---

## 🛠 Tecnologías

| Capa | Detalle |
|---|---|
| **Markup** | HTML5 semántico |
| **Estilos** | CSS3 — Custom Properties, `color-mix()`, Grid, Flexbox, `details`/`summary` |
| **Lógica** | Vanilla JS ES6+ — `IntersectionObserver`, `localStorage`, template literals |
| **Tipografía** | Google Fonts: Space Grotesk · JetBrains Mono · Inter |
| **IA** | NotebookLM — audio overviews + chatbot por materia (externo) |
| **Despliegue** | GitHub Pages — sin servidor, sin build step, sin dependencias |

---

## 👤 Autor

**Wilbert Miguel Nahuatlato**  
Ingeniero Mecatrónico · UNAM Facultad de Ingeniería  
GitHub: [@Wilbert83](https://github.com/Wilbert83)

---

## 📄 Licencia

[MIT](LICENSE) — libre para usar, modificar y compartir con atribución.