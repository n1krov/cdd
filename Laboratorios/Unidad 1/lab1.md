quiere una expo de 5 min por equipo con el objetivo de dar una clase a los compañeros
entregar
- 1 notebook con coneptos claves que se puedan identificar
- 1 notebook con ejercicios (elegir un dataset de Kaggle)
- Puede o no usar slides o con el notebook
- sube nota si un equipo encuentre un bug en el material y se lo reporte como issue


## 🔹 1. Introducción y primer vistazo

👉 **¿Por qué empiezan mirando el dataset crudo (`head()`, `info()`, gráficos iniciales)?**  
Porque antes de limpiar tenés que **diagnosticar**. Es como un médico: primero ve los síntomas.

- `head()` → muestra ejemplos de filas para ver qué datos trae.
    
- `info()` → revisa cuántos nulos tiene y qué tipo de dato hay en cada columna.
    
- Histograma de edad → visualizan qué tan grave es el problema de los valores faltantes.
    

**Si no hacés esto**: podrías limpiar a ciegas, sin saber qué columnas realmente lo necesitan.

---

## 🔹 2. Manejo de valores faltantes

👉 **¿Por qué rellenan algunos y eliminan otros?**

- **Edad (`age`) → rellenan con la mediana**.
    
    - Porque es una variable numérica continua.
        
    - La mediana es más robusta: no se ve afectada por outliers como una edad de 150 años.
        
- **Puerto de embarque (`embarked`) → rellenan con la moda**.
    
    - Porque es categórica.
	   - Una variable categórica es aquella cuyos valores indican una cualidad o categoría, y no un valor numérico medible.

    - Si 70% de los pasajeros salió de Southampton, lo lógico es asumir que un valor faltante era también de ahí.
        
- **`deck` → la eliminan.**
    
    - Tiene demasiados nulos (casi todo vacío). Rellenarla inventando valores metería ruido.
        
    - Es más seguro descartarla.
        
- **`embark_town` → la eliminan.**
    
    - Aporta lo mismo que `embarked`, es redundante.
        

**Si no hacés esto**: los algoritmos de Machine Learning no soportan NaNs, te tiran error. Además, columnas con demasiado ruido confunden más que ayudan.

---

## 🔹 3. Transformación de datos

👉 **¿Por qué convierten texto en números (`get_dummies`)?**  
Porque la compu **no entiende palabras**, necesita variables numéricas.  
Ejemplo:

- `sex` → pasa de {male, female} a {0,1}.
    
- `embarked` → pasa de {C, Q, S} a 3 columnas binarias (one-hot encoding).
    

**Si no hacés esto**: no podrías entrenar un modelo predictivo porque las variables categóricas quedarían como strings y no sirven para operaciones matemáticas.

---

## 🔹 4. Pipeline con `.pipe()`

👉 **¿Por qué arman funciones y las encadenan con `.pipe()`?**  
Porque quieren que el proceso sea:

- **Reproducible** → si mañana vuelven a cargar el Titanic o un dataset parecido, con el pipeline pueden repetir exactamente la misma limpieza.
    
- **Ordenado** → cada paso está encapsulado en una función con un nombre que explica qué hace.
    
- **Escalable** → si más adelante agregan otro paso (ej. normalización de `fare`), solo meten una nueva función en la cadena.
    

**Si no hacés esto**: el notebook se llena de pasos sueltos, es difícil volver a correr todo desde cero.

---

## 🔹 5. Conclusión y visualización

👉 **¿Por qué muestran un gráfico final (barplot de supervivencia por sexo)?**  
Porque ahora el dataset ya está **listo para análisis serio**:

- No tiene nulos.
    
- Las variables están en formato numérico.
    
- Solo quedaron las columnas relevantes.
    

La visualización es un **storytelling**: conecta la limpieza con un insight real → _las mujeres tenían más chances de sobrevivir_.

**Si no hacés esto**: quedás en “hicimos limpieza porque sí”, sin mostrar para qué sirve. Siempre conviene terminar con un resultado tangible.

---

✅ En resumen:

- **Explorar primero** → saber qué problemas hay.
    
- **Tratar nulos inteligentemente** → algunos se imputan, otros se eliminan.
    
- **Transformar categóricas** → volverlas numéricas.
    
- **Pipeline** → mantenerlo limpio y repetible.
    
- **Visualización final** → demostrar que valió la pena.
    


