# 📁 Estructura de carpetas — Prontuario Mecatrónica UNAM
## GitHub Pages · Plan 2016 · Wilbert83

---

## 🗂 Estructura completa del repositorio

```
INGENIERIA-MECATRONICA/          ← raíz del repositorio
│
├── index.html                   ← página principal (índice de semestres)
├── favicon.png                  ← logo IM (puedes extraerlo del base64 del index)
├── README.md                    ← descripción del repo en GitHub
│
├── s1/                          ← Primer Semestre
│   ├── algebra/
│   │   ├── index.html           ← apunte de Álgebra
│   │   └── imagenes/            ← imágenes exportadas del Word
│   │       ├── triangulo.png
│   │       └── grafica-01.png
│   ├── calculo-geometria-analitica/
│   │   ├── index.html
│   │   └── imagenes/
│   ├── redaccion-exposicion/
│   │   └── index.html
│   ├── quimica/
│   │   └── index.html
│   └── fundamentos-programacion/
│       └── index.html
│
├── s2/                          ← Segundo Semestre
│   ├── algebra-lineal/
│   │   └── index.html
│   ├── calculo-integral/
│   │   └── index.html
│   ├── fisica-experimental/
│   │   └── index.html
│   ├── estatica/
│   │   └── index.html
│   └── dibujo-mecanico-industrial/
│       └── index.html
│
├── s3/                          ← Tercer Semestre
│   ├── probabilidad/
│   ├── calculo-vectorial/
│   ├── ecuaciones-diferenciales/
│   ├── cinematica-dinamica/
│   ├── manufactura-1/
│   └── cultura-comunicacion/
│
├── s4/ ... s9/                  ← igual para los demás semestres
│
└── s10/                         ← Décimo Semestre
    ├── recursos-necesidades-mexico/
    ├── proyecto-ingenieria/
    ├── opt/                     ← Optativas (carpeta especial)
    │   ├── inteligencia-artificial/
    │   ├── robotica-movil/
    │   └── ...
    └── ext/                     ← Otras carreras
        ├── electronica-potencia/
        └── ...
```

---

## 🔗 Cómo funciona la URL final

Cuando actives GitHub Pages, cada carpeta con `index.html` se convierte en una URL:

| Archivo en el repo | URL en GitHub Pages |
|---|---|
| `index.html` | `https://wilbert83.github.io/INGENIERIA-MECATRONICA/` |
| `s1/algebra/index.html` | `https://wilbert83.github.io/INGENIERIA-MECATRONICA/s1/algebra/` |
| `s3/ecuaciones-diferenciales/index.html` | `https://wilbert83.github.io/INGENIERIA-MECATRONICA/s3/ecuaciones-diferenciales/` |

Por eso en el `index.html` principal, los slugs ya están listos:
```js
{ name: "Álgebra", slug: "algebra", status: "disponible" }
// genera el enlace: s1/algebra/
```

---

## ✅ Cómo activar una materia en el index.html

Cuando ya tienes el `index.html` de una materia listo, sólo cambia su `status`:

```js
// Antes (pendiente):
{ name: "Álgebra", slug: "algebra", status: "pendiente" }

// Después (publicada):
{ name: "Álgebra", slug: "algebra", status: "disponible" }

// Si está en proceso:
{ name: "Álgebra", slug: "algebra", status: "progreso" }
```

Eso es todo — el index automáticamente la convierte en enlace clickeable y actualiza el contador.

---

## 📋 Flujo de trabajo: Word → HTML → GitHub

### Paso 1 — Escribe en Word
Redacta tu apunte con títulos (Título 1, Título 2, Título 3), párrafos, tablas y fórmulas.

### Paso 2 — Exporta a HTML desde Word
- Archivo → Guardar como → **Página Web, filtrada (.htm)**
- Elige **NO** guardar con carpeta extra (o usa la carpeta de imágenes que genera)
- Renombra el archivo a `index.html`

### Paso 3 — Limpia el HTML de Word
El HTML de Word trae mucha basura (estilos inline, clases raras). Lo más fácil:
1. Abre el archivo en tu editor (VS Code).
2. Copia sólo el texto del `<body>` de Word.
3. Pégalo dentro de `<article class="content">` del template `materia-template.html`.
4. Envuelve cada sección en `<section class="topic" id="tema-N">`.
5. Las imágenes que Word exportó van a la carpeta `imagenes/` de esa materia.

### Paso 4 — Sube a GitHub
```bash
# Primera vez (ya tienes el repo clonado)
git add .
git commit -m "Agrego apunte de Álgebra — S1"
git push

# Para actualizaciones posteriores
git add s1/algebra/
git commit -m "Actualizo tema 2 de Álgebra"
git push
```

---

## 🚀 Activar GitHub Pages (sólo se hace una vez)

1. Ve a tu repo: `github.com/Wilbert83/INGENIERIA-MECATRONICA`
2. Click en **Settings** → sección **Pages**
3. En "Source" selecciona: **Deploy from a branch**
4. Branch: **main** / Folder: **/ (root)**
5. Click **Save**
6. En 1-2 minutos aparece el link: `https://wilbert83.github.io/INGENIERIA-MECATRONICA/`

---

## 📐 Rutas relativas — regla de oro

Dentro de cada `index.html` de materia, las rutas a recursos son **relativas** al archivo:

| Estás en... | Para llegar a... | Ruta |
|---|---|---|
| `s1/algebra/index.html` | el `index.html` principal | `../../index.html` |
| `s1/algebra/index.html` | `favicon.png` en la raíz | `../../favicon.png` |
| `s1/algebra/index.html` | una imagen local | `imagenes/mi-imagen.png` |
| `s3/ecuaciones-diferenciales/index.html` | el índice | `../../index.html` |

**Siempre dos niveles arriba** (`../../`) porque todas las materias viven dos carpetas adentro de la raíz (`s1/algebra/`).

---

## 💡 Tips rápidos

- **Imágenes de Word**: cuando exportas como "Página Web filtrada", Word crea una carpeta `nombre_archivos/` con las imágenes. Muévelas a `imagenes/` dentro de la carpeta de la materia y actualiza los `src=""` en el HTML.
- **Fórmulas de Word**: si tienes ecuaciones del editor de Word, considera convertirlas a texto Unicode (ej. `sen²(α) + cos²(α) = 1`) o usar una librería como MathJax añadiendo este script al template de materia: `<script src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>`
- **VS Code**: instala la extensión **Live Server** para previsualizar los cambios localmente antes de subir a GitHub.
- **Git Desktop**: si no quieres usar la terminal, GitHub Desktop hace lo mismo con interfaz gráfica.

---

## 🔄 Ciclo de actualización

```
Editas Word
    ↓
Exportas / copias a HTML
    ↓
Pruebas local con Live Server
    ↓
git add + commit + push
    ↓
GitHub Pages actualiza automáticamente (~1 min)
```

---

*Prontuario personal · UNAM FI · Ingeniería Mecatrónica · Plan 2016 · Wilbert83*
