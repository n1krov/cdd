¡Perfecto! Empecemos con una introducción clara y luego profundizamos en cada paso.

## 🔬 Introducción al Laboratorio: Ingeniería de Características de Texto

El laboratorio se centra en el **Procesamiento del Lenguaje Natural (NLP)** aplicado al _Machine Learning_.

### 🎯 El Objetivo Central

El propósito del laboratorio es mostrar cómo transformar la **información textual no estructurada** (como descripciones o comentarios) en **características predictivas numéricas**.


> En este contexto, una **característica** (o _feature_) es una **variable numérica y medible** que se extrae del texto crudo para que pueda ser utilizada como _input_ en un modelo de _machine learning_.

- **Texto a Números:** Dado que los modelos de _machine learning_ solo operan con datos numéricos, el texto debe ser cuantificado para poder ser utilizado como _input_ en estos modelos.

### 🛠️ Las Técnicas

El enfoque del capítulo es utilizar métodos de ingeniería de características que permiten extraer información rápidamente de **textos cortos**, capturando su complejidad a través de parámetros estadísticos.


##### 1. Características Estructurales/Estilísticas 📏

Estas características se centran en la **estructura física y el estilo de escritura** del texto, ignorando el significado específico de las palabras. Miden **cómo está escrito** el texto.

- **Pregunta Clave:** ¿Cómo está organizada la información?
    
- **Qué Miden:** **Parámetros estadísticos** del texto.
    
    - **Longitud:** ¿Es un texto largo o corto? (Número de caracteres, número de palabras).
        
    - **Diversidad:** ¿Qué tan variado es el vocabulario? (Número de palabras únicas).
        
    - **Estructura:** ¿Cuántas ideas completas contiene? (Conteo de oraciones).
        
- **Analogía:** Es como clasificar un libro por su número de páginas, el tamaño de la letra o la cantidad de capítulos, sin leer la trama.
    
- **Recetas del Laboratorio:** Cubiertas en la **Receta 1** (Conteo de palabras/caracteres) y **Receta 2** (Conteo de oraciones).
    

##### 2. Características de Contenido/Sintácticas 🧠

Estas características se centran en el **contenido semántico** del texto y la **importancia de las palabras**. Miden **de qué trata** el texto.

- **Pregunta Clave:** ¿Qué palabras se usan y qué tan importantes son?
    
- **Qué Miden:** La presencia, la frecuencia y el peso de las palabras.
    
    - **Contenido:** Se registra qué palabras aparecen y cuántas veces (Bag-of-Words - BoW).
        
    - **Importancia:** Se pondera la relevancia de cada palabra en relación con el conjunto completo de documentos (TF-IDF).
        
- **Analogía:** Es como clasificar un libro por las 100 palabras clave más importantes que utiliza ("magia," "dragón," "profecía").
    
- **Recetas del Laboratorio:** Cubiertas en la **Receta 3** (Bag-of-Words), **Receta 4** (TF-IDF), y la **Receta 5** (Limpieza y Stemming, que es un paso de preparación crucial para el contenido).



## 👩‍🏫 Profundización en Cada Receta

Ahora, vamos a ver el detalle de cada una de las 5 "Recetas" del laboratorio.

### 1. Receta 1: Conteo de Caracteres, Palabras y Vocabulario

Esta es la forma más básica de cuantificar un texto y se realiza usando las funciones vectorizadas de _strings_ de **pandas**.

- **Implementación en Python:**
    
    - **Número de Caracteres:** `df["text"].str.strip().str.len()`
        
    - **Número de Palabras:** `df["text"].str.split().str.len()`

	- 1. Número de Vocabulario (Palabras Únicas)
		Esta es una **medida absoluta** de la riqueza del vocabulario
		- **Definición:** Es el **conteo directo** de cuántas palabras diferentes aparecen en el texto.
		- **Implementación:** Se usa `len(set(palabras))`. El conjunto (`set`) elimina duplicados, dejando solo las palabras únicas.
		- **Ejemplo:** En la frase: "La casa azul, la casa es grande", el vocabulario único es {'la', 'casa', 'azul', 'es', 'grande'}, dando un **Número de Vocabulario = 5**.
    

	-  2. Diversidad Léxica

		Esta es una **medida relativa** que indica la tasa de **repetición** o **variedad** de palabras.

		- Definición: Es un cociente entre el número total de palabras y el número de palabras únicas.
	    $$\text{Diversidad Léxica} = \frac{\text{Número total de palabras}}{\text{Número de palabras únicas}}$$
		- **Interpretación:**
		    - Un valor **cercano a 1** indica **mucha diversidad**, es decir, se repiten muy pocas palabras (casi todas las palabras usadas son únicas).
		    - Un valor **alto** (mayor que 1, a menudo 2, 3 o más) indica **poca diversidad**; el texto es repetitivo y reutiliza las mismas palabras con frecuencia.
        
- **Ejemplo (Continuación):**
    
    - Número total de palabras (contando repeticiones): 7 ("La", "casa", "azul", "la", "casa", "es", "grande")
    - Número de Vocabulario (Únicas): 5
    - **Diversidad Léxica:** $7 / 5 = 1.4$. Un valor moderado que indica cierta repetición de palabras como 'la' y 'casa'.        

¡Claro! La Receta 2 es muy sencilla y se enfoca en una idea: **contar cuántas ideas completas tiene un texto** para medir su complejidad o densidad de información.

---

#### 📜 Receta 2: Contar las Ideas (Conteo de Oraciones)

##### 🎯 El Objetivo

El objetivo de esta receta es crear una **característica numérica** que represente la **cantidad de oraciones** que hay en un documento.

- **¿Por qué importa?** Un texto con diez oraciones probablemente contiene más información o es más complejo que un texto con solo una oración.
    

##### 🔑 El Proceso: Tokenización de Oraciones

Para contar las oraciones, se usa una técnica de NLP llamada **Tokenización de Oraciones**.

1. **Herramienta:** Se utiliza la función `sent_tokenize` de la librería **NLTK** (Natural Language Toolkit).
    
2. **Mecanismo:** Esta función "rompe" o divide el texto cada vez que encuentra un signo de puntuación que marca el final de una oración (como un punto `.`, un signo de interrogación `?` o un signo de exclamación `!`).
    
3. **Resultado:** `sent_tokenize` devuelve una **lista** donde cada elemento es una oración completa.
    

##### 💻 Implementación Fácil (El Código)

El código simplemente hace esto:

1. Aplica `sent_tokenize` al texto para obtener la lista de oraciones.
    
2. Cuenta **cuántos elementos tiene esa lista** (`len()`).
    
3. Ese conteo es el valor numérico de la nueva característica (`num_sent`) para ese documento.
    

|**Texto Original**|**Oraciones Tokenizadas (Lista)**|**Característica Numérica**|
|---|---|---|
|"Hoy es martes. ¿Vendrás al laboratorio?"|`['Hoy es martes.', '¿Vendrás al laboratorio?']`|**2**|

##### 🛑 La Regla de Oro

La **Nota Importante** es crucial: **Este conteo debe hacerse primero.**

- **La razón:** Si haces la limpieza de texto (Receta 5) antes, eliminarías los puntos, signos de interrogación y exclamación. Si no hay puntuación, la función `sent_tokenize` no tendrá cómo saber dónde termina una idea y comienza la siguiente, y el conteo será incorrecto.
    

**En resumen:** La Receta 2 nos da el número de "ideas" que tiene el texto, y debe ser el primer paso de preprocesamiento que involucre la puntuación.


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
    
