# 📚 Prontuario de Ingeniería Mecatrónica

[![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat-square&logo=html5&logoColor=white)](https://developer.mozilla.org/es/docs/Web/HTML)
[![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat-square&logo=css3&logoColor=white)](https://developer.mozilla.org/es/docs/Web/CSS)
[![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black)](https://developer.mozilla.org/es/docs/Web/JavaScript)
[![GitHub Pages](https://img.shields.io/badge/GitHub%20Pages-222222?style=flat-square&logo=github&logoColor=white)](https://wilbert83.github.io/INGENIERIA-MECATRONICA/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green?style=flat-square)](LICENSE)
[![Estado](https://img.shields.io/badge/estado-activo-brightgreen?style=flat-square)]()

> Sitio web personal de apuntes y prontuario de **Ingeniería Mecatrónica** — Plan 2016.  
Apuntes organizados por semestre y materia, con integración completa de NotebookLM (9 tipos de recursos por materia), con sistema de temas, colores de identidad por asignatura y TOC interactivo generado automáticamente desde exportaciones de Word.

🌐 **Demo en vivo:** <https://wilbert83.github.io/INGENIERIA-MECATRONICA/>

---

## ✨ Características

| Característica | Detalle |
|---|---|
| 📖 **Cobertura curricular** | 87 materias · 10 semestres · Plan 2016 |
| 🎨 **Identidad visual por materia** | Cada asignatura tiene su color y emoji únicos |
| 🌗 **Tema oscuro / claro** | Persistido en `localStorage`, sin flash al navegar |
| 🎨 **26 colores de acento** | Selector visual + botón 🎲 aleatorio |
| 🎓 **Secuencia de estudio** | 9 recursos de NotebookLM por materia en orden pedagógico |
| 🎧 **Integración NotebookLM** | Audio, mapa mental, presentación, tarjetas, cuestionario, informe, guía de aprendizaje, infografía y guía de estudio |
| 🃏 **Flashcards automáticas** | Generadas desde términos `<em>` del contenido Word con navegación por teclado |
| 📑 **TOC colapsable** | Generado automáticamente desde los headings del Word exportado |
| 👁️ **Auto-highlight en scroll** | `IntersectionObserver` marca la sección activa en el índice lateral |
| 🔍 **Búsqueda global** | Busca en nombres de materias y temas clave configurables |
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
├── materia-template.html         ← Plantilla reutilizable para cada asignatura
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
│   └── fundamentos-programacion/
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

## 🔄 Flujo de trabajo: Word → HTML → GitHub y 🎓 Secuencia de estudio por materia

Cada página de materia muestra 9 recursos de NotebookLM en orden pedagógico.  
Los recursos con link aparecen activos; los pendientes aparecen atenuados hasta que se configuren.

Usa los estilos de párrafo nativos de Word. La plantilla los mapea así:
| Paso | Recurso | Propósito |
|---|---|---|
| 1 | 🗺️ **Mapa mental** | Estructura visual del tema antes de cualquier lectura |
| 2 | 🎧 **Audio resumen** | Input pasivo — escuchar mientras se hace otra actividad |
| 3 | 📊 **Presentación** | Refuerzo visual con más detalle y estructura |
| 4 | 🖼️ **Infografía** | Vista compacta de conceptos clave |
| 5 | 🃏 **Tarjetas didácticas** | Primer repaso activo concepto por concepto |
| 6 | ❓ **Cuestionario** | Autoevaluación formal |
| 7 | 🧑‍🏫 **Guía de aprendizaje** | Tutor IA que detecta huecos y adapta la explicación |
| 8 | 📝 **Informe** | Consolidación escrita — base para los apuntes Word |
| 9 | 📓 **Guía de estudio** | Notebook completo de la materia como referencia |

---

## 🔄 Flujo de trabajo

### Opción A — Publicar rápido (solo recursos NotebookLM)

Si ya tienes los recursos generados en NotebookLM pero aún no los apuntes en Word:

1. Copiar `materia-template.html` a `sN/nombre-materia/index.html`
2. Rellenar los `<meta>` con los links de NotebookLM
3. Cambiar `status` a `"progreso"` en el índice
4. `git push` — la materia queda publicada con todos sus recursos

La página muestra los 9 pasos con links activos aunque no haya apunte escrito.

### Opción B — Flujo completo con apuntes Word

#### 1 — Redactar en Word

Usa los estilos de párrafo nativos. La plantilla los mapea así:

| Estilo Word | HTML | Resultado visual |
|---|---|---|
| Título 1 | `<h2>` | Nombre de la materia (va al hero automáticamente) |
| Título 2 | `<h3>` | Bloque de tema principal con color de identidad |
| Título 3 | `<h4>` | Subtema con fondo semitransparente |
| Título 4 | `<h5>` | Apartado con línea inferior |
| Normal | `<p>` | Texto del apunte |
| Cursiva / negrita | `<em>` | Término clave → generado como flashcard automática |

#### 2 — Exportar desde Word

```
Archivo → Guardar como → Página Web, filtrada (.htm)
```

Genera un `.htm` + carpeta `nombre_archivos/` con las imágenes incrustadas.

#### 3 — Integrar en la plantilla

1. Copiar `materia-template.html` a `sN/nombre-materia/index.html`
2. Configurar los `<meta>` del encabezado:

```html
<!-- Datos de la materia -->
<meta name="MATERIA"      content="Álgebra">
<meta name="SEMESTRE"     content="Primer Semestre">
<meta name="CLAVE"        content="1120">
<meta name="CREDITOS"     content="8">
<meta name="COLOR"        content="#C62828">

<!-- Recursos NotebookLM — pegar link cuando esté disponible -->
<meta name="MAPA"         content="">
<meta name="AUDIO"        content="">
<meta name="PRESENTACION" content="">
<meta name="INFOGRAFIA"   content="">
<meta name="TARJETAS"     content="">
<meta name="CUESTIONARIO" content="">
<meta name="GUIA_APR"     content="">
<meta name="INFORME"      content="">
<meta name="GUIA"         content="">
```

3. Pegar el contenido de `<div class=WordSection1>…</div>` del `.htm` dentro de `<div id="word-content">`.
4. Mover la carpeta `nombre_archivos/` junto al `index.html`.

El JavaScript de la plantilla hace automáticamente:
- Extrae el objetivo del curso al hero
- Limpia todos los estilos inline de Word
- Genera el TOC lateral colapsable con triángulos ▶
- Genera flashcards desde los términos `<em>` del contenido
- Muestra activos solo los recursos con link configurado

#### 4 — Activar la materia en el índice

En `index.html`, localizar la entrada en el array `PLAN` y cambiar su `status`:

```js
// Sin apunte (punto gris, sin enlace):
{ emoji:"🔢", name: "Álgebra", slug: "algebra", status: "pendiente" }

// Recursos disponibles, apunte en proceso (badge ámbar):
{ emoji:"🔢", name: "Álgebra", slug: "algebra", status: "progreso" }

// Apunte publicado (enlace activo, badge verde):
{ emoji:"🔢", name: "Álgebra", slug: "algebra", status: "disponible" }
```

Para habilitar badges de NotebookLM en las tarjetas del índice y búsqueda por temas:

```js
{ emoji:"🔢", name: "Álgebra", slug: "algebra", status: "disponible",
  audio: "https://notebooklm.google.com/...",   // muestra badge 🎧
  guia:  "https://notebooklm.google.com/...",   // muestra badge 📄
  temas: ["trigonometria", "polinomios", "matrices", "sistemas de ecuaciones"] }
```

#### 5 — Publicar

```bash
# Nueva materia
git add sN/nombre-materia/
git commit -m "feat: agregar apunte de NombreMateria — SN"

# Actualizar índice
git add index.html
git commit -m "feat: activar NombreMateria en el índice"

git push
```

GitHub Pages actualiza el sitio en ~1 minuto.

---

## 🚀 Activar GitHub Pages (una sola vez)

1. Ir al repositorio: `github.com/Wilbert83/INGENIERIA-MECATRONICA`
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
| Imagen local del Word | `index_archivos/imagen.png` |

---

## 🛠 Tecnologías

| Capa | Detalle |
|---|---|
| **Markup** | HTML5 semántico |
| **Estilos** | CSS3 — Custom Properties, `color-mix()`, Grid, Flexbox, `details`/`summary` |
| **Lógica** | Vanilla JS ES6+ — `IntersectionObserver`, `localStorage`, template literals |
| **Tipografía** | Google Fonts: Space Grotesk · JetBrains Mono · Inter |
| **IA** | NotebookLM — 9 tipos de recursos por materia, 49 notebooks activos |
| **Despliegue** | GitHub Pages — sin servidor, sin build step, sin dependencias |

---

## 👤 Autor

**Wilbert Miguel Nahuatlato**  
Ingeniero Mecatrónico · UNAM Facultad de Ingeniería  
GitHub: [@Wilbert83](https://github.com/Wilbert83)

---

## 📄 Licencia

[MIT](LICENSE) — libre para usar, modificar y compartir con atribución.