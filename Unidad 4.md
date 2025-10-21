
## 🧠 Aprendizaje Supervisado

> [!definition]  
> **Aprendizaje supervisado** es cuando un modelo aprende a partir de ejemplos que **ya tienen respuestas correctas** (llamadas **etiquetas** o _labels_).

- Tenemos un conjunto de datos con **entradas (inputs)** y **salidas esperadas (outputs)**.
    
- El modelo aprende la relación entre ambos para poder **predecir la salida correcta** en casos nuevos.
    

### 🔹 Ejemplo simple

Imaginá que querés que una computadora aprenda a reconocer si un correo es **spam o no spam**.

|Email (texto)|Etiqueta|
|---|---|
|“¡Has ganado un premio!”|Spam|
|“Reunión a las 10:00”|No spam|

➡️ El modelo aprende de estos ejemplos, y luego puede predecir si un nuevo correo es spam o no.  
👉 Es “supervisado” porque **alguien (el humano)** le dice cuál es la respuesta correcta durante el entrenamiento.

---

## 🧩 Aprendizaje No Supervisado

> [!definition]  
> **Aprendizaje no supervisado** es cuando el modelo **no tiene etiquetas**; sólo recibe los datos y debe **descubrir patrones ocultos** por sí mismo.

- El objetivo no es predecir una etiqueta, sino **entender la estructura interna de los datos**.
    
- El modelo busca **grupos, similitudes o relaciones** dentro del conjunto de datos.
    

### 🔹 Ejemplo simple

Supongamos que tenés una base de datos con información de clientes, pero **sin saber quiénes son clientes frecuentes, nuevos o inactivos**.

|Cliente|Compras por mes|Monto promedio|
|---|---|---|
|A|2|$50|
|B|15|$200|
|C|1|$40|

➡️ El algoritmo puede descubrir **grupos naturales**:

- Grupo 1: clientes frecuentes
    
- Grupo 2: clientes nuevos
    
- Grupo 3: clientes inactivos
    

👉 El modelo **descubre estas categorías por sí solo**, sin que nadie le haya dicho cuáles existen.

---

## 🔍 Clustering

> [!definition]  
> **Clustering** (agrupamiento) es una técnica del aprendizaje no supervisado que **agrupa datos similares entre sí** en función de sus características.

- Cada grupo se llama **“cluster”**.
    
- Los datos dentro de un mismo cluster son **parecidos**, y los de clusters distintos son **diferentes**.
    

### 🔹 Ejemplo visual

Imaginá que tenés puntos en un gráfico según **edad** y **gasto mensual**:

```
     ↑ gasto mensual
     |
300  |       ●●●
200  |    ●●●
100  | ●●
     +--------------------→ edad
       20   30   40   50
```

➡️ El algoritmo de _clustering_ detecta que hay **3 grupos** de comportamiento:

- Jóvenes con bajo gasto
    
- Adultos con gasto medio
    
- Mayores con gasto alto
    

---

### 🧩 Algoritmos comunes de clustering

- **K-Means** → agrupa según cercanía de puntos en el espacio.
    
- **Hierarchical Clustering** → crea una jerarquía de grupos.
    
- **DBSCAN** → encuentra grupos de cualquier forma y detecta valores atípicos (_outliers_).
    


---


## 🎯 Clasificación

> [!definition]  
> **Clasificación** es un tipo de **aprendizaje supervisado** donde el modelo aprende a **asignar una etiqueta o categoría conocida** a cada dato nuevo.

- Los datos de entrenamiento **ya tienen etiquetas** (por ejemplo: “spam” o “no spam”).
    
- El modelo aprende a reconocer los **patrones que distinguen cada clase**.
    
- Luego, cuando recibe un dato nuevo, **predice su clase**.
    

### 🔹 Ejemplo

Querés que tu modelo identifique si una foto es de un **gato 🐱** o de un **perro 🐶**.

|Imagen|Etiqueta|
|---|---|
|🐱|Gato|
|🐶|Perro|
|🐶|Perro|
|🐱|Gato|

➡️ El modelo aprende qué características visuales corresponden a cada clase.  
Después, cuando le das una imagen nueva, te dice:  
👉 “Esto parece un **gato**.”

---

## 🔍 Clustering

> [!definition]  
> **Clustering** es un tipo de **aprendizaje no supervisado** que busca **agrupar datos similares entre sí**, **sin saber de antemano qué categorías existen**.

- No hay etiquetas conocidas.
    
- El algoritmo intenta descubrir **patrones naturales** o **grupos ocultos** en los datos.
    
- Sirve para **explorar** o **entender la estructura interna** del conjunto de datos.
    

### 🔹 Ejemplo

Tenés miles de fotos de animales 🐾, pero no sabés cuáles son gatos, perros o conejos.  
Le das todas al algoritmo de clustering.

El algoritmo agrupa automáticamente las imágenes en **tres clusters**:

- Cluster 1: fotos con orejas puntiagudas → “posibles gatos”
    
- Cluster 2: hocicos grandes → “posibles perros”
    
- Cluster 3: orejas largas → “posibles conejos”
    

👉 No le diste nombres ni etiquetas; él los descubrió solo.

---

## ⚖️ Diferencias clave

|Aspecto|Clasificación 🧭|Clustering 🔍|
|---|---|---|
|Tipo de aprendizaje|**Supervisado**|**No supervisado**|
|Etiquetas conocidas|✅ Sí|❌ No|
|Objetivo|Predecir una **clase específica**|Descubrir **grupos naturales**|
|Ejemplo típico|Detectar spam / no spam|Agrupar clientes según comportamiento|
|Resultado|“Clase” o “categoría” conocida|“Cluster” sin nombre previo|

---

### 🧠 Analogía simple

Imaginá una maestra en clase:

- **Clasificación:** la maestra ya tiene la lista con quiénes aprobaron o reprobaron, y entrena al modelo para predecir eso.
    
- **Clustering:** la maestra no tiene esa lista; observa cómo se comportan los alumnos y agrupa a los parecidos (los que participan mucho, los que son callados, etc.).
    

---

## 🧭 1. Cuándo usar **Clasificación**

> [!definition]  
> Usá **clasificación** cuando **ya sabés cuáles son las categorías posibles** y **tenés ejemplos etiquetados** de cada una.

### ✅ Se usa cuando:

- Tenés **datos históricos** con **etiquetas conocidas**.
- Tu objetivo es **predecir la etiqueta** de un nuevo dato.
- Querés **automatizar una decisión** que hoy hacen personas.

### 💡 Ejemplos:

|Caso|Qué hace el modelo|
|---|---|
|📨 Detección de spam|Clasifica emails en “spam” o “no spam”.|
|❤️ Diagnóstico médico|Predice si un paciente tiene o no una enfermedad.|
|👟 E-commerce|Clasifica productos en categorías (“ropa”, “tecnología”, etc.).|
|💬 Chatbots|Detecta la intención del mensaje: “consulta”, “reclamo”, “saludo”.|

### 🎯 En resumen:

> Sabés **qué etiquetas existen** y querés que el modelo **aprenda a reconocerlas automáticamente**.

---

## 🔍 2. Cuándo usar **Clustering**

> [!definition]  
> Usá **clustering** cuando **no sabés cuántas categorías hay**, **no tenés etiquetas**, y querés **descubrir patrones o grupos naturales**.

### ✅ Se usa cuando:

- No conocés las clases o categorías de los datos.
    
- Querés **explorar** o **segmentar** tus datos.
    
- Buscás **entender relaciones ocultas** o **patrones de comportamiento**.
    

### 💡 Ejemplos:

|Caso|Qué hace el modelo|
|---|---|
|🧑‍🤝‍🧑 Segmentación de clientes|Agrupa clientes por hábitos de compra (frecuentes, ocasionales, nuevos).|
|🎶 Recomendaciones musicales|Agrupa canciones por similitud de ritmo o estilo.|
|🧬 Análisis genético|Agrupa genes o muestras con comportamientos parecidos.|
|🛰️ Detección de anomalías|Encuentra datos que no encajan en ningún grupo (posibles fraudes o errores).|

### 🎯 En resumen:

> No sabés qué grupos hay; el modelo **te ayuda a descubrirlos** y entender la estructura de los datos.

---

## ⚖️ 3. Diferencia práctica y guía rápida

|Situación|Técnica recomendada|
|---|---|
|Tenés etiquetas (“spam/no spam”, “enfermo/sano”)|**Clasificación**|
|No tenés etiquetas y querés descubrir patrones|**Clustering**|
|Querés predecir una categoría conocida|**Clasificación**|
|Querés agrupar datos similares sin saber los grupos|**Clustering**|
|Objetivo: decisión o predicción|**Clasificación**|
|Objetivo: exploración o segmentación|**Clustering**|

---

## 🧠 Analogía sencilla

Imaginá una escuela:

- **Clasificación:** el profesor ya sabe quién es de qué curso (1°, 2°, 3°).  
    👉 El modelo aprende a reconocer el curso de cada alumno nuevo según su edad, notas, etc.
    
- **Clustering:** el profesor no tiene cursos definidos. Observa a los alumnos y los agrupa según intereses o rendimiento.  
    👉 El modelo descubre los grupos por sí solo.
    



> [!summary]  
> **Clustering** se usa cuando **no tenés etiquetas** y querés **descubrir grupos o patrones ocultos** dentro de los datos.

### 🧭 Cuándo usarlo:

- Cuando **no sabés cuántas categorías existen**.
    
- Cuando querés **segmentar o explorar** tus datos.
    
- Cuando necesitás **entender comportamientos o similitudes** entre elementos.
    

### 💡 Ejemplos:

- Agrupar clientes por hábitos de compra.
    
- Detectar comunidades en redes sociales.
    
- Encontrar patrones en datos médicos o biológicos.
    

👉 En resumen: **usás clustering para descubrir estructura** en los datos, **no para predecir etiquetas conocidas**.



---

## 🧩 Qué muestra la imagen

La imagen describe **las etapas clave del _Predictive Modeling_** (modelado predictivo), que es el proceso de **usar datos existentes para predecir resultados futuros**.

![[Pasted image 20251021132614.png]]

### 🔹 Elementos de la imagen:

1. **Defining the outcome**  
    → Definir qué querés predecir.  
    Ejemplo: ¿va a subir o bajar la venta el mes que viene?, ¿este paciente desarrollará la enfermedad?, ¿cuál será la temperatura mañana?
    
2. **Searching within the data for past occurrences**  
    → Buscar en los datos históricos ejemplos del mismo fenómeno.  
    Ejemplo: mirar ventas pasadas, registros médicos anteriores, temperaturas de días anteriores.  
    Esto sirve para encontrar **patrones que se repiten**.
    
3. **Imposing constraints on the data that can be used for training the model**  
    → Aplicar **restricciones o filtros** para mejorar el entrenamiento:
    
    - Eliminar valores atípicos (_outliers_).
        
    - Seleccionar variables relevantes.
        
    - Asegurar que los datos estén en el mismo formato y rango temporal.  
        En resumen: **limpiar y preparar los datos** para que el modelo aprenda bien.
        

---

## 📈 Cómo construir modelos predictivos a partir de datos temporales

> [!definition]  
> Los **datos temporales** (o series de tiempo) son aquellos que cambian a lo largo del tiempo: ventas por día, temperatura por hora, tráfico por minuto, etc.  
> El **modelado predictivo temporal** busca anticipar valores futuros en base a las tendencias pasadas.

### 🔹 Pasos principales:

1. **Definir el objetivo de predicción (outcome)**
    
    - Qué querés predecir: la venta del próximo mes, la demanda futura, la temperatura, etc.
        
2. **Recolectar y ordenar los datos en orden temporal**
    
    - Los datos deben tener una **marca de tiempo** (fecha, hora).
        
    - Ejemplo:
        
        |Fecha|Ventas|
        |---|---|
        |2024-01|100|
        |2024-02|120|
        |2024-03|130|
        
3. **Explorar patrones**
    
    - Identificar **tendencias**, **estacionalidades** (por ejemplo, subidas en verano) y **anomalías**.
        
4. **Preparar los datos (preprocesamiento)**
    
    - Eliminar datos faltantes.
        
    - Escalar variables.
        
    - Crear nuevas características: “mes”, “día de la semana”, “lag” (valor anterior), etc.
        
5. **Seleccionar un modelo apropiado**  
    Ejemplos de modelos predictivos temporales:
    
    - **ARIMA / SARIMA:** modelan tendencias y estacionalidad.
        
    - **Prophet (Meta):** fácil de usar para predicciones de negocio.
        
    - **LSTM / RNN:** redes neuronales especializadas en secuencias.
        
    - **Regresión con variables temporales:** simple y explicativa.
        
6. **Entrenar el modelo**
    
    - Se usa la parte histórica para que aprenda patrones.
        
    - Por ejemplo: entrenar con datos hasta 2024 y predecir 2025.
        
7. **Validar y ajustar**
    
    - Comparar las predicciones con datos reales.
        
    - Ajustar parámetros si hay errores altos.
        
8. **Predecir y monitorear**
    
    - Aplicar el modelo para predecir valores futuros.
        
    - Actualizarlo periódicamente con nuevos datos.
        

---

### 💡 Ejemplo simple:

Querés predecir la cantidad de pasajeros diarios en un aeropuerto.

- Datos históricos: 3 años de registros diarios.
    
- Detectás una tendencia creciente y picos en vacaciones.
    
- Usás un modelo **SARIMA** que captura tendencia + estacionalidad.
    
- El modelo predice cuántos pasajeros habrá el próximo mes.
    
