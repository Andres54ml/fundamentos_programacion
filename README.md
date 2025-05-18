# fundamentos_programacion

# Análisis y Visualización de Series Temporales Económicas y Financieras

Este proyecto realiza la descarga, limpieza, análisis y visualización de datos financieros y macroeconómicos, enfocado en la serie histórica del ADR de Bancolombia (CIB) y varias variables macroeconómicas clave de Colombia.

---

## Descripción general

El flujo general del análisis consiste en:

1. **Descarga de datos financieros**
   - Se obtiene el histórico de precios del ADR Bancolombia (`CIB`) con `yfinance`, tomando la columna de apertura diaria.

2. **Lectura de datos macroeconómicos**
   - Se cargan series económicas desde un archivo Excel, con fechas convertidas correctamente a formato datetime.

3. **Preparación y combinación de datos**
   - Se ajustan columnas y se unifican los DataFrames por fecha para combinar precios y variables macroeconómicas.
   - Se limpian las variables numéricas para manejar valores faltantes y formatos no numéricos.

4. **Análisis exploratorio y descriptivo**
   - Se generan estadísticas básicas, gráficos de series, histogramas y medias móviles para cada variable.
   - Se realizan pruebas de estacionariedad (ADF y KPSS).
   - Se lleva a cabo una descomposición estacional y análisis de autocorrelación (ACF y PACF).

5. **Preparación de pares para análisis conjunto**
   - Se crean DataFrames con pares de series (precio diario vs variable macro) alineadas temporalmente para facilitar el análisis bivariado.

6. **Análisis de correlaciones**
   - Se calcula la correlación de Pearson entre pares de variables.
   - Se clasifican las relaciones como procíclicas, contracíclicas o acíclicas según el signo y magnitud de la correlación.
   - Se generan gráficos comparativos con ambas series superpuestas en ejes dobles.

---

## Estructura del proyecto

- **Descarga y preprocesamiento**  
  Código para obtener y preparar datos (yfinance, pandas).

- **Limpieza y unificación**  
  Tratamiento de valores faltantes, conversión de tipos y combinación de fuentes.

- **Análisis univariado**  
  Estadísticas descriptivas, pruebas de estacionariedad y descomposición.

- **Análisis bivariado**  
  Construcción de pares y análisis de correlación con visualización.

---

## Requisitos

- Python 3.7 o superior
- Librerías:
  - pandas
  - numpy
  - yfinance
  - matplotlib
  - statsmodels
  - scipy

---

## Uso

1. Ejecutar el código de descarga y limpieza para obtener el DataFrame principal combinado.
2. Ejecutar los análisis univariados para cada serie macroeconómica.
3. Preparar los DataFrames para pares de análisis.
4. Ejecutar el análisis de correlaciones para identificar relaciones y visualizar los resultados.

---

## Objetivo

El proyecto busca entender cómo se relaciona la evolución diaria del precio del ADR Bancolombia con variables macroeconómicas importantes, proporcionando un análisis cuantitativo y visual para detectar patrones y posibles dependencias económicas.

---

## Autor

[Andres Camilo]

---


