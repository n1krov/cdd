¡Perfecto! Empecemos con una introducción clara y luego profundizamos en cada paso.

## 🔬 Introducción al Laboratorio: Ingeniería de Características de Texto

El laboratorio se centra en el **Procesamiento del Lenguaje Natural (NLP)** aplicado al _Machine Learning_.

### 🎯 El Objetivo Central

El propósito del laboratorio es mostrar cómo transformar la **información textual no estructurada** (como descripciones o comentarios) en **características predictivas numéricas**.

- **Texto a Números:** Dado que los modelos de _machine learning_ solo operan con datos numéricos, el texto debe ser cuantificado para poder ser utilizado como _input_ en estos modelos.
    

### 🛠️ Las Técnicas

El enfoque del capítulo es utilizar métodos de ingeniería de características que permiten extraer información rápidamente de **textos cortos**, capturando su complejidad a través de parámetros estadísticos.

Las técnicas se dividen en dos grandes grupos:

1. **Características Estructurales/Estilísticas:** Crean características a partir de parámetros estadísticos del texto, como la longitud de las palabras, el número de palabras únicas o el conteo de oraciones. (Cubierto en Recetas 1 y 2).
    
2. **Características de Contenido/Sintácticas:** Representan el contenido del texto, enfocándose en qué palabras se usan y qué tan importantes son, a través de métodos de vectorización como Bag-of-Words y TF-IDF. (Cubierto en Recetas 3, 4 y 5).
    

---

## 👩‍🏫 Profundización en Cada Receta

Ahora, vamos a ver el detalle de cada una de las 5 "Recetas" del laboratorio.

### 1. Receta 1: Conteo de Caracteres, Palabras y Vocabulario

Esta es la forma más básica de cuantificar un texto y se realiza usando las funciones vectorizadas de _strings_ de **pandas**.

- **Implementación en Python:**
    
    - **Número de Caracteres:** `df["text"].str.strip().str.len()`
        
    - **Número de Palabras:** `df["text"].str.split().str.len()`
        
    - **Número de Vocabulario (Únicas):** Se aplica `.str.lower()` (para unificar mayúsculas/minúsculas) y luego se calcula la longitud del conjunto (`set`) de las palabras divididas.
        
    - **Diversidad Léxica:** Se calcula como `Número total de palabras / Número de palabras únicas`.
        
- **Utilidad:** Las descripciones más largas y ricas en vocabulario único suelen contener más información y pueden ser un predictor fuerte en algunos problemas.
    

---

### 2. Receta 2: Estimación de la Complejidad por Conteo de Oraciones

Aquí se utiliza la librería **NLTK** para realizar la **tokenización de oraciones**.

- **Concepto Clave:** La `sent_tokenize` de NLTK divide el texto en oraciones individuales basándose en la puntuación (puntos, signos de exclamación/interrogación).
    
- **Implementación en Python:** Se define una función que usa `nltk.tokenize.sent_tokenize(text)` y devuelve el número de elementos en la lista resultante. Esta función se aplica a la columna de texto del DataFrame usando `.apply()`.
    
- **Nota Importante:** Este paso **debe hacerse antes** de cualquier eliminación de puntuación o cambio de caso.
    

---

### 3. Receta 3: Bag-of-Words (BoW) y N-grams

Este método convierte el texto en una gran matriz de conteos. Se utiliza el `CountVectorizer` de **scikit-learn**.

- **Pipeline de Transformación:**
    
    1. **Limpieza Previa:** Se recomienda eliminar puntuación y números del texto antes de la vectorización.
        
    2. **Vectorización:**
        
        - `CountVectorizer` crea el vocabulario (todas las palabras únicas) a partir de los documentos.
            
        - Cada palabra del vocabulario se convierte en una **columna** de la matriz resultante.
            
        - Cada fila representa un documento, y el valor es la **frecuencia absoluta** de la palabra en ese documento.
            
    3. **Configuración Común:**
        
        - `stop_words="english"`: Ignora palabras comunes como 'the', 'a', 'is'.
            
        - `ngram_range=(1, 1)`: Indica que solo se considerarán palabras individuales (unigramas). Se podría usar `(1, 2)` para incluir palabras individuales y pares de palabras (bigramas).
            
        - `min_df` o `max_features`: Se utilizan para controlar el tamaño de la matriz, eliminando palabras muy raras o muy comunes, o limitando el total de columnas.
            

---

### 4. Receta 4: Implementación de TF-IDF

Esta técnica refina el BoW asignando un peso a cada palabra según su relevancia, utilizando el `TfidfVectorizer` de **scikit-learn**.

- **Fórmula Conceptual:** $\text{TF-IDF} = \text{TF} \times \text{IDF}$.
    
- **Term Frequency (TF):** La frecuencia de la palabra en el documento.
    
- **Inverse Document Frequency (IDF):** Una medida de cuán rara es la palabra en **toda la colección** de documentos.
    

|**Componente**|**Describe**|**Impacto en el Peso**|
|---|---|---|
|**TF (Frecuencia)**|¿Cuánto aparece la palabra en _este_ documento?|Alto si aparece mucho.|
|**IDF (Rareza)**|¿En cuántos otros documentos de la colección aparece?|Alto si es rara (solo aparece en pocos documentos).|

- **Resultado:** El TF-IDF da un peso **bajo** a palabras muy comunes y un peso **alto** a palabras específicas que son clave para ese documento en particular.
    

---

### 5. Receta 5: Limpieza y Stemming de Variables de Texto

Este es el proceso completo de preprocesamiento, crucial para estandarizar el texto antes de la vectorización (Recetas 3 y 4).

- **Pasos de Limpieza (en orden):**
    
    1. **Puntuación y Números:** Se eliminan o reemplazan por espacios.
        
    2. **Minúsculas:** Conversión a _lowercase_.
        
    3. **Normalización de Espacios:** Múltiples espacios se reducen a uno solo.
        
    4. **Eliminación de Stop Words:** Se usa el conjunto de _stop words_ de NLTK para remover palabras como 'a', 'is', 'the'.
        
    5. **Stemming:** Reducción de las palabras a su raíz usando un _Stemmer_ (como `SnowballStemmer`). Por ejemplo, 'computando', 'computadora' $\rightarrow$ 'comput'.
        
- **Importancia:** Un texto limpio (estandarizado) garantiza que, por ejemplo, 'Corriendo.' y 'correr' sean tratados como la misma característica ('corr') en el BoW o TF-IDF, mejorando la calidad del modelo.
    
