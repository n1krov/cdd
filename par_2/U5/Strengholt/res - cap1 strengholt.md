---
title: "Building Medallion Architectures - Designing with Delta Lake and Spark"
subtitle: "Resumen del capítulo 1"
author: "Piethein Strengholt"
date: \today
geometry: margin=1.6in
colorlinks: true
header-includes:
  - \usepackage{fvextra}
  - \DefineVerbatimEnvironment{Highlighting}{Verbatim}{breaklines,commandchars=\\\{\}}
  - \usepackage{graphicx}
	# - \setkeys{Gin}{width=0.95\textwidth}
  - \usepackage{float}
  - \floatplacement{figure}{H}
  - \usepackage{tabularx}
  - \usepackage{array}
  - \renewcommand{\arraystretch}{1.5}
  
  # neutralizamos tightlist y ajustamos espaciado de listas
  - \let\tightlist\relax
  - \usepackage{enumitem}
  - \setlist[itemize,enumerate]{itemsep=1\baselineskip, topsep=1\baselineskip}
  
  # estilo rosado pálido con fuente aclarada
  - \usepackage[most]{tcolorbox}
  - |
    \newtcolorbox{noteBox}{
      colback=red!5!white,
      colframe=red!30!black,
      coltext=black!70,        % color del texto menos saturado
      arc=4pt,
      left=6pt, right=6pt, top=4pt, bottom=4pt,
      boxrule=0.5pt,
      breakable
    }
  - |
    \renewenvironment{quote}{\begin{noteBox}}{\end{noteBox}}

  # --- Caption sin numeración para figuras ---
  - \usepackage{caption}
  - \captionsetup[figure]{labelformat=empty}
---

# Capítulo 1. La Evolución de la Arquitectura de Datos

Crear una arquitectura de datos robusta es uno de los aspectos más desafiantes de la gestión de datos. El proceso abarca desde la recolección hasta la transformación, distribución y consumo final, variando según la gobernanza, herramientas, perfil de riesgo y madurez de la organización.

A pesar de estas diferencias, el autor propone una metáfora fundamental para estructurar cualquier estrategia de datos: el **Diseño de Arquitectura de Tres Capas**.

![Figura 1-1: El diseño de arquitectura de tres capas](f11%203.png)

Este diseño consta de:

### 1. 🧑‍💻 Capa 1: Proveedores de Datos (**Data Providers**)

- **¿Qué es?** Son los **puntos de origen** de todos los datos.
    
- **En la práctica:** Es donde está la información bruta: tus bases de datos operacionales, los archivos de texto, los datos que vienen de sensores, los registros de aplicaciones, etc.
    
- **Desafío:** Vienen en **muchos formatos y ubicaciones diferentes** (la "mezcla de tipos de datos, formatos y ubicaciones dispersas").

### Capa 2: Capa de Distribución (**Distribution Layer**)

- **¿Qué es?** Es el **sistema de transporte y procesamiento**. Es la plataforma donde los datos se mueven, se limpian, se transforman y se preparan.
    
- **En la práctica:** Aquí es donde se usan herramientas complejas (como **Apache Spark**) para integrar y procesar grandes volúmenes de datos crudos, convirtiéndolos en algo útil.
    
- **Desafío:** Es la parte **más compleja** porque hay muchísimas tecnologías diferentes para hacer esta integración (el "Modern Data Stack").

### 3. 📊 Capa 3: Consumidores de Datos (**Data Consumers**)

- **¿Qué es?** Son los **usuarios finales** y las **aplicaciones** que necesitan la información lista para tomar decisiones.
    
- **En la práctica:** Son los paneles de control (**BI**), los modelos de **Machine Learning (ML)** para hacer predicciones, y los sistemas de **Inteligencia Artificial (AI)** que automatizan acciones.


### Capa Transversal: 🛡️ Metadatos y Gobernanza

- **¿Qué es?** Es la **supervisión y las reglas** que controlan todas las capas.
    
- **En la práctica:** Se asegura de que los datos sean **seguros**, que sean de **calidad** (no tengan errores) y que todo el mundo sepa **qué significa** cada dato (metadatos).
    

### El Desafío Actual

El texto menciona el **"Modern Data Stack"** como el problema clave hoy en día.

- **Problema:** Este "Stack" está hecho de **muchas herramientas individuales** (para almacenamiento, procesamiento, etc.) que no siempre se hablan bien entre sí. Esto hace que sea muy **difícil y costoso** para las empresas crear una plataforma de distribución funcional.
    
- **Solución:** La **Arquitectura Medallion** (que usa tecnologías como Spark y Delta Lake) surge como una forma de **estandarizar** esta Capa de Distribución, simplificando el proceso y mejorando la calidad de los datos. En resumen: **Los datos nacen (Proveedores), se preparan (Distribución) y se usan (Consumidores), todo bajo la vigilancia de la Gobernanza.**

## ¿Qué es una Arquitectura Medallion?

Es un patrón de diseño de datos utilizado para organizar lógicamente los datos, generalmente en un *Lakehouse*. Su objetivo es mejorar incremental y progresivamente la estructura y calidad de los datos a medida que fluyen a través de tres capas principales.

Es una forma de **organizar el flujo de datos** en tu sistema, dividiéndolo en **tres niveles de calidad y refinamiento** (como si fueran medallas) que se construyen incrementalmente.

El objetivo es **mejorar progresivamente los datos** a medida que pasan de una capa a la siguiente, asegurando que el producto final sea de **alta calidad y fácil de usar**.

| **Capa**   | **Función Clave**                                                                                                                               | **Medalla**   |
| ---------- | ----------------------------------------------------------------------------------------------------------------------------------------------- | ------------- |
| **Bronze** | Es la **Zona de Datos Crudos (Raw Data)**. Los datos se almacenan **tal cual** como vienen de la fuente.                                        | 🟠 **Bronce** |
| **Silver** | Es la **Zona de Limpieza y Estandarización**. Los datos se **limpian**, se **validan** y se **estructuran** (se les da un formato consistente). | ⚪ **Plata**   |
| **Gold**   | Es la **Zona de Datos de Negocio**. Los datos se **agregan**, se **resumen** y se **optimizan** para la analítica y los reportes finales.       | 🟡 **Oro**    |

![Figura 1-2: Una arquitectura Medallion, que organiza los datos en tres capas, mejorando la estructura y calidad de los datos a medida que avanza a través de las capas](f12%202.png)

Aunque las etiquetas son intuitivas, muchas empresas fallan al modelar sus datos dentro de estas capas, confundiendo objetivos y estrategias de gobernanza. Para entender cómo aplicar esto correctamente, es vital comprender primero la historia de las arquitecturas de datos.

## Una Breve Historia de la Arquitectura de Data Warehouse

En los años 90, el **Data Warehousing** surgió para crear una "versión única de la verdad" integrando datos en una colección unificada.

![Figura 1-3: Arquitectura típica de un data warehouse](f13%202.png)


El Data Warehouse (DW) surgió para crear un **"Versión Única de la Verdad"** (Single Source of Truth), integrando datos de varias fuentes para el análisis. La arquitectura típica se compone de cuatro etapas en un flujo de izquierda a derecha.

#### La Cadena de Flujo del DW:

1. **Sistemas OLTP** (Fuentes)
    
2. **Staging Area** (Preparación)
    
3. **Data Warehouse** (Almacén Central)
    
4. **Data Marts** (Presentación)
    

### 📌 Diferencia Clave: OLTP vs. OLAP

La principal diferencia en la arquitectura de datos es el propósito: transacciones vs. análisis.

|**Característica**|**OLTP (Online Transaction Processing)**|**OLAP (Online Analytical Processing)**|
|---|---|---|
|**Propósito**|Operaciones diarias, transacciones (Ej: Compra en línea, retiro bancario).|Análisis de tendencias, toma de decisiones (Ej: Reportes de ventas, predicciones).|
|**Diseño**|**Normalizado** (3NF). Reduce la redundancia, optimiza escrituras.|**Desnormalizado** (Esquema de Estrella). Optimiza lecturas complejas (_joins_).|
|**Operación**|Cargas de trabajo predecibles: Leer, actualizar, borrar un registro.|Consultas complejas que acceden a grandes volúmenes de datos.|
|**Propiedades**|Requiere **ACID** (Atomicidad, Consistencia, Aislamiento, Durabilidad).|No requiere ACID en la misma medida. Prioriza velocidad y agregación.|

> [!note] Problema del OLTP para Analítica
> 
> Los sistemas OLTP están diseñados para escribir rápido. Extraer datos para análisis profundo (que requiere muchos joins y datos históricos) los sobrecarga, y suelen perder historia al borrar datos antiguos.

### 🗄️ Normalización y Desnormalización

- **Normalización:** Técnica de diseño de DB para **reducir la redundancia** y mejorar la integridad de los datos. Es eficiente para las escrituras (insertar/actualizar).
    
    - **Ejemplo:** Tener una tabla `Clientes` separada de una tabla `Pedidos`, conectadas por un ID.
        
- **Desnormalización:** **Introduce redundancia intencional** (duplica datos) para mejorar el rendimiento de las consultas (lecturas), evitando costosos _joins_. Es la técnica principal en Data Warehousing (OLAP).
    
    - **Ejemplo:** En la tabla `Pedidos` se copia directamente el `Nombre_Cliente` y la `Dirección` para no tener que hacer _join_ con la tabla `Clientes`.
        

### 🏭 El Área de Staging (Staging Area)

Es la zona de "aterrizaje" de los datos crudos antes de ser transformados y cargados al Data Warehouse (la etapa **E**xtracción de **E**TL).

- **Función Clave:**
    
    - **Aísla** las fuentes (OLTP) del proceso de transformación.
        
    - Sirve como **respaldo** de los datos extraídos (copias históricas).
        
- **Contenido:** Generalmente bases de datos relacionales temporales o almacenamiento de archivos de bajo costo.
    


### 🗺️ Metodologías de Diseño de Data Warehouse

Existen dos enfoques principales para construir un Data Warehouse, definidos por la jerarquía de construcción.

#### 1. Metodología Inmon (Top-Down)

- **Creador:** Bill Inmon.
    
- **Enfoque:** De **Arriba hacia Abajo** (Top-Down). Primero se construye el gran almacén central, luego los subconjuntos para los usuarios.
    
- **Flujo:**
    
    1. Cargar datos a un **Enterprise Data Warehouse (EDW)** central.
        
    2. El EDW usa un modelo **normalizado (3NF)**.
        
    3. Crear **Data Marts** departamentales _derivados_ del EDW, utilizando modelos desnormalizados (esquema de estrella) para reportes.
        

> [!warning] Desventaja de Inmon
> 
> Requiere un doble esfuerzo de ETL: primero para llevar los datos crudos al EDW normalizado, y luego para llevarlos del EDW a los Data Marts desnormalizados.


![Figura 1-4: El enfoque Inmon; un diseño de arriba hacia abajo donde primero se construye un almacén de datos centralizado y luego se crean data marts a partir de este almacén central](f14%201.png)

#### 2. Metodología Kimball (Bottom-Up)

- **Creador:** Ralph Kimball.
    
- **Enfoque:** De **Abajo hacia Arriba** (Bottom-Up). Se construyen Data Marts que luego se integran para formar el DW.
    
- **Modelo:** Utiliza el **Modelo Dimensional (Esquema de Estrella)** como estándar de integración.
    
    - **Tablas de Hechos:** Contienen las métricas (lo que se mide: ventas, clics).
        
    - **Tablas de Dimensiones:** Contienen el contexto (quién, qué, dónde, cuándo: cliente, producto, tiempo).
        
![Figura 1-5: La metodología Kimball; un enfoque de abajo hacia arriba para construir el data warehouse](f15%201.png)

##### Conceptos Clave de Kimball

- **Dimensiones Conformadas (Conformed Dimensions):** Tablas de dimensiones (ej. `Tiempo`, `Cliente`) que son **idénticas** o subconjuntos estandarizados entre diferentes Data Marts. Esto permite que los reportes de Ventas y Marketing puedan "hablar el mismo idioma".
    
- **SCDs (Slowly Changing Dimensions):** Estrategias para registrar los **cambios históricos** en las tablas de dimensiones (ej. cuando un cliente cambia de dirección).
    

##### Tabla: Tipos de SCD

|**Tipo**|**Nombre**|**Estrategia**|**Pérdida de Historia**|**Tamaño de Tabla**|
|---|---|---|---|---|
|**SCD1**|Sobrescribir (Overwrite)|Actualiza el registro existente con el nuevo valor.|**Sí** (Pierde la historia anterior).|Pequeño.|
|**SCD2**|Añadir nueva fila (Add row)|Crea un **nuevo registro** para el cambio, manteniendo el viejo. Usa fechas de vigencia.|**No** (Mantiene historia completa).|Grande (Aumenta con cada cambio).|
|**SCD3**|Añadir nueva columna|Agrega una columna para el valor anterior (ej. `Dirección_Anterior`).|**Sí** (Solo guarda una versión anterior limitada).|Moderado.|

> [!example] Ejemplo SCD2 (Añadir nueva fila)
> 
> Un cliente vive en Madrid hasta 2024-01-01.
> 
> |**ID_Cliente_Surrogada**|**Nombre**|**Ciudad**|**Fecha_Inicio_Vigencia**|**Fecha_Fin_Vigencia**|
> |---|---|---|---|---|
> |100|Juan|Madrid|2020-01-01|2024-01-01|
> |101|Juan|Barcelona|2024-01-02|NULO|

### 🛑 Conclusiones y Limitaciones del DW Tradicional

Los Data Warehouses tradicionales son muy efectivos para datos estructurados y consultas **OLAP** rápidas. Sin embargo, tienen limitaciones importantes en la era moderna:

- **Escalabilidad Costosa:** Escalar la capacidad (verticalmente) es muy caro y tiene límites físicos.
    
- **No Aptos para Datos Modernos:** No manejan bien los datos **no estructurados** (imágenes, video) ni los semi-estructurados (JSON, logs), y tampoco están optimizados para cargas de trabajo de **Machine Learning (ML)**.


## Una Breve Historia de los Data Lakes

Los Data Lakes surgieron a mediados de los 2000 como solución a las limitaciones del Warehouse, impulsados por el software open source (**Hadoop**) y hardware commodity (barato).

![Figura 1-6: Arquitectura típica de data lake con copias crudas de datos](f16%201.png)

Aquí tienes la explicación simplificada de los componentes clave que dieron origen a los primeros **Data Lakes** y cómo evolucionaron.

### La Primera Generación de Data Lakes (Hadoop)

El ecosistema **Hadoop** fue la base de los Data Lakes originales. Permitió almacenar y procesar **grandes volúmenes de datos crudos** a bajo costo.

##### 1. HDFS (Hadoop Distributed File System)

- **¿Qué es?** Es el **sistema de almacenamiento distribuido**.
    
- **Funcionamiento Sencillo:** Toma un archivo gigante, lo parte en **pequeños bloques** (ej. 128 MB) y guarda copias de esos bloques en varias máquinas baratas (**escala horizontal**). Si una máquina falla, el dato sigue seguro.
    
- **Problema Principal:**
    
    - **Archivos Pequeños:** Funciona mal si tienes millones de archivos muy pequeños (unos pocos KB), porque el sistema que rastrea los metadatos (_NameNode_) se satura y se vuelve muy lento.
        
    - **Inmutabilidad:** Los datos son casi **inmutables** (solo puedes añadir al final, no puedes actualizar o borrar fácilmente un dato en medio del archivo). Esto es un dolor de cabeza para tareas como llevar el historial de clientes (**SCDs**).
        

##### 2. MapReduce

- **¿Qué es?** El **modelo de programación** para procesar los datos almacenados en HDFS.
    
- **Funcionamiento Sencillo:** Divide la tarea en tres etapas: **Map** (divide el problema), **Shuffle** (intercambia datos entre las máquinas), y **Reduce** (combina los resultados).
    
- **Problema Principal:** Es **muy lento** porque en cada etapa tiene que leer y escribir datos en el **disco duro** (E/S intensa).
    

##### 3. Apache Hive

- **¿Qué es?** Un **traductor de SQL** para Hadoop.
    
- **Funcionamiento Sencillo:** Te permite escribir consultas **SQL** (_HiveQL_) y Hive las traduce automáticamente a los lentos trabajos **MapReduce**.
    
- **Concepto Clave (Schema-on-read):** Los datos se almacenan sin un esquema estricto, y el esquema se aplica **solo cuando los lees**. Esto te da flexibilidad, pero si no modelas bien los datos, el análisis será caótico y lento.
    
- **Metastore:** Es el **índice central** que dice dónde están guardadas las tablas y qué columnas tienen. Esto sigue siendo vital hoy.
    


#### 🚀 El Proyecto Spark (La Evolución)

**Apache Spark** nació para resolver la principal limitación de Hadoop: la lentitud de MapReduce.

- **Diferencia Clave:** Utiliza el procesamiento **en memoria (RAM)**. En lugar de leer y escribir en el disco en cada paso (como hacía MapReduce), Spark lee los datos una vez, hace todo el procesamiento en la RAM (que es **mucho más rápida**), y solo escribe el resultado final al disco.
    
- **Resultado:** Es **hasta 100 veces más rápido** que MapReduce.
    
- **Limitación:** Necesita un tiempo inicial (_cold start_) para cargar los datos en memoria antes de poder empezar a procesar a alta velocidad.
    

#### 💡 Aprendizajes de los Data Lakes (El Problema)

Los Data Lakes lograron almacenar todo tipo de datos de forma barata, pero no resolvieron el problema de **hacer que esos datos fueran valiosos**.

- **Desafíos:**
    
    - **Latencia:** Las consultas no eran lo suficientemente rápidas.
        
    - **Falta de Transaccionalidad (ACID):** No podían garantizar la integridad de los datos ni soportar actualizaciones fáciles como un Data Warehouse.
        
    - **Complejidad:** La solución terminó siendo tener el **Data Lake** para almacenar lo crudo y el **Data Warehouse** para el consumo final, lo que es costoso y difícil de mantener (el "patrón de dos niveles").


## Una Breve Historia de la Arquitectura Lakehouse

La arquitectura **Lakehouse** combina lo mejor de ambos mundos: la escalabilidad y flexibilidad del Data Lake (almacenamiento en objetos en la nube barato) con la confiabilidad y rendimiento del Data Warehouse (transacciones ACID).

![Figura 1-8: Arquitectura típica de lakehouse, con una representación de las capas Bronce, Plata y Oro incluidas](f18%201.png)

### Fundadores de Spark y Databricks
Los creadores de Spark fundaron **Databricks** en 2013. A diferencia de sus competidores (Cloudera/Hortonworks que se enfocaron en on-premise), Databricks apostó por la **Nube** y la separación de cómputo y almacenamiento.

### Evolución Tecnológica
*   **Almacenamiento de Objetos:** Reemplazo de HDFS por S3 (AWS), ADLS (Azure), GCS (Google). Más barato y escala a petabytes.
*   **Spark en la Nube:** Clusters elásticos que se crean y destruyen según demanda (Kubernetes), sin estar atados a un cluster físico gigante.

### Emergencia de Formatos de Tabla Abiertos (Open Table Formats)
Para solucionar la falta de transacciones ACID y la gestión de metadatos en los Data Lakes, surgieron nuevos formatos:

1.  **Apache Hudi (2017, Uber):** Enfocado en upserts eficientes.
2.  **Apache Iceberg (2018, Netflix):** Enfocado en corrección y rendimiento en grandes escalas.
3.  **Delta Lake (2019, Databricks):** Trajo transacciones ACID, manejo escalable de metadatos, unificación de batch/streaming y "Time Travel". Usa archivos **Parquet** más una capa de metadatos transaccionales.

#### Cómo funciona Delta Lake
Usa un **Transaction Log (DeltaLog)**.

*   Cada cambio (insert, update, delete) se registra como un commit atómico en archivos JSON secuenciales (`000000.json`).
*   Permite **Time Travel**: Consultar cómo estaba la tabla en el pasado.
*   Usa archivos Parquet para los datos físicos.

![Figura 1-7: Ejemplo de cómo Delta Lake estructura sus datos y registro de transacciones](f17%201.png)

### Proveedores de Lakehouse
El mercado ha adoptado el concepto:

*   **Databricks:** Pionero, fuerte integración Spark + Delta Lake.
*   **Microsoft Fabric / Synapse / HDInsight:** Integran Spark y Delta.
*   **Snowflake, AWS, Google:** También han adoptado terminología y funcionalidades Lakehouse.
*   **Cloudera, Dremio, Starburst:** Ofrecen plataformas sobre estos formatos abiertos.

## Arquitectura Medallion y sus Desafíos Prácticos
Databricks y Microsoft promueven la Arquitectura Medallion como la mejor práctica para organizar datos en este entorno.
Sin embargo, el libro señala un problema crítico: **Falta de orientación práctica**.

*   Aunque los términos Bronce/Plata/Oro suenan bien, no hay consenso universal sobre qué transformación exacta ocurre en cada capa.
*   La confusión sobre el modelado de datos persiste. ¿Dónde aplico reglas de negocio? ¿Dónde hago *joins*?

### Conclusión del Capítulo
Hemos evolucionado de almacenes rígidos on-premise a sistemas distribuidos y flexibles en la nube.

*   **Data Warehouse:** Gran control, gran rendimiento, difícil escalado, caro.
*   **Data Lake:** Gran escalado, barato, difícil gestión y calidad (pantano de datos).
*   **Lakehouse:** Intenta unificar ambos mediante formatos de tabla modernos (Delta, Iceberg) y motores rápidos (Spark).

El desafío actual no es solo tecnológico, sino de **diseño y modelado**. La velocidad de entrega exigida por el negocio presiona a los equipos a saltarse el modelado (a veces bajo la excusa de "Data Mesh" mal implementado), creando silos y deuda técnica. La Arquitectura Medallion ofrece un marco, pero requiere una ejecución disciplinada que se detallará en los próximos capítulos (2 y 3) del libro.
