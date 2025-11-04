# Diferencia entre `None` y `NaN` en Python y Pandas

En Python y Pandas, `None` y `NaN` son valores que representan ausencia de datos, pero tienen diferencias importantes:

## `None` (Python)

- Es un objeto singleton de Python (tipo `NoneType`)
- Representa la ausencia de valor o un valor nulo
- Es comparable usando el operador `is`: `if x is None`
- No es numérico y no permite operaciones matemáticas

```python
x = None
print(type(x))  # <class 'NoneType'>
print(x is None)  # True
```

## `NaN` (Pandas/NumPy)

- Significa "Not a Number" (No es un número)
- Es un valor flotante especial (`float`) de NumPy/Pandas
- Representa valores numéricos indefinidos o no representables
- No es comparable usando `==`: `NaN == NaN` es `False`
- Requiere funciones especiales como `pd.isna()`, `np.isnan()`
- Permite operaciones matemáticas (que resultan en más `NaN`)

```python
import pandas as pd
import numpy as np

x = pd.NA  # Pandas NA
y = np.nan  # NumPy NaN

print(type(np.nan))  # <class 'float'>
print(np.isnan(np.nan))  # True
print(np.nan == np.nan)  # False
```

## Principales diferencias

1. **Tipo de dato**:
   - `None` es un objeto Python de tipo `NoneType`
   - `NaN` es un valor float especial de NumPy/Pandas

2. **Uso típico**:
   - `None` para valores ausentes en Python general
   - `NaN` para valores ausentes en datos numéricos/análisis de datos

3. **Operaciones matemáticas**:
   - `None` no permite operaciones matemáticas
   - `NaN` permite operaciones (pero propaga `NaN`)

4. **Comparación**:
   - `None` puede compararse con `is`
   - `NaN` requiere funciones como `pd.isna()` o `np.isnan()`

5. **En DataFrames**:
   - Pandas generalmente convierte `None` a `NaN` en operaciones

## Ejemplo práctico

```python
import pandas as pd
import numpy as np

# Crear un DataFrame con None y NaN
df = pd.DataFrame({
    'A': [1, None, 3, np.nan],
    'B': [np.nan, 5, None, 7]
})

print(df)
print("\nDetección de valores faltantes:")
print(df.isna())  # Ambos None y NaN son detectados como ausentes
```

Cuando trabajas con Pandas, `None` típicamente se convierte a `NaN` internamente para cálculos numéricos.