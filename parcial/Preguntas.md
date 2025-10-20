
## 🧠 Banco de Preguntas — _Strengholt (Cap. 1)_

**Tema:** _The Journey to Becoming Data-Driven_  
**Objetivo:** verificar comprensión del texto, no opinión personal.

---

### 🔸 Tipo V/F (Verdadero / Falso) — con fundamento

1. **P:** Strengholt afirma que la transformación hacia una organización data-driven es principalmente tecnológica.  
    **R:** **Falso.**  
    **Fundamento:** Insiste en que el cambio es **cultural y organizacional** (personas, procesos y tecnología), no solo de herramientas.
    
2. **P:** El autor sostiene que el cambio hacia una cultura data-driven requiere modificar la forma en que las personas, los procesos y la tecnología se alinean con los datos.  
    **R:** **Verdadero.**  
    **Fundamento:** Plantea una **realineación integral** (people–process–technology) para gestionar datos a escala.
    
3. **P:** Según Strengholt, los modelos centralizados de datos seguirán siendo suficientes para escalar en el futuro.  
    **R:** **Falso.**  
    **Fundamento:** Explica que el **centralismo** no escala por complejidad, acoplamiento y cuellos de botella.
    
4. **P:** La descentralización es descrita por el autor como una tendencia inevitable para lograr escalabilidad.  
    **R:** **Verdadero.**  
    **Fundamento:** “**Decentralization is not a desired state, but the inevitable future of data**”.
    
5. **P:** El concepto de _data fabric_ enfatiza la federación de responsabilidades humanas por sobre la capa tecnológica.  
    **R:** **Falso.**  
    **Fundamento:** _Data fabric_ se centra **más en la capa tecnológica** (metadata unificada, acceso/integ. end-to-end).
    
6. **P:** El _data mesh_ se enfoca más en la tecnología que en la organización y cultura.  
    **R:** **Falso.**  
    **Fundamento:** _Data mesh_ **prioriza lo humano/organizacional** (federar responsabilidades, dominios).
    
7. **P:** Para el autor, ser data-driven implica gestionar los datos como un producto dentro de la organización.  
    **R:** **Verdadero.**  
    **Fundamento:** “**Manage data as a product**” es una idea central (propiedad, calidad, documentación, acceso).
    
8. **P:** Strengholt considera que la gestión de datos debe ser vista como un activo que se controla a lo largo de su ciclo de vida.  
    **R:** **Verdadero.**  
    **Fundamento:** Retoma DAMA-DMBOK: **planificar, controlar y proteger** el valor del dato **en todo su ciclo**.
    
9. **P:** Las arquitecturas tradicionales son adecuadas para manejar el crecimiento exponencial de los datos actuales.  
    **R:** **Falso.**  
    **Fundamento:** Critica DW/lakes **monolíticos** por su dificultad para **escalar y desacoplar**.
    
10. **P:** La transformación hacia la analítica distribuida se logra manteniendo un modelo monolítico de operación.  
    **R:** **Falso.**  
    **Fundamento:** Propone **federación** y **desacoplo**; el monolito es el **bottleneck**.
    

---

### 🔸 Tipo CITA (respuestas breves y literales)

11. **P:** Cite la definición de _data management_ según la **DAMA-DMBOK** que menciona el autor.  
    **R:** “**The development, execution, and supervision of plans, policies, programs, and practices that deliver, control, protect, and enhance the value of data and information assets throughout their life cycles.**”
    
12. **P:** Mencione los **11 functional areas of data management** listadas por Strengholt.  
    **R:** Data Governance; Data Architecture; Data Modeling & Design; Data Storage & Operations; Data Security; Data Integration & Interoperability; Document & Content Management; Reference & Master Data Management; Data Warehousing & BI; Metadata Management; Data Quality Management.
    
13. **P:** ¿Qué dos metodologías emergentes presenta el capítulo?  
    **R:** **Data mesh** y **data fabric**.
    
14. **P:** Según el autor, ¿cuál es la relación entre _metadata_ e _interoperability_?  
    **R:** La **metadata está dispersa** y requiere **integración/interoperabilidad** para **entender, integrar y asegurar** los datos a escala.
    
15. **P:** ¿Qué frase usa sobre la descentralización?  
    **R:** “**Decentralization is not a desired state, but the inevitable future of data.**”
    

---

### 🔸 Tipo EXPLICACIÓN CONCEPTUAL

16. **P:** “La descentralización no es un estado deseado, sino un resultado inevitable”. Explique.  
    **R:** No se descentraliza por moda: el **volumen/variedad/velocidad** obligan a **federar responsabilidades** para escalar sin cuellos de botella.
    
17. **P:** ¿Por qué _data warehouse_ y _data lake_ no escalan bien en entornos distribuidos?  
    **R:** Al ser **repositorios centrales**, generan **acoplamiento**, **latencia**, colas de cambio y **dependencias cruzadas** que frenan la evolución.
    
18. **P:** _Data proliferation_ vs. _data intensiveness_.  
    **R:** **Proliferation:** copias del mismo dato por toda la org (origen y calidad difusos). **Intensiveness:** **muchas lecturas** (reentrenos, features) que fuerzan **duplicaciones/preprocesos**.
    
19. **P:** Rol de _data governance_ en DAMA.  
    **R:** Proveer **autoridad y control** (políticas, propiedad, cumplimiento) que enmarcan al resto de dominios.
    
20. **P:** ¿Qué es “managing data as a product”?  
    **R:** Cada **dominio** publica datasets con **dueño**, **SLOs de calidad**, **documentación**, **interfaces claras** y **autonomía** para consumo seguro.
    
21. **P:** ¿Cómo impacta la “use case diversity”?  
    **R:** Fragmenta el panorama: **cada caso pide features distintos**, aumenta **copias/transformaciones**, complica **control/alineación**.
    
22. **P:** ¿Por qué los _centralized operating models_ no funcionan con _self-serve_?  
    **R:** El **autoservicio** requiere **autonomía** y **ciclos rápidos**; un equipo central **no escala** para atender a todos.
    
23. **P:** Transformación digital y presión regulatoria.  
    **R:** Más **datos personales** y **distribución** ⇒ mayor riesgo/impacto ⇒ **leyes** (GDPR/CCPA, etc.) y **controles** más estrictos.
    
24. **P:** Problema de la “single version of the truth”.  
    **R:** Cada **aplicación/dominio** tiene **contexto semántico** propio; **unificar** puede **borrar matices** y crear **ambigüedades**.
    
25. **P:** ¿Qué implica pasar de monolítica a federada?  
    **R:** **Dividir y agrupar responsabilidades** por dominios, con **estándares comunes** y **alineación central** (pero ejecución local).
    

---

### 🔸 Tipo DIFERENCIAS / COMPARACIONES

26. **P:** _Data mesh_ vs. _data fabric_.  
    **R:** **Mesh:** foco **organizacional/humano**, federar dominios. **Fabric:** foco **tecnológico**, **metadata unificada** y capa de acceso/integ. end-to-end.
    
27. **P:** _Data integration_ vs. _data interoperability_.  
    **R:** **Integration:** **mover/combinar** datos en una vista. **Interoperability:** **comunicarse/compartir** sin conocer detalles internos.
    
28. **P:** _Operational_ vs. _analytical systems_.  
    **R:** **Operational:** **transacciones** y procesos en línea. **Analytical:** **histórico/agregado** para **insights/decisiones**.
    
29. **P:** _Data warehouse_ vs. _data lake_.  
    **R:** **DW:** datos **limpios/estructurados** para **reporting**. **Lake:** datos **crudos/variados** para **exploración/ML**.
    
30. **P:** _Centralized_ vs. _federated_ data management.  
    **R:** **Centralized:** control único, **cuello de botella**. **Federated:** **autonomía** con **estándares** y **alineación central**.
    
31. **P:** _Data-driven_ vs. intuición.  
    **R:** **Data-driven:** decisiones con **evidencia**; **intuición:** experiencia/percepción sin prueba objetiva.
    
32. **P:** _Top-down_ vs. _domain-driven_.  
    **R:** **Top-down:** diseño central prescriptivo. **Domain-driven:** límites por **dominios** y **responsabilidad local**.
    
33. **P:** _Metadata management_ vs. _Data quality management_.  
    **R:** **Metadata:** **describe/contextualiza** datos. **Quality:** asegura **exactitud, integridad, consistencia**.
    

---

### 🔸 Tipo APLICACIÓN / EJEMPLO

34. **P:** Ejemplo de “big ball of mud” por centralización.  
    **R:** DW con **capas/vistas/ETL** ad-hoc de años; cambios en una tabla **rompen** múltiples dependencias; nadie entiende el grafo.
    
35. **P:** Ejemplo real de _data proliferation_.  
    **R:** Marketing, Ventas y Finanzas **copian** la base de clientes y la transforman distinto; **tres verdades** incompatibles.
    
36. **P:** Caso ideal para _data mesh_.  
    **R:** Multinacional por países/unidades, cada dominio **publica** sus datos con **contratos/estándares** globales.
    
37. **P:** Cuando un _data warehouse_ es ventajoso vs. _data lake_.  
    **R:** **Reportes regulatorios/financieros** que exigen **consistencia y control**.
    
38. **P:** Mala metadata obstaculiza interoperabilidad.  
    **R:** Un campo “status” sin diccionario común: cada equipo lo interpreta distinto ⇒ **errores** en integraciones.
    
39. **P:** Falta de _data governance_ y decisiones.  
    **R:** Cada área define KPI “churn” distinto ⇒ **decisiones** contradictorias.
    
40. **P:** Ejemplo de _data monetization_.  
    **R:** Vender **datasets agregados/anónimos** de comportamiento a partners (cumpliendo privacidad).
    

---

### 🔸 Tipo CAUSA – EFECTO

41. **P:** Factores tech que cuestionan la centralización.  
    **R:** **Volumen/variedad/velocidad** crecientes, **monolitos** costosos de evolucionar, **nuevos patrones** (tiempo real/ML).
    
42. **P:** ¿Por qué el cloud aumenta la fragmentación?  
    **R:** Se **separan** cómputo/almacenamiento, **múltiples regiones/servicios**, **SaaS/MLaaS** ⇒ **datos distribuidos**.
    
43. **P:** ¿Cómo complican _DevOps_ y _microservices_?  
    **R:** **Descomponen** apps y **dispersan** datos (más fuentes, **replicas/sync**, **consistencia** y **linaje** complejos).
    
44. **P:** ¿Por qué privacidad/seguridad son prioridad?  
    **R:** Más **datos personales** y **brechas**; **regulaciones** más duras (GDPR/CCPA); necesidad de **trazabilidad**.
    
45. **P:** Efecto de la colaboración interorganizacional.  
    **R:** Exige **APIs**, **estándares** y **arquitecturas** que **compartan/integ** datos entre **ecosistemas**.
    

---

### 🔸 Tipo INTEGRACIÓN / SÍNTESIS

46. **P:** Ideas clave de una organización realmente _data-driven_.  
    **R:** **Datos como producto/activo**, **gobierno sólido**, **dominios federados**, **estándares comunes**, y **decisiones basadas en evidencia**.
    
47. **P:** Objetivo del capítulo.  
    **R:** Mostrar **por qué** volverse **data-driven** es **inevitable**, y **cómo** rediseñar **personas/procesos/tecnología** y **arquitecturas** para lograrlo.
    
48. **P:** ¿Por qué el futuro del _data management_ es inevitablemente descentralizado?  
    **R:** Por la **escala** y **complejidad** actuales: solo **federando** responsabilidades y **desacoplando** se sostiene el crecimiento.
    
49. **P:** Interrelación personas–procesos–tecnología.  
    **R:** **Personas** definen/usan datos; **procesos** norman propiedad, calidad y acceso; **tecnología** habilita **escalado/seguridad/automatización**.
    
50. **P:** Tres principios para definir una _data strategy_.  
    **R:** (1) **Tratar los datos como producto**; (2) **Federar responsabilidades** con **estándares y gobierno**; (3) **Alinear** estrategia/cultura/arquitectura para **decidir con evidencia**.
    
