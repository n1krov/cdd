# 📊 Capítulo 9 – Visualización de muchas distribuciones a la vez

Cuando tenemos **una sola distribución** (ejemplo: notas de un examen o altura de una población), basta con un histograma o un boxplot.

👉 Pero en la práctica **casi siempre queremos comparar varias distribuciones al mismo tiempo**.  
Ejemplo: temperaturas de cada mes, ingresos por distintas regiones, tiempos de espera en diferentes sucursales.

Este capítulo muestra **qué técnicas son más adecuadas** y **por qué algunas representaciones engañan o pierden información**.

---

## 🔑 Variables en juego

- **Variable respuesta**: la que analizamos (ej. temperatura, ingreso, tiempo de espera).
    
- **Variable de agrupamiento**: divide los datos en categorías (ej. meses, regiones, sucursales).
    

En este tipo de visualizaciones, una dimensión del gráfico corresponde a la variable respuesta, y la otra a los grupos.

## 🔑 Conceptos básicos

- **Variable respuesta**: es la variable que queremos analizar.  
    👉 Ejemplo: temperatura.
    
- **Variable de agrupamiento**: es la que divide los datos en subconjuntos.  
    👉 Ejemplo: meses del año.
    

En estas gráficas, un eje muestra la **variable respuesta** y el otro eje la **variable de agrupamiento**.

---

## 🚫 Método inicial: puntos con barras de error

![[Pasted image 20250916144708.png]]

Un enfoque muy usado es mostrar:

- La **media o mediana** de cada grupo como un punto.
- La **variabilidad** con barras de error (error bars).

🔴 **Problemas:**

1. **Se pierde información** → un punto y dos barras no cuentan toda la historia de la distribución.
2. **Ambigüedad** → no queda claro si es media o mediana.
3. **Confusión en las barras** → las barras pueden representar distintas cosas (desvío estándar, error estándar, intervalo de confianza).
4. **Asimetría mal representada** → barras simétricas no reflejan bien distribuciones sesgadas.

👉 Conclusión: este método es poco informativo y puede ser engañoso.

---

## ✅ Métodos más efectivos

## 📦 Boxplots (diagramas de caja)

El **boxplot** es uno de los métodos más usados para mostrar distribuciones.  
Fue inventado por John Tukey en los años 70, y se hizo popular porque era fácil de dibujar **a mano** (en esa época no había software estadístico moderno).

![[Pasted image 20250916144858.png]]

### ¿Cómo funciona?

- Se toma la distribución de datos y se divide en **cuartiles**:
    
    - 25% más bajo (Q1),
        
    - 25% intermedio inferior,
        
    - 25% intermedio superior,
        
    - 25% más alto (Q3).
        
- La **caja** representa el rango entre Q1 y Q3 (el 50% central de los datos).
    
- La **línea dentro de la caja** marca la **mediana** (el valor “del medio”).
    
- Los **bigotes** se extienden desde la caja hasta los valores máximos y mínimos, siempre que estén dentro de un rango razonable (1.5 veces el tamaño de la caja).
    
- Si hay puntos mucho más lejos, se dibujan aparte como **outliers**.
    

### ¿Por qué es útil?

Porque con una simple caja podemos ver:

- la tendencia central (mediana),
    
- la dispersión (tamaño de la caja),
    
- si hay valores extremos,
    
- y si la distribución está sesgada (la mediana se va hacia arriba o abajo).
    

### Limitación

El boxplot **no muestra la forma de la distribución**.  
Ejemplo: si los datos tienen **dos picos** (bimodales), el boxplot los “aplana” en una sola caja. Te dice dónde están los cuartiles, pero no te muestra si hay montañas dobles dentro de los datos.

---

## 🎻 Violin plots

El **violin plot** es una evolución moderna del boxplot.  
La idea es combinar la **simplicidad del boxplot** con una representación de la **densidad** (qué valores son más comunes).
![[Pasted image 20250916145108.png]]
![[Pasted image 20250916145041.png]]

### ¿Cómo funciona?

- Se estima la densidad de los datos (algo así como un histograma suavizado).
- Esa densidad se dibuja de manera simétrica en forma de violín.
- Así, donde el violín es más ancho → hay más datos concentrados.
- Donde es angosto → hay pocos datos.

### ¿Por qué es mejor que un boxplot?

Porque **sí muestra la forma de la distribución**.

- Si hay un solo pico, se ve un violín con un centro marcado.
- Si hay **dos picos (bimodalidad)**, el violín tendrá “dos pancitas”, algo que el boxplot jamás mostraría.    

### Precaución

El violín funciona bien cuando hay **muchos datos**.  
Si los datos son pocos, la curva de densidad puede “inventar” una forma suave donde en realidad no hay suficiente información. Es decir, puede dar la impresión de que hay continuidad o picos que no existen en los datos reales.


### 3. ⚪ Strip charts (gráfico de puntos crudos)
![[Pasted image 20250916145213.png]]


El **strip chart** es la forma más directa y simple de mostrar una distribución:  
👉 **dibujar todos los puntos, tal cual están en los datos**.

### ¿Cómo funciona?

- Cada observación se representa con un puntito.
    
- Se colocan en el gráfico alineados según su valor.
    
- Si estamos comparando varios grupos, cada grupo tiene su propia columna de puntos.
    

### Ventaja

- No hay resúmenes ni promedios: ves **los datos reales**.
    
- Perfecto para datasets pequeños → como ver “toda la evidencia” sin procesar.
    

### Problema

- Si hay muchos puntos, se enciman y forman una mancha.  
    Resultado: ya no se distingue dónde están las concentraciones de datos.
    

### Solución: Jittering

Para evitar el encimado, se usa una técnica llamada **jittering**:

- Se agrega un pequeño “ruido” en la posición horizontal de cada punto.
    
- Es decir, los puntos se separan un poquito al azar, para que no queden uno encima de otro.
    
- Esto no cambia la información, solo mejora la legibilidad.
    

👉 Así, podemos ver mejor cuántos datos hay en cada zona de valores.
---

### 4. **Sina plots**

![[Pasted image 20250916145353.png]]


El **sina plot** es como un paso intermedio entre el strip chart y el violin plot.

### ¿Cómo funciona?

- Cada observación sigue siendo un punto individual.
    
- Pero a diferencia del jittering, los puntos no se dispersan al azar.
    
- En cambio, se dispersan **proporcionalmente a la densidad de datos**:
    
    - Donde hay más datos, los puntos se expanden más en horizontal.
        
    - Donde hay menos, se agrupan más cerca del centro.
        

### Ventaja

- Se ven **los puntos reales** (como en el strip chart).
    
- Y al mismo tiempo se aprecia **la forma general de la distribución** (como en el violin plot).
    

### Por qué es útil

El sina plot combina lo mejor de ambos mundos:

- Transparencia → cada dato es visible.
    
- Contexto → la nube de puntos forma naturalmente la “figura” de la distribución.
---

## 🌄 Ridgeline plots

Aquí llegamos al tipo de gráfico más llamativo del capítulo.  
El ridgeline plot es una técnica visual muy usada cuando hay **muchas distribuciones** que comparar, especialmente cuando cambian con el tiempo.

### ¿Cómo funciona?

- La **variable respuesta** (ej. temperatura) se pone en el eje horizontal.
    
- Cada grupo (ej. mes) se pone en el eje vertical.
    
- En vez de hacer un boxplot o violín para cada grupo, se dibuja su **curva de densidad**.
    
- Las curvas se apilan una encima de la otra → parecen **cordilleras de montañas** (de ahí el nombre “ridgeline”).
    

### Ventaja principal

Es mucho más fácil ver **cómo cambia la forma de las distribuciones** entre grupos.

Ejemplos:

1. **Temperaturas por mes** → la curva de noviembre muestra claramente dos picos (uno frío y otro templado).  
    → Ese detalle se veía poco en el violín, pero en el ridgeline es obvio.
    
2. **Duración de películas (1913–2005)** → con casi 100 distribuciones, se entiende perfecto cómo en los años 20 había películas de todas las duraciones posibles, pero después de 1960 todas convergieron en ~90 minutos.  
    → Pese a la cantidad de datos, la visualización sigue siendo clara.
    
3. **Patrones de voto en el Congreso de EE.UU.** → dos ridgelines, uno para Demócratas y otro para Republicanos, comparados año a año.  
    → Se ve cómo las distribuciones se separan con el tiempo (polarización política).
    

### Por qué son tan poderosos

- Porque **escalan muy bien** → incluso con decenas de grupos, siguen siendo legibles.
    
- Porque hacen evidente la **bimodalidad o cambios de tendencia**.
    
- Porque muestran la “historia completa” de los datos, no solo promedios.
    

### Precaución

- Si en lugar de densidades se usan histogramas, el resultado suele ser **confuso**.
    
    - Las barras de cada grupo se alinean en los mismos puntos del eje x.
        
    - Esto hace que el gráfico se vea recargado y difícil de leer.  
        👉 Mejor usar densidades suavizadas, no histogramas.
        

### Ejemplos:

- Temperaturas mes a mes.

![[Pasted image 20250916145827.png]]

- Duración de películas a lo largo del siglo XX → muestran cómo se estandarizó en ~90 min después de 1960.
![[Pasted image 20250916145928.png]]

- Patrones de voto en el Congreso de EE.UU. → comparando partidos políticos a lo largo de los años.
![[Pasted image 20250916150030.png]]

⚠️ Si se usan histogramas en lugar de densidades, suelen ser confusos porque las barras se alinean y sobrecargan la visualización.



## 📝 Resumen práctico

- **Boxplots** → buenos para comparaciones rápidas.
    
- **Violin plots** → muestran la forma y posibles bimodalidades.
    
- **Strip charts / Sina plots** → útiles con pocos datos o cuando queremos mostrar cada punto.
    
- **Ridgeline plots** → ideales para:
    
    - series temporales,
        
    - grandes cantidades de grupos,
        
    - análisis de tendencias y cambios de forma en las distribuciones.
        


# 🧠 Clave del capítulo

El autor insiste en que **la elección del gráfico depende de lo que queremos mostrar**:

- No basta con resumir → hay que **visualizar la forma de la distribución**.
    
- Cuantos más grupos tengamos, más importante es elegir un gráfico que **escalé bien** (ej. ridgelines).
    
- La visualización debe evitar confusión: mostrar **tanto la tendencia general** como la **variabilidad real** de los datos.


----

## Analisis del notebook


### 📝 Explicación del Notebook (Capítulo 9 – Muchas distribuciones)

El dataset `tips` de Seaborn tiene cuentas de restaurante (`total_bill`), propinas (`tip`), día de la semana, etc. Lo usamos para mostrar distintos tipos de gráficos de distribuciones.

La idea es **hacer bien y mal algunas visualizaciones** para entender qué aporta cada enfoque.

---

## 1) ❌ Incorrecto (engaña)

```python
sns.violinplot(..., y="total_bill")
sns.stripplot(..., y="total_bill")
medians_tip = tips_df.groupby("day")["tip"].median()
```

👉 Aquí se grafica la distribución de **total_bill** con un violin plot + puntos individuales.  
Pero encima se dibuja la **mediana de _tip_** (propinas), con la etiqueta “Mediana total_bill”.

🔴 Problema: estamos mezclando **dos variables distintas** en el mismo eje sin aclararlo.

- El violín muestra una cosa (total_bill).
    
- El punto rojo representa otra (tip).
    
- La etiqueta dice otra cosa más (mal nombrada).
    

Esto conecta con lo que dice Wilke en el capítulo 9: **si el gráfico es ambiguo o engañoso, el lector saca conclusiones falsas**.  
Aquí alguien podría pensar que el punto rojo es la mediana de la cuenta, pero en realidad es la mediana de la propina.

✅ **Lección**: siempre que se superponen estadísticas, deben corresponder a la misma variable o estar bien explicadas en la leyenda.

---

## 2) ⚠️ Malo (oculta información)

```python
means = tips_df.groupby("day")["total_bill"].mean()
plt.bar(x, means)
```

👉 Aquí se muestran las **medias** de la cuenta por día en un gráfico de barras.

El problema es que **sólo se ve la media**, pero no se muestra nada sobre:

- dispersión (qué tan concentrados están los datos),
    
- asimetría (si hay sesgo),
    
- outliers (valores extremos),
    
- tamaño de muestra.
    

Wilke en el capítulo 9 insiste en esto: **resumir con un solo número y sin contexto es peligroso**.

- Dos días podrían tener la misma media, pero distribuciones completamente distintas (uno con datos concentrados, otro con datos muy dispersos).
    
- El lector se engaña pensando que los días son “iguales”.
    

✅ **Lección**: si queremos comparar medias, debemos añadir barras de error (intervalos de confianza o desviación estándar), o mejor aún, usar boxplots/violines para mostrar toda la distribución.

---

## 3) 😵 Feo pero correcto

```python
sns.violinplot(..., y="total_bill")
sns.stripplot(..., y="total_bill")
medians = tips_df.groupby("day")["total_bill"].median()
```

👉 Aquí los datos están **correctamente representados**:

- Violines → muestran forma de la distribución.
    
- Puntos → muestran observaciones individuales.
    
- Medianas → calculadas correctamente de `total_bill`.
    

El problema no es el contenido, sino la **estética**:

- Colores chillones.
    
- Fondo amarillo.
    
- Letras difíciles de leer.
    
- Marcadores demasiado grandes.
    

Esto conecta con lo que dice Wilke en varios capítulos: **un gráfico correcto también debe ser legible y no cansar la vista**.  
Un gráfico feo puede hacer que el lector pierda interés o malinterprete simplemente porque se distrae con los colores.

✅ **Lección**: además de ser correcto, un gráfico debe ser **claro, legible y estéticamente consistente**.

---

## 4) ✅ Correcto (buena práctica)

```python
sns.violinplot(..., y="total_bill")
sns.stripplot(..., y="total_bill")
medians = tips_df.groupby("day")["total_bill"].median()
```

👉 Este es el gráfico **bien hecho**:

- Se usa un **sina plot** (violín + puntos dispersados).
    
- Se superpone la **mediana** como punto rojo.
    
- Se mantiene un diseño claro y simple (colores neutros, buen contraste).
    

### ¿Por qué es bueno?

1. **Muestra toda la distribución** → forma, densidad, asimetría.
    
2. **Muestra observaciones individuales** → no hay riesgo de inventar formas inexistentes.
    
3. **Muestra un resumen robusto** (mediana) que no se ve afectado por outliers.
    
4. **Claridad y precisión** → no hay ambigüedad, todo está etiquetado y corresponde a la misma variable.
    

Esto es lo que Wilke describe como el punto ideal:

- Un gráfico debe **mostrar la historia completa** de los datos,
    
- y al mismo tiempo dar un **resumen fácil de interpretar**.
    

---

## 5) 📊 Complemento numérico

```python
stats_robust = tips_df.groupby("day")["total_bill"].agg(
    mediana="median",
    q1=lambda x: x.quantile(0.25),
    q3=lambda x: x.quantile(0.75),
    mad=lambda x: robust.mad(x)
)
```

👉 Además del gráfico, se calculan **estadísticas robustas**:

- Mediana → tendencia central resistente a outliers.
    
- Q1 y Q3 → cuartiles (para ver la caja de un boxplot).
    
- IQR = Q3 - Q1 → rango intercuartílico (dispersión).
    
- MAD (median absolute deviation) → otra medida robusta de variabilidad.
    

Esto conecta directamente con los **boxplots** del capítulo 9:

- Se representan exactamente estas estadísticas.
    
- Permiten comparar varias distribuciones de forma resumida, pero sin perder lo esencial (centro, dispersión, outliers).
    

---

# 📌 Resumen final (relación con el capítulo 9)

- **Gráfico 1 (Incorrecto)** → muestra el peligro de etiquetas engañosas → conecta con la advertencia de Wilke sobre malas prácticas (pérdida de confianza).
    
- **Gráfico 2 (Malo)** → sólo muestra medias, oculta la variabilidad → conecta con el problema de “puntos + barras de error” que Wilke desaconseja.
    
- **Gráfico 3 (Feo pero correcto)** → los datos están bien, pero la estética importa → Wilke enfatiza la importancia de claridad visual.
    
- **Gráfico 4 (Correcto)** → ejemplo ideal de buena práctica → similar a un sina plot o violin plot bien diseñado.
    
- **Estadísticas finales** → lo que sustenta los boxplots y permite cuantificar lo que los gráficos muestran.
    
