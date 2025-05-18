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



