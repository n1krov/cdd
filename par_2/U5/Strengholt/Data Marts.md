
Los **Data Marts** son subconjuntos o versiones más pequeñas y enfocadas del Data Warehouse central.

![Imagen de Data Marts deriving from a central Data Warehouse](https://encrypted-tbn0.gstatic.com/licensed-image?q=tbn:ANd9GcSlU9ySdaUX_YHP-SaKzC6FKCArrZM6jkJ9vtARG7BDaYzKPGmwrU9fij1fHeL7FySqdvYbWxr86aiSURp576Y4oW7ij3DpMYH-zORd3N-y2wXz3ig)

## ¿Qué son los Data Marts?

Un Data Mart es un **almacén de datos temático y específico**, diseñado para satisfacer las necesidades de **análisis de un solo departamento o área de negocio** (como Ventas, Marketing, o Finanzas).

Piensa en el Data Warehouse central como una gran biblioteca de toda la empresa. El Data Mart sería una **sala de lectura especializada** dentro de esa biblioteca, que solo contiene libros (datos) relevantes para un tema específico.

### Características Clave

- **Alcance Limitado:** Contienen solo los datos necesarios para un departamento o función específica. Esto los hace **más pequeños, rápidos** y **más fáciles de usar** que el Data Warehouse central.
    
- **Orientación al Usuario Final:** Están altamente **desnormalizados** (usan el Esquema de Estrella o Dimensional de Kimball) y optimizados para el uso directo por analistas y herramientas de Business Intelligence (BI).
    
- **Fuente de Datos:**
    
    - **Metodología Inmon:** Se derivan y construyen **a partir** del Data Warehouse central.
        
    - **Metodología Kimball:** Se construyen **primero**, y la colección integrada de todos los Data Marts conforma el Data Warehouse.
        

En resumen, los Data Marts son la **capa de presentación** final de la arquitectura, permitiendo a los usuarios acceder rápidamente a la información que necesitan sin tener que navegar por todo el almacén de datos de la organización.
