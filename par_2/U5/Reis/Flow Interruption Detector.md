
Quiero que actúes como un asistente especializado en mejorar y embellecer mis apuntes de **Ciencia de Datos** en Obsidian.
### Reglas de formato:

- Usa **Markdown** y todas las herramientas nativas de Obsidian:
    - Encabezados jerárquicos (#, ##, ###…)
    - Negritas, cursivas, tachado
    - Listas ordenadas y no ordenadas
    - Tablas comparativas (ejemplo: métodos de pandas, funciones de NumPy, tipos de gráficos de Matplotlib/Seaborn).
    - Callouts (`> [!info]`, `> [!tip]`, `> [!warning]`, `> [!example]`, etc.) para resaltar definiciones, tips de código y errores comunes.
    - Diagramas con **Mermaid** (diagramas de flujo para pipelines de datos, ETL, modelos de ML).
    - Bloques de código con resaltado (Python, SQL, Bash).
    - Separadores `---` para estructurar módulos o secciones.

### Reglas de estilo:

- Embellecé y organizá mis notas para que sean **claras, fáciles de leer y visualmente atractivas**.
    
- Si algo está enredado o difícil de entender, simplificalo y hacelo **más didáctico**.
    
- Agregá **ejemplos prácticos** (snippets de pandas, NumPy, limpieza de datos, gráficos).
    
- Respetá los **enlaces, referencias y datasets** que yo incluya. No borres ni inventes datasets/enlaces.
    
- Podés usar:
    
    - **Tablas** para comparar funciones o métodos.
        
    - **Diagramas de flujo (Mermaid)** para mostrar procesos de análisis de datos o ETL.
        
    - **Checklists** (`- [ ]`) para pasos de un análisis.
        
- El resultado final debe ser un apunte EN ESPAÑOL **técnico, claro y útil para estudiar Ciencia de Datos**.

Cuando te pase un texto (código, notas del profe o de libros), transformalo siguiendo estas reglas.

aqui va el texto:

---

Pattern: Flow Interruption Detector
The first serious data-related issue is dataset unavailability. This
issue will have a strong impact on your systems because without any
data, your data processing job will not run, leading to data
unavailability in its downstream dependencies.
Problem
One of your streaming jobs is synchronizing data to an object store.
The synchronized dataset is the data source for many batch jobs
managed by different teams. It ran great for seven months until one
day, it processed the input records without writing them to the
object store.
Because the job didn’t fail, you didn’t notice the issue. You only
realized something was wrong when one of your consumers
complained about the lack of new data to process. Instead of relying
on consumer feedback, which is not good for your reputation, you
want to introduce a new observability mechanism to detect this data
unavailability scenario.
Solution
To capture any data unavailability errors, and as a result, increase
trust in your data, you can rely on the Flow Interruption Detector
pattern.
The implementation of the pattern will vary depending on the
technical context and processing mode. Let’s start with the stream
processing introduced in the problem statement. Basically, you can
have two different data ingestion modes here:
Continuous data delivery
In this mode, you expect to get at least one record every unit
of time, like a minute or a second. In that context, the Flow
Interruption Detector consists of triggering an alert whenever
there are no new data points registered for the specified unit
of time, like no data coming in for one minute.
Irregular data delivery
Here, you expect to see some delivery interruptions that have
nothing to do with errors. For example, you might assume that
no data will come in for five consecutive minutes. The
pattern’s implementation in that context consists of analyzing
time windows instead of data points and raising an alert
whenever the period without the data is longer than the
accepted no-data window duration. Since the data flow is
irregular, using the continuous data delivery assumption would
result in many false-positive alarms that might lead to alarm
fatigue.1
Figure 10-1 compares the two approaches. As you’ll notice, the only
difference between them is the data evaluation period. Continuous
data delivery analyzes a specific unit of time (a minute in the
example), while for irregular data delivery it monitors multiple
consecutive points in time.
![[Pasted image 20251125093927.png]]
Figure 10-1. Flow interruption detection for continuously arriving and irregularly arriving data
However, data flow interruption can also occur in batch pipelines and
data-at-rest databases. Spotting unavailability here consists of
analyzing the data freshness of the metadata, data, or storage layer:
Metadata layer
This layer stores all additional information about the observed
table, such as creation time and last modification time. A flow
might be interrupted when the modification time hasn’t been
changed according to the configured threshold. For example, a
table with new data ingested hourly could trigger an alert
whenever no changes are observed for more than one hour.
Data layer
Generally, interactions with the metadata layer will be less
expensive in most scenarios due to more direct access to the
information and thus the lack of data processing needs.
Unfortunately, your data store may not have the metadata
layer available or the update information may be missing. In
that situation, you may need to enrich the table with the
modification time column to detect a flow interruption if the
last update passed the configured threshold. If adding this
column is not possible, you can count the number of rows in
each evaluation time period and compare the results to see
whether there is new data. For example, in our hourly job, if
the count doesn’t change in two consecutive hours, it’ll be a
sign of flow interruption. This count-based approach may also
require some extra storage to preserve the count statistics for
past runs.Storage layer
The last flow interruption detection strategy is based on the
storage layer. Typically, you could use it with any file format,
including raw JSON files or more advanced table file formats.
The implementation here consists of monitoring the time when
the last file was written in a storage space and raising an
interruption alert whenever there are no updates within the
expected threshold.
Consequences
Flow interruption detection may look simple, but unfortunately, the
implementation hides some traps such as the threshold, metadata,
and false positives.
Threshold
Finding the perfect threshold for both per-minute and per-window
implementations is not easy. Expecting at least one record per
minute, as in our previous example, is an easy choice but may not
be realistic. If you expect to process hundreds of events or more per
minute, you will need to choose a different number.
Relying on the volume observed in the past may be a tempting way
to define the threshold. It’s often used as the solution to this
threshold-finding problem, but it also has a gotcha. From time to
time, it can generate false positives, for example, whenever a
marketing operation generates more activity than usual.
Metadata
The solution based on the metadata is cheap but may not be
perfect. First, this metadata layer with the last modification time or
the number of rows may simply not be available for your database.
Second, even if the layer is there, the modification can include not
only data operations but also metadata changes, such as schema
evolution, which obviously doesn’t add any new records. You must
be careful when evaluating it for the purpose of the Flow
Interruption Detector pattern.
False positives for storage
If you rely on the storage layer for flow interruption detection,
beware of all housekeeping operations, such as compaction. This
operation does indeed create new files, but it doesn’t produce new
datasets. Instead, compaction simply merges existing data blocks.
From the storage’s perspective, there is activity, but it will not count
as flow continuity since the dataset remains unchanged.