---
title: ""
author: ""
date: ""
geometry: margin=1.6in
colorlinks: true
header-includes:
  - \usepackage{fvextra}
  - \DefineVerbatimEnvironment{Highlighting}{Verbatim}{breaklines,commandchars=\\\{\}}
  - \usepackage{graphicx}
  - \setkeys{Gin}{width=0.75\textwidth}
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

# Yo, pobre humano pensando...

*«¿Entonces, podemos entender que Strengholt propone que gracias al DDS podemos generar valor a partir de los datos mediante el BI y el MLOPs, siendo el BI una técnica para que las personas no técnicas (como lo son muchas veces los gerentes o CEOs) puedan ver reportes y el MLOPs la manera de crear y aplicar modelos de ML a la empresa?*

*... ¿Y para qué nos sirven en este contexto los modelos de ML?»*

# Respuesta de mi amigo "JeremÍAs Frutal"

Podríamos decir que has formulado el **resumen ejecutivo perfecto** de la filosofía del autor para el lado del consumidor.

Vamos a validar y refinar un poco cada uno de tus puntos para que queden cristalinos, y luego responderemos a tu última pregunta, que es la más importante.

---

## Validación y Refinamiento de tu Resumen

**1. "Strengholt propone que gracias al DDS podemos generar valor a partir de los datos mediante el BI y el MLOps..."**

*   **Correcto.** El **DDS (Domain Data Store)** no es el valor en sí mismo, es el **entorno controlado**, la "cocina" que el dominio consumidor construye para sí mismo. Es el lugar arquitectónico donde se llevan a cabo las actividades de creación de valor. Y las dos grandes categorías de "recetas" para crear valor son, efectivamente, el BI y la Analítica Avanzada (gestionada a través de MLOps).

**2. "...siendo el BI una técnica para que las personas no técnicas (como lo son muchas veces los gerentes o CEOs) puedan ver reportes..."**

*   **Correcto, y para ser aún más precisos...** El BI no es *solo* para que vean reportes estáticos. Es para **empoderarlos**. Gracias a herramientas como las **Capas Semánticas**, un gerente puede explorar los datos y responder a sus propias preguntas sin saber SQL. El BI es el conjunto de herramientas y procesos que permiten a la organización **entender el rendimiento pasado y presente** de una manera accesible. Su objetivo es generar *insights* para que los **humanos** tomen mejores decisiones.

**3. "...y el MLOps la manera de crear y aplicar modelos de ML a la empresa?"**

*   **Correcto, y para ser aún más precisos...** MLOps es la **disciplina industrializada** para crear, aplicar y, sobre todo, **mantener** modelos de ML en la empresa. Un científico de datos puede "crear" un modelo en su portátil. **MLOps** es lo que permite que ese modelo se reentrene automáticamente cada noche, se despliegue sin errores, atienda a millones de usuarios y se monitoree para que no empiece a dar predicciones erróneas. Es el paso de un proceso artesanal a una **línea de ensamblaje automatizada y confiable** para la inteligencia artificial.

Tu resumen es excelente porque has entendido que el **DDS es el lugar**, y **BI y MLOps son las actividades** que se realizan en ese lugar.

---

## ¿Y para qué nos sirve en este contexto los modelos de ML?

Esta es la pregunta del millón. Si el BI ya nos permite entender el negocio, ¿por qué necesitamos la complejidad de los modelos de ML y MLOps?

Porque el BI mira hacia el pasado, mientras que los modelos de ML **miran hacia el futuro y actúan a una escala que los humanos no pueden**. En el contexto de un negocio, los modelos de ML sirven principalmente para tres propósitos transformadores:

### 1. Predecir el Futuro (Para Tomar Acciones Proactivas)

Los modelos de ML pueden identificar patrones en los datos históricos para predecir lo que es más probable que ocurra. Esto permite a la empresa dejar de reaccionar y empezar a anticiparse.

*   **Ejemplo de Churn**: En lugar de esperar a que un cliente se dé de baja, un modelo de ML predice **qué clientes tienen un alto riesgo de hacerlo en el próximo mes**. Con esta información, el equipo de marketing puede lanzar una campaña de retención *específicamente* para ellos.
*   **Ejemplo de Demanda**: En lugar de adivinar cuánto stock de un producto se necesita, un modelo predice **la demanda para la próxima semana en cada tienda**, optimizando el inventario y evitando tanto la falta de stock como el exceso.

### 2. Automatizar Decisiones a Escala (Para Ser Más Eficientes y Personalizados)

Hay decisiones que deben tomarse millones de veces al día, de forma instantánea y personalizada para cada usuario. Un humano no puede hacer esto. Un modelo de ML sí.

*   **Ejemplo de Recomendación (Netflix/Amazon)**: Cuando entras a Netflix, un modelo de ML decide en milisegundos **qué 10 películas mostrarte a ti**, de entre miles de opciones, basándose en tu historial. Multiplica eso por 200 millones de usuarios.
*   **Ejemplo de Detección de Fraude**: Cuando usas tu tarjeta de crédito, un modelo de ML decide en tiempo real si **esa transacción es fraudulenta o legítima**. Protege tu dinero y el del banco, 24/7.
*   **Ejemplo de Precios Dinámicos (Uber/Aerolíneas)**: Un modelo ajusta el precio de un viaje o un billete de avión en tiempo real basándose en la demanda, el tráfico, la hora del día, etc.

### 3. Extraer Insights Ocultos de Datos Complejos (Para Descubrir Oportunidades)

Los modelos de ML pueden encontrar patrones y relaciones en datos masivos y no estructurados que serían invisibles para un analista humano.

*   **Ejemplo de Segmentación de Clientes**: En lugar de los segmentos tradicionales (edad, género), un modelo puede analizar el comportamiento de compra y descubrir **"micro-segmentos"** como "compradores nocturnos de snacks saludables" o "buscadores de ofertas de fin de semana". Esto permite un marketing mucho más preciso.
*   **Ejemplo de Análisis de Sentimiento**: Un modelo puede leer miles de reseñas de productos o tweets cada día y **cuantificar el sentimiento** de los clientes sobre una nueva característica, dando un feedback casi instantáneo al equipo de producto.

**En resumen**, dentro de tu DDS, el **BI te da el volante y el mapa** para que entiendas por dónde has venido y dónde estás. Los **modelos de ML te dan el piloto automático y un motor de predicción del futuro**, permitiéndote llegar a tu destino de forma más rápida, eficiente y automatizada.
