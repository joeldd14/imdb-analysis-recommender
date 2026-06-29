# IMDb Analysis & Recommender

> Herramienta de análisis y recomendación de cine y series construida sobre el dataset _IMDb Top 10.000 Movies & TV Series_. Combina un módulo que **predice y explica** la nota de IMDb de un título con un módulo que **recomienda** títulos similares.

**Estado:** En construcción — Fase 1 (EDA y limpieza). Consulta la [hoja de ruta](#hoja-de-ruta) para ver el avance.

---

## Descripción

Este proyecto explora un mismo conjunto de datos de IMDb desde dos ángulos complementarios, reutilizando la misma limpieza y las mismas variables en ambos:

- **Módulo A — Valoración.** A partir de las características de un título (género, año, votos...) se entrena un modelo de aprendizaje supervisado para **predecir** su nota de IMDb y, sobre todo, **explicar** qué variables pesan en esa predicción (interpretabilidad). Como subproducto, los errores del modelo permiten señalar títulos potencialmente **infravalorados** y **sobrevalorados**.

- **Módulo B — Recomendador.** Dado un título, se buscan los más **parecidos** mediante similitud no supervisada sobre esas mismas variables. Es el caso de uso clásico de los sistemas de recomendación: "si te gustó esto, quizá te guste esto otro".

> El objetivo del proyecto es de aprendizaje y portfolio: demostrar un flujo completo de datos de principio a fin (exploración → modelado → evaluación honesta → app desplegada), no superar a un sistema de recomendación comercial.

## Dataset

- **Fuente:** [IMDb Top 10,000 Movies & TV Series — Kaggle](https://www.kaggle.com/datasets/abbas829/imdb-top-10000-movies-and-tv-series-dataset)
- **Licencia del dataset:** CC BY-SA 4.0 (reutilización permitida con atribución; ver la ficha de Kaggle).
- **Tamaño aproximado:** ~10.000 títulos más votados/populares, con géneros anidados, años y más de 3 millones de votos.

> **Los datos no se incluyen en este repositorio.** La carpeta `data/` está ignorada por git para mantener el repo ligero y reproducible; los datos se obtienen del enlace original. Sigue los pasos de [Instalación y reproducción](#instalación-y-reproducción) para descargarlos.

## Estructura del repositorio

```
imdb-analysis-recommender/
├── data/                 # Datos crudos — IGNORADO por git
├── notebooks/            # Exploración y prototipado (EDA, modelado)
├── src/                  # Código reutilizable (carga, limpieza, features…)
├── app/                  # Aplicación de Gradio (Fase 4)
├── .gitignore
├── requirements.txt      # Dependencias del proyecto
├── LICENSE
└── README.md
```

## Instalación y reproducción

> Requiere [Python 3.10+](https://www.python.org/) y una cuenta de [Kaggle](https://www.kaggle.com/).

**1. Clonar el repositorio**

```bash
git clone https://github.com/joeldd14/imdb-analysis-recommender.git
cd imdb-analysis-recommender
```

**2. Crear y activar un entorno virtual**

```bash
python -m venv .venv

# Windows (PowerShell)
.venv\Scripts\activate

# macOS / Linux
source .venv/bin/activate
```

**3. Instalar dependencias**

```bash
pip install -r requirements.txt
```

**4. Configurar las credenciales de Kaggle**

Kaggle usa un token de API que se muestra **una sola vez**. En [kaggle.com](https://www.kaggle.com/) → _Settings_ → sección _API_ → **Generate New Token**, y copia el token (`KGAT_...`). Es una credencial: **no debe subirse nunca al repositorio**.

Guárdalo en el archivo que la CLI lee automáticamente:

- **Windows (PowerShell):**

```powershell
  New-Item -ItemType Directory -Force -Path $env:USERPROFILE\.kaggle | Out-Null
  Set-Content -Path "$env:USERPROFILE\.kaggle\access_token" -Value "TU_TOKEN"
```

- **macOS / Linux:**

```bash
  mkdir -p ~/.kaggle && echo "TU_TOKEN" > ~/.kaggle/access_token && chmod 600 ~/.kaggle/access_token
```

**5. Descargar el dataset**

```bash
kaggle datasets download -d abbas829/imdb-top-10000-movies-and-tv-series-dataset -p data/ --unzip
```

El CSV quedará dentro de `data/`, listo para los notebooks.

## Uso

_Próximamente._ Cuando la aplicación esté lista (Fase 4), aquí se documentará cómo lanzarla
en local y se enlazará la demo pública en Hugging Face Spaces.

## Stack

- **Datos y modelado:** pandas, scikit-learn
- **Interpretabilidad:** SHAP
- **Aplicación:** Gradio, Hugging Face Spaces
- **Mejora futura (NLP):** sentence-transformers (Hugging Face) para recomendación por similitud semántica de sinopsis (posible ampliación del dataset actual, ya que este no contiene las sinopsis)
- **Control de versiones:** Git / GitHub

## Hoja de ruta

- [x] **Fase 0 — Definir y preparar:** repositorio, README y descarga del dataset
- [ ] **Fase 1 — EDA y limpieza:** cargar, entender variables, desanidar géneros, elegir features _(en curso)_
- [ ] **Fase 2 — Módulo A (nota):** baseline → modelo que lo supere → evaluación → interpretabilidad → títulos infra/sobrevalorados
- [ ] **Fase 3 — Módulo B (recomendador):** similitud sobre las features para devolver los N títulos más parecidos
- [ ] **Fase 4 — App y despliegue:** app única en Gradio sobre Hugging Face Spaces
- [ ] **Fase 5 — Documentación y publicación:** README final, capturas y difusión
- [ ] **Mejora (NLP):** recomendador basado en contenido con embeddings de sinopsis (posible ampliación del dataset actual, ya que este no contiene las sinopsis)

## Licencia

Código distribuido bajo licencia [MIT](LICENSE). El dataset pertenece a su autor en Kaggle y está sujeto a la licencia indicada en su ficha.

## Autor

**Joel** — Estudiante de Ingeniería Informática (rama de Computación), UPV · ETSINF.
Orientado a Inteligencia Artificial, Machine Learning y Datos.
