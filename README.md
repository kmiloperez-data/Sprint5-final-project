# Sprint5-final-project

# 🚗 Movilidad Urbana y Economía en América Latina y el Mundo (2024)

Este proyecto evalúa la relación entre la **movilidad urbana** (tiempos de congestión y retrasos viales) y la **productividad económica** (PIB per cápita, desempleo y población) en las principales ciudades latinoamericanas y globales durante el año 2024. El análisis busca identificar qué metrópolis requieren prioridad en inversión de infraestructura de transporte público y gestión del tráfico.

---

## 🎯 Objetivo del Proyecto

- **General:** Evaluar si un mayor nivel socioeconómico mitiga los problemas de tráfico urbano o si la congestión vial actúa como un cuello de botella para el desarrollo económico en ciudades emergentes y desarrolladas.
- **Específicos:**
  - Limpiar y estandarizar datos masivos de movilidad en tiempo real e indicadores macroeconómicos.
  - Consolidar las métricas diarias de tráfico en promedios anuales representativos para el año 2024.
  - Integrar ambos universos de datos mediante técnicas de manipulación y unión en `pandas`.
  - Identificar patrones, valores atípicos (*outliers*) y ciudades prioritarias para proyectos de movilidad sostenible.

---

## 📊 Datasets Utilizados

| Dataset | Origen | Descripción | Columnas Clave |
| :--- | :--- | :--- | :--- |
| `tomtom_traffic.csv` | **TomTom Traffic Index** | +1 millón de registros de tráfico global en tiempo real e histórico. | `City`, `Country`, `UpdateTimeUTC`, `JamsDelay`, `TravelTimeLivePer10KmsMins`, `MinsDelay` |
| `oecd_city_economy.csv` | **OECD Cities** | Indicadores económicos y demográficos de 30 grandes ciudades globales. | `City`, `Country`, `Year`, `City GDP/capita`, `Unemployment %`, `PM2.5 (μg/m³)`, `Population (M)` |

---

## 🛠️ Etapas del Análisis

El desarrollo del proyecto se ejecutó en 7 pasos clave:

1. **Carga y Exploración Inicial:**
   - Inspección de tipos de datos (`.info()`) e identificación de columnas de texto con valores numéricos y marcas temporales.
2. **Limpieza y Estandarización:**
   - Conversión de nombres de columnas a formato `snake_case`.
   - Conversión de fechas a tipo `datetime` UTC.
   - Limpieza de cadenas numéricas en variables económicas (remoción de `%`, `.`, `,` y casting a `float`).
   - Cálculo de la población total (`population`) a partir de `population_m`.
3. **Filtrado Temporal:**
   - Extracción de la marca anual `.dt.year` y aislamiento de los datos correspondientes al año **2024**.
4. **Agregación de Datos de Movilidad:**
   - Agrupación por ciudad, país y año para calcular promedios anuales de retrasos (`jams_delay`, `mins_delay`) e índices de tráfico.
5. **Unión e Integración (`INNER JOIN`):**
   - Fusión de los datasets de movilidad y economía utilizando `city` y `year` como llaves primarias de unión (`merged`).
6. **Análisis Visual y Diagnóstico:**
   - Generación de *Boxplots* para detectar *outliers* de congestión.
   - Histogramas de distribución del PIB per cápita.
   - Gráficos de barras comparativos de congestión vs. PIB per cápita.
7. **Exportación de Resultados:**
   - Generación del dataset consolidado y limpio `ladb_mobility_economy_2024_clean.csv`.

---

## 💡 Hallazgos Clave

- **Ausencia de Correlación Directa:** Un mayor PIB per cápita no garantiza mejores condiciones de movilidad. Metrópolis con alto ingreso per cápita como Montevideo muestran tráfico moderado, mientras que metrópolis con PIB medio/bajo enfrentan graves cuellos de botella.
- **Valores Atípicos Críticos:** **Mexico-City** se posiciona como la ciudad más congestionada de la muestra con un `jams_delay` promedio de **2,833.06 unidades**.
- **Ciudades Prioritarias para Inversión:** Metrópolis como **Bogotá** y **Lima** combinan alta congestión vehicular con PIB per cápita moderado o bajo, lo que indica pérdidas significativas de productividad y exige atención prioritaria en infraestructura de transporte masivo.

---

## ⚙️ Requisitos del Entorno

Para ejecutar este cuaderno localmente o en la nube necesitas Python 3.9+ y las siguientes librerías:

```bash
pip install pandas numpy matplotlib seaborn jupyter
```

---

## 🚀 Cómo Ejecutar el Notebook

### Opción A: Ejecutar en Google Colab (Recomendado)
1. Sube el archivo `S5 ladb_mobility_economy_project_student.ipynb` a tu Google Drive o impórtalo directamente en [Google Colab](https://colab.research.google.com/).
2. Asegúrate de colocar los archivos `tomtom_traffic.csv` y `oecd_city_economy.csv` en el directorio de trabajo o en la ruta `/datasets/`.
3. Selecciona **Entorno de ejecución > Ejecutar todas**.

### Opción B: Ejecutar Localmente en Jupyter Notebook
1. Clona este repositorio:
   ```bash
   git clone https://github.com/tu-usuario/nombre-del-repositorio.git
   cd nombre-del-repositorio
   ```
2. Crea una carpeta llamada `datasets/` en la raíz del proyecto y coloca los archivos `.csv` correspondientes.
3. Inicia Jupyter Notebook:
   ```bash
   jupyter notebook
   ```
4. Abre `S5 ladb_mobility_economy_project_student.ipynb` y ejecuta las celdas secuencialmente.

---

## 📋 Guía de Reproducción Paso a Paso

1. **Paso 1:** Verifica la lectura correcta de las fuentes de datos desde la ruta `/datasets/`.
2. **Paso 2:** Corre las celdas de limpieza para validar que el tipo de dato de `city_gdp_capita`, `unemployment_pct` y `population` sea `float64`.
3. **Paso 3 y 4:** Filtra el período 2024 y genera el DataFrame agrupado `traffic_city_year_2024`.
4. **Paso 5:** Realiza la unión `pd.merge(..., how='inner')` para generar la tabla final `merged`.
5. **Paso 6:** Ejecuta la celda de visualización para reconstruir los gráficos descriptivos.
6. **Paso 7:** Ejecuta la celda de exportación para generar el archivo comprimido/limpio `ladb_mobility_economy_2024_clean.csv`.

---

## 📁 Archivos del Repositorio

- `S5 ladb_mobility_economy_project_student.ipynb`: Notebook principal con código, análisis y visualizaciones.
- `ladb_mobility_economy_2024_clean.csv`: Dataset resultante procesado e integrado.
- `README.md`: Documentación del proyecto.
