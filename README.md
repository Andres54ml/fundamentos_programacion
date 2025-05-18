# fundamentos_programacion

# Análisis de Series Temporales Económicas y Financieras: Caso Bancolombia ADR y Macroeconomía Colombiana

Este proyecto consiste en un análisis exploratorio y correlacional entre la serie histórica del precio de apertura del ADR de Bancolombia (CIB) y varias variables macroeconómicas de Colombia. El análisis incluye la descarga, limpieza, preparación, visualización y pruebas estadísticas para comprender las relaciones y comportamiento de estas series en el tiempo.

---

## Contenido del proyecto

El código realiza las siguientes etapas principales:

### 1. Descarga y Preparación Inicial de Datos

- **Datos financieros (ADR Bancolombia):**  
  Se utiliza la librería `yfinance` para descargar datos históricos del ADR Bancolombia (ticker `CIB`) desde mayo 2015 hasta mayo 2025.  
  Se selecciona únicamente la columna `Open` (precio de apertura diario) y se convierte el índice de fechas en una columna normal para facilitar la manipulación posterior.

- **Datos macroeconómicos:**  
  Se leen variables macroeconómicas almacenadas en un archivo Excel (`graficador_series.xlsx`) que contiene diferentes series temporales en formato textual.  
  Se convierte la columna de fecha en tipo datetime, asegurando que el formato día/mes/año sea interpretado correctamente. También se renombra esta columna a `Date` para estandarizar.

### 2. Unificación y Limpieza de Datos

- **Normalización de columnas y combinación:**  
  Se ajustan los nombres de columnas del DataFrame financiero para eliminar niveles (en caso de multiíndices) y luego se realiza una unión (`merge`) con el DataFrame macroeconómico usando la columna `Date` como clave.  
  Esto genera un DataFrame combinado que contiene el precio de apertura diario y las variables macroeconómicas para cada fecha.

- **Limpieza de valores faltantes:**  
  En ciertas columnas macroeconómicas, los valores faltantes o inconsistentes estaban marcados con guiones (`"-"`). Estos se reemplazan por `NaN` para que Pandas los reconozca como valores faltantes y facilite el análisis estadístico.

### 3. Análisis Univariado de Series Temporales

Para cada variable macroeconómica de interés, se realiza:

- **Conversión numérica robusta:**  
  Se normalizan formatos numéricos (puntos decimales, porcentajes, etc.) para convertir las series a tipos numéricos.

- **Estadísticas descriptivas:**  
  Se imprimen medidas básicas como media, desviación estándar, cuartiles, etc., para tener una primera impresión de la distribución de cada serie.

- **Visualización:**  
  - Serie temporal para observar tendencia y posibles patrones.  
  - Histograma para analizar la distribución de valores.  
  - Media móvil para suavizar la serie y destacar tendencias de mediano plazo.

- **Análisis de autocorrelación:**  
  Se realizan gráficos de autocorrelación (ACF) y autocorrelación parcial (PACF) para entender dependencias temporales en la serie.

- **Pruebas de estacionariedad:**  
  - **ADF (Augmented Dickey-Fuller):** prueba para detectar raíces unitarias y si la serie es estacionaria.  
  - **KPSS (Kwiatkowski-Phillips-Schmidt-Shin):** otra prueba complementaria para estacionariedad.

- **Descomposición estacional:**  
  Separación de la serie en componentes de tendencia, estacionalidad y residual para entender mejor su comportamiento.

### 4. Preparación para Análisis Bivariado

- Se alinean las series del precio diario (`Open_CIB`) con cada variable macroeconómica según su frecuencia (mensual o trimestral) usando reindexación con método `forward-fill`. Esto garantiza que cada observación tenga su correspondiente dato macroeconómico.

- Para las variables con frecuencia diaria (por ejemplo, la tasa de política monetaria), se busca la intersección de fechas disponibles y se crea un DataFrame conjunto.

- Se generan DataFrames independientes para cada par (`Open_CIB` vs variable macro), facilitando análisis específicos.

### 5. Análisis de Correlaciones y Visualización Conjunta

- Se calcula la correlación de Pearson para cada par de variables.  
- Según el valor y signo de la correlación, se clasifica la relación en:  
  - **Procíclica:** correlación positiva fuerte (mayor que un umbral).  
  - **Contracíclica:** correlación negativa fuerte (menor que el umbral negativo).  
  - **Acíclica:** correlación débil o cercana a cero.

- Se crean gráficos con doble eje y para visualizar simultáneamente ambas series, facilitando la interpretación visual de la relación entre ellas.

- Se presenta un resumen con las correlaciones y su clasificación para todas las parejas analizadas.

---

## Estructura del código

| Sección                         | Descripción                                                                                 |
|--------------------------------|---------------------------------------------------------------------------------------------|
| Descarga datos financieros      | Descarga histórico diario del ADR Bancolombia con `yfinance`.                              |
| Lectura y procesamiento Excel   | Carga y limpieza de variables macroeconómicas desde archivo Excel.                         |
| Unión y limpieza de datos       | Combina ambos DataFrames en uno solo, normaliza columnas y reemplaza valores faltantes.     |
| Análisis univariado             | Estadísticas descriptivas, pruebas de estacionariedad, descomposición y gráficos.           |
| Preparación para análisis bivar | Creación de DataFrames por pares para comparación directa entre precio y variables macro.   |
| Análisis correlacional          | Cálculo y clasificación de correlaciones, junto con visualización comparativa.              |

---
# Proyecto de Predicción de Series Económicas con RNN

Este repositorio contiene el código y la documentación para el preprocesamiento y la imputación de series de tiempo económicas, preparando los datos para su uso en un modelo de Red Neuronal Recurrente (RNN) para tareas de predicción.

## Imputación de Series Económicas

### Objetivo

El objetivo de esta sección es limpiar y rellenar (imputar) valores faltantes en una serie de variables económicas clave para garantizar su continuidad temporal antes de ser usadas en un modelo de predicción.

---

### Pasos realizados

1.  **Limpieza de datos:**
    * Se reemplazan guiones (–, —, -) por `NaN`.
    * Se reemplazan comas por puntos para manejar correctamente los valores decimales.
2.  **Conversión de datos:**
    * Se convierten las columnas relevantes a tipo `float`.
    * Se asegura que el índice del DataFrame sea de tipo `datetime` y esté ordenado.
3.  **Imputación de valores faltantes:**
    * **Interpolación temporal** (`interpolate(method='time')`): Aplicada a series con periodicidad mensual como M1 y tasa de desempleo.
    * **Forward-fill + backward-fill** (`fillna(method='ffill').fillna(method='bfill')`): Utilizado para variables trimestrales o más estables como PIB e inflación, asegurando que se llenen también los `NaN`s iniciales.
4.  **Verificación:**
    * Se imprime el número de valores nulos antes y después de imputar para confirmar el proceso.
    * Se muestran las primeras filas del DataFrame para comprobar visualmente la estructura y los datos imputados.

---

## Preprocesamiento para RNN

### Objetivo

Esta sección transforma los datos imputados en un formato adecuado para entrenar una red neuronal recurrente (RNN), utilizando secuencias de tiempo multivariadas como entrada y una variable económica específica como objetivo.

---

### Pasos realizados

1.  **Selección de columnas:**
    * Se definen las variables económicas que actuarán como características de entrada (`input_cols`).
    * Se especifica la variable objetivo (`target_col`) a predecir.
2.  **Escalado con MinMaxScaler:**
    * Todas las columnas seleccionadas (inputs y target) son escaladas al rango [0, 1] utilizando `sklearn.preprocessing.MinMaxScaler`. Esto es crucial para optimizar el entrenamiento de la red neuronal.
    * *(Nota: En un flujo de trabajo real, el escalador debe ser ajustado SOLO con los datos de entrenamiento para evitar data leakage).*
3.  **Separación de inputs y target escalados:**
    * Se dividen los datos escalados en dos arrays NumPy:
        * `training_set_scaled`: Contiene las características de entrada escaladas.
        * `y_data_scaled`: Contiene los valores de la variable objetivo escalada.
4.  **Creación de ventanas temporales (Windowing):**
    * Se construyen secuencias deslizantes de tamaño `window_size` (por ejemplo, 60 pasos de tiempo).
    * Cada secuencia es un array 2D (`window_size` x `n_variables`) que captura el historial reciente de las variables de entrada.
    * La etiqueta (`y`) para cada secuencia es el valor del target escalado en el paso de tiempo inmediatamente siguiente a la ventana.
5.  **Conversión a arrays NumPy finales:**
    * Las listas de secuencias (`X_train`) y de objetivos (`y_train`) se convierten a arrays NumPy para su uso directo en el entrenamiento de la RNN.

---

### Salida

Después de este proceso de preprocesamiento, se obtienen los siguientes arrays listos para ser usados como entrada en un modelo de aprendizaje secuencial (como una capa LSTM o GRU en Keras/TensorFlow o PyTorch):

* `X_train`: Array NumPy con forma `(n_muestras, window_size, n_variables)`, donde:
    * `n_muestras`: es el número total de secuencias creadas.
    * `window_size`: es el tamaño de cada ventana temporal.
    * `n_variables`: es el número de columnas de input seleccionadas.
* `y_train`: Array NumPy con forma `(n_muestras,)` (si se predice una sola variable), conteniendo los valores objetivo escalados correspondientes a cada secuencia en `X_train`.

  
## Dependencias

Para ejecutar el proyecto necesitas tener instaladas las siguientes librerías:

- `pandas`
- `numpy`
- `yfinance`
- `matplotlib`
- `statsmodels`
- `scipy`

Puedes instalar todas con:

```bash
pip install pandas numpy yfinance matplotlib statsmodels scipy





