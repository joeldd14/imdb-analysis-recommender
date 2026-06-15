# IMDb Analysis & Recommender

> Herramienta de análisis y recomendación de cine y series construida sobre el dataset *IMDb Top 10.000 Movies & TV Series*. Combina un módulo que **predice y explica** la nota de IMDb de un título con un módulo que **recomienda** títulos similares.

**Estado:** En construcción — Fase 0 (definición y preparación). Consulta la [hoja de ruta](#hoja-de-ruta) para ver el avance.

---

## Descripción

Este proyecto explora un mismo conjunto de datos de IMDb desde dos ángulos complementarios, reutilizando la misma limpieza y las mismas variables en ambos:

- **Módulo A — Valoración.** A partir de las características de un título (género, año, duración, votos, etc.) se entrena un modelo de aprendizaje supervisado para **predecir** su nota de IMDb y, sobre todo, **explicar** qué variables pesan en esa predicción (interpretabilidad). Como subproducto, los errores del modelo permiten señalar títulos potencialmente **infravalorados** y **sobrevalorados**.

- **Módulo B — Recomendador.** Dado un título, se buscan los más **parecidos** mediante similitud no supervisada sobre esas mismas variables. Es el caso de uso clásico de los sistemas de recomendación: "si te gustó esto, quizá te guste esto otro".

> El objetivo del proyecto es de aprendizaje y portfolio: demostrar un flujo completo de datos de principio a fin (exploración → modelado → evaluación honesta → app desplegada), no superar a un sistema de recomendación comercial.

## Dataset

- **Fuente:** [IMDb Top 10,000 Movies & TV Series — Kaggle](https://www.kaggle.com/datasets/abbas829/imdb-top-10000-movies-and-tv-series-dataset)
- **Tamaño aproximado:** ~10.000 títulos mejor valorados, con géneros anidados, años y más de 3 millones de votos.

> **Los datos no se incluyen en este repositorio.** La carpeta `data/` está ignorada por git para no redistribuir el dataset (respetando su licencia en Kaggle) y mantener el repo ligero. Sigue los pasos de [Instalación y reproducción](#instalación-y-reproducción) para descargarlos.

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
git clone https://github.com/<tu-usuario>/imdb-analysis-recommender.git
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

- En [kaggle.com](https://www.kaggle.com/) → *Settings* → *API* → **Create New Token**.
  Esto descarga un archivo `kaggle.json` (es una credencial: **no debe subirse nunca al repositorio**).
- Coloca el archivo en:
  - **Windows:** `C:\Users\<usuario>\.kaggle\kaggle.json`
  - **macOS / Linux:** `~/.kaggle/kaggle.json` (y `chmod 600 ~/.kaggle/kaggle.json`)

**5. Descargar el dataset**

```bash
kaggle datasets download -d abbas829/imdb-top-10000-movies-and-tv-series-dataset -p data/ --unzip
```

El CSV quedará dentro de `data/`, listo para los notebooks.

## Uso

*Próximamente.* Cuando la aplicación esté lista (Fase 4), aquí se documentará cómo lanzarla
en local y se enlazará la demo pública en Hugging Face Spaces.

## Stack

- **Datos y modelado:** pandas, scikit-learn
- **Interpretabilidad:** SHAP
- **Aplicación:** Gradio, Hugging Face Spaces
- **Mejora futura (NLP):** sentence-transformers (Hugging Face) para recomendación por similitud semántica de sinopsis
- **Control de versiones:** Git / GitHub

## Hoja de ruta

- [ ] **Fase 0 — Definir y preparar:** repositorio, README y descarga del dataset *(en curso)*
- [ ] **Fase 1 — EDA y limpieza:** cargar, entender variables, desanidar géneros, elegir features
- [ ] **Fase 2 — Módulo A (nota):** baseline → modelo que lo supere → evaluación → interpretabilidad → títulos infra/sobrevalorados
- [ ] **Fase 3 — Módulo B (recomendador):** similitud sobre las features para devolver los N títulos más parecidos
- [ ] **Fase 4 — App y despliegue:** app única en Gradio sobre Hugging Face Spaces
- [ ] **Fase 5 — Documentación y publicación:** README final, capturas y difusión
- [ ] **Mejora (NLP):** recomendador basado en contenido con embeddings de sinopsis

## Licencia

Código distribuido bajo licencia [MIT](LICENSE). El dataset pertenece a su autor en Kaggle y está sujeto a la licencia indicada en su ficha.

## Autor

**Joel** — Estudiante de Ingeniería Informática (rama de Computación), UPV · ETSINF.
Orientado a Inteligencia Artificial, Machine Learning y Datos.
