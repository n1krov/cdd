# 📂 Carpeta `Datasets` — Curso de Ciencia de Datos (5º año)

¡Bienvenido/a! Aquí iremos subiendo **todos los conjuntos de datos (datasets)** que usemos en la materia:  
- **Aportes de la cátedra** (material oficial para prácticas y exámenes).  
- **Aportes de alumnos** (datasets propios para laboratorios y proyectos).  

> _Regla de oro_: si el archivo pesa más que la cafetera del laboratorio, mejor **subí un enlace** y una **instrucción reproducible** (API/CLI) para descargarlo. 🧪☕

---

## 🎯 Objetivos de esta carpeta
- Centralizar los datasets usados en clase y proyectos.
- Documentar **origen, licencia y versión** de cada dataset.
- Fomentar buenas prácticas de **reproducibilidad** (scripts de descarga/limpieza).
- Evitar “dataset huérfanos”: todo dataset debe tener su **ficha**.

---

## 🧱 Estructura sugerida

```
Datasets/
├─ README.md                  # este archivo
├─ catalogo.csv               # índice opcional de datasets (nombre, origen, licencia, versión)
├─ oficiales/                 # datasets provistos por la cátedra
│  ├─ 12 Aug 2025-ejemplo/       
│  │  ├─ data/               # archivos .csv/.parquet/.json
│  │  ├─ metadata/           # README_origen.md, LICENSE, schema.json
│  │  └─ notebooks/          # EDA y limpieza
└─ alumnos/
   ├─ equipo-01-nombre-dataset/
   │  ├─ data/
   │  ├─ metadata/
   │  └─ notebooks/
```

**Convenciones de nombre**: `equipo-<NN>-<slug-dataset>` o `{AAAA-MM-DD}-<slug>` para oficiales.

---

## 📝 Ficha obligatoria de cada dataset

Incluí un `metadata/README_origen.md` con:
- **Nombre**:  
- **Autor/es**:  
- **Origen/URL**:  
- **Fecha de descarga**:  
- **Licencia** (ej.: CC BY 4.0, ODbL, Public Domain).  
- **Versión** (número o commit/tag).  
- **Descripción breve** (3–5 líneas).  
- **Esquema** (columnas, tipos, unidades).  
- **Pasos de preparación** (script o notebook).  
- **Limitaciones y sesgos conocidos**.  

> Pro tip: agregá un `schema.json` o `table_schema.json` (frictionless) si el dataset es tabular.

---

## 🧠 Kaggle: ¿qué es y cómo lo usaremos?

**Kaggle** es una plataforma de Google para Ciencia de Datos con:  
- **Datasets públicos**, **Kaggle Notebooks**, **API/CLI**, **modelos** y **competencias**.  
- Excelente para **encontrar** y **compartir** datos, y para ejecutar notebooks en la nube.

### 👉 Cómo lo usaremos en la materia
1. **Búsqueda y selección** de datasets reales para prácticas.  
2. **Descarga reproducible** con la **Kaggle API** (nada de “me lo pasás por WhatsApp”).  
3. **Citación del origen** y **respeto de licencias**.  
4. Publicación de **subsets limpios** de producción del curso (si la licencia lo permite).

### 🚀 Pasos rápidos para usar la API de Kaggle
1. Crear cuenta en Kaggle y **generar token** (`kaggle.json`) en _Account → API → Create New Token_.  
2. Guardar `~/.kaggle/kaggle.json` (Linux/Mac) o `%HOMEPATH%\.kaggle\kaggle.json` (Windows). **No lo comitees**.  
3. Instalar la CLI:
   ```bash
   pip install kaggle
   kaggle --help
   ```
4. Descargar un dataset (ejemplos):
   ```bash
   # YouTube Trending (por país)
   kaggle datasets download -d datasnaek/youtube-new -p ./Datasets/oficiales/youtube_trending/ -u -o

   # Netflix Movies & TV Shows
   kaggle datasets download -d shivamb/netflix-shows -p ./Datasets/oficiales/netflix/ -u -o

   # US Accidents 2016–2023 (muy grande)
   kaggle datasets download -d sobhanmoosavi/us-accidents -p ./Datasets/oficiales/us_accidents/ -u -o
   ```
   _Flags útiles_: `-p` (destino), `-u` (descomprimir), `-o` (sobrescribir), `-f` (archivo específico).

> **Licencias**: verificá siempre la licencia en la página del dataset. Si es restrictiva, **no re-publicar** los datos crudos; subí solo scripts de preparación.

---

## 🌟 3 ejemplos llamativos en Kaggle (para inspirarte)

- **US Accidents (2016–2023)** — dataset masivo de siniestros viales en EE. UU., ideal para geodatos, series temporales y clima.  
  URL: https://www.kaggle.com/datasets/sobhanmoosavi/us-accidents

- **Trending YouTube Video Statistics** — métricas diarias de videos en tendencia (varios países), excelente para _EDA_ y scraping-aware pipelines.  
  URL: https://www.kaggle.com/datasets/datasnaek/youtube-new

- **Netflix Movies and TV Shows** — catálogo (periódicamente actualizado) para análisis de contenido y _recommenders_.  
  URL: https://www.kaggle.com/datasets/shivamb/netflix-shows

### 🏆 ¿El dataset “más descargado”?
Kaggle **no publica un ranking oficial global** de descargas. Entre los datasets con contador visible, **Trending YouTube Video Statistics** figura con **≈ 280 000 descargas** (consultado el 12 Aug 2025). Tómenlo como **referencia**, no como récord absoluto, porque las cifras varían por versión y espejo.

---

## 🌍 10 sitios populares (acceso libre) para descargar datasets

1. **UCI Machine Learning Repository** — clásicos de ML, gran variedad tabular.  
   https://archive.ics.uci.edu/

2. **Google Dataset Search** — buscador vertical de datasets en la web.  
   https://datasetsearch.research.google.com/

3. **Registry of Open Data on AWS** — datos abiertos alojados en Amazon (S3, etc.).  
   https://registry.opendata.aws/

4. **Data.gov (EE. UU.)** — portal de datos abiertos del gobierno federal.  
   https://data.gov/

5. **data.europa.eu (UE)** — portal oficial de datos abiertos de la Unión Europea.  
   https://data.europa.eu/

6. **World Bank Open Data** — indicadores económicos y sociales globales.  
   https://data.worldbank.org/

7. **OECD Data** — estadísticas comparadas de países OCDE.  
   https://www.oecd.org/en/data.html

8. **Our World in Data** — compilaciones curadas sobre temas globales (CSV accesibles).  
   https://ourworldindata.org/

9. **OpenML** — repositorio y API para datasets estandarizados de ML.  
   https://www.openml.org/

10. **Harvard Dataverse** — repositorio académico con DOIs para citar.  
    https://dataverse.harvard.edu/

---

## ✅ Buenas prácticas (checklist rápido)

- [ ] Incluí **ficha** con origen, licencia, fecha y versión.  
- [ ] Subí **scripts de descarga/limpieza** (no subas binarios gigantes si hay fuente pública).  
- [ ] Documentá **pasos para reproducir** (README + `requirements.txt`).  
- [ ] Anonimizá datos sensibles (cumplimiento y ética > curiosidad).  
- [ ] **No** subas `kaggle.json` ni claves a Git.  
- [ ] Si tu dataset pesa >100 MB, considerá **Parquet** o compresión.  

---

## 🤹‍♀️ Nota final con chiste malo
¿Sabías que algunos datasets tienen **outliers** porque… simplemente **no encajan**? 😅  
Tranquilo: para eso están tus skills de limpieza y validación.

---

### Créditos y referencias
- Kaggle Docs — Datasets: https://www.kaggle.com/docs/datasets  
- Kaggle Docs — Public API/CLI: https://www.kaggle.com/docs/api  
- Kaggle API (repo oficial): https://github.com/Kaggle/kaggle-api  
- Datasets de ejemplo: ver enlaces arriba en cada viñeta.

