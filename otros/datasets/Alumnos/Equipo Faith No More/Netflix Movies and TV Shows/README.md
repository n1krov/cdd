# Netflix Shows Dataset

Este conjunto de datos proporciona un catálogo completo de programas de televisión y películas disponibles en Netflix. Es una excelente fuente para el análisis de datos, la visualización y la práctica de habilidades de ciencia de datos con datos del mundo real de una popular plataforma de streaming.

## Contenido

El conjunto de datos netflix_titles.csv contiene las siguientes columnas:

*   *show_id*: ID único para el programa o película.
*   *type*: Tipo de contenido, ya sea 'Movie' (Película) o 'TV Show' (Programa de televisión).
*   *title*: Título del programa o película.
*   *director*: Nombre(s) del director(es).
*   *cast*: Nombres de los principales miembros del reparto.
*   *country*: País(es) donde se produjo el contenido.
*   *date_added*: Fecha en que el contenido se añadió a Netflix.
*   *release_year*: Año en que el contenido fue lanzado originalmente.
*   *rating*: Clasificación por edades del contenido (ej., TV-MA, PG-13).
*   *duration*: Duración del contenido (ej., "90 min" para películas, "1 Season" o "2 Seasons" para programas de televisión).
*   *listed_in*: Género(s) o categoría(s) a los que pertenece el contenido.
*   *description*: Breve descripción o sinopsis del contenido.

## Fuente

Este conjunto de datos fue recopilado de Kaggle por [Shivam Bansal](https://www.kaggle.com/shivamb). Puedes encontrar el conjunto de datos original y más detalles aquí:
[Netflix Shows en Kaggle](https://www.kaggle.com/datasets/shivamb/netflix-shows)

## Posibles Análisis y Preguntas de Investigación

Este conjunto de datos es rico en oportunidades para la exploración de datos. Aquí hay algunas ideas:

*   *Tendencias de Contenido:* ¿Cómo ha cambiado la distribución de películas versus programas de televisión a lo largo de los años?
*   *Popularidad de Géneros:* ¿Qué géneros son los más comunes en Netflix?
*   *Análisis de Directores y Actores:* ¿Qué directores o actores aparecen con más frecuencia? ¿Existen patrones en sus proyectos?
*   *Distribución Geográfica:* ¿De qué países proviene la mayor parte del contenido? ¿Hay diferencias en el tipo de contenido producido por diferentes países?
*   *Clasificaciones por Edad:* ¿Cómo se distribuyen las clasificaciones por edad y si se correlacionan con la duración o el tipo de contenido?
*   *Contenido a lo largo del tiempo:* ¿Cómo ha crecido la biblioteca de Netflix desde su inicio?
*   *Análisis de Duración:* ¿Cuál es la duración promedio de las películas? ¿Cuántas temporadas tienen la mayoría de los programas de televisión?

## Uso

Para usar este conjunto de datos, simplemente descarga el archivo netflix_titles.csv. Se puede leer fácilmente en Python usando la biblioteca Pandas:

python
import pandas as pd

df = pd.read_csv('netflix_titles.csv')
print(df.head())


## Licencia

La licencia de este conjunto de datos generalmente sigue los términos de uso de Kaggle. Para detalles específicos de la licencia, consulta la página del conjunto de datos original en Kaggle.
