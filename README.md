# Pipeline de Datos ETL para Análisis de Viajes de Uber en NYC (2014)

---

# Sales ETL Pipeline

![Python](https://img.shields.io/badge/python-v3.9+-blue.svg)
![License](https://img.shields.io/badge/license-MIT-green.svg)

---
<artifact identifier="readme-uber-etl" type="text/markdown" title="README.md para Repositorio GitHub">
# 🚖 Uber NYC ETL Pipeline - Arquitectura Medallion

📋 Descripción del Proyecto
Pipeline ETL profesional de extremo a extremo para el análisis de 4.5+ millones de viajes de Uber en NYC (2014), implementando una arquitectura de lago de datos tipo Medallion con tres capas (Bronze, Silver, Gold). El proyecto demuestra capacidades avanzadas de ingeniería de datos utilizando tecnologías cloud-native y mejores prácticas de la industria.
🎯 Características Principales

✅ Arquitectura Medallion completa (Bronze → Silver → Gold)
✅ Procesamiento distribuido con Apache Spark
✅ Transacciones ACID mediante Delta Lake
✅ Ingeniería de características automatizada
✅ Data Quality validations en cada capa
✅ 5 tablas Gold especializadas para analytics
✅ Dashboard ejecutivo con SQL analytics
✅ 100% reproducible en Databricks Community Edition


🎯 Objetivos del Proyecto
Objetivos de Negocio

Analizar patrones de demanda temporal y geográfica de Uber NYC
Identificar hotspots de alta concentración de viajes
Optimizar operaciones mediante insights de horas pico y rendimiento por base
Generar KPIs ejecutivos para toma de decisiones estratégicas

Objetivos Técnicos

Construir un pipeline ETL escalable y mantenible
Implementar mejores prácticas de Data Engineering
Demostrar experiencia con Databricks, Spark y Delta Lake
Crear un portafolio profesional de ingeniería de datos


#### **Resumen Ejecutivo**
Describe brevemente el proyecto y sus objetivos principales.
Este proyecto establece una robusta **canalización de datos ETL (Extracción, Transformación, Carga)** para analizar los datos de viajes de Uber en la ciudad de Nueva York durante el período de **abril a septiembre de 2014**. Utilizando una **arquitectura Medallón (Bronze, Silver, Gold)** implementada en **Databricks Free Edition**, la solución ingesta datos crudos, los limpia y enriquece, y finalmente los agrega en un formato optimizado para el análisis de negocio. El objetivo principal es proporcionar **insights accionables** sobre patrones de demanda, rendimiento de bases y distribución geográfica de los viajes, permitiendo la toma de decisiones informadas.

#### **Contexto del Negocio y Objetivos**
Explica el problema de negocio y las preguntas clave que el proyecto busca responder.
La gestión eficiente de una plataforma de transporte como Uber requiere una comprensión profunda de los patrones de demanda y oferta. Sin un análisis de datos estructurado, Uber NYC podría enfrentar ineficiencia operacional, una experiencia de usuario subóptima y una planificación estratégica deficiente.

Este proyecto busca responder preguntas clave como:
*   ¿Cuáles son las **horas pico de demanda** de Uber en NYC y cómo varían por día de la semana?
*   ¿Cómo se distribuye la demanda de viajes **geográficamente** en NYC? ¿Existen "hotspots" de recogida?
*   ¿Cuál es el **rendimiento de cada base de Uber** en términos de volumen de viajes y actividad?
*   ¿Cómo ha evolucionado la demanda de viajes **mes a mes** durante el período analizado (abril-septiembre de 2014)?
*   ¿Existen patrones de demanda distintivos entre **días de semana y fines de semana**?

Los objetivos principales del proyecto son:
*   Construir una **Canalización de Datos Confiable**.
*   Proporcionar **Datos de Alta Calidad**.
*   Generar **Insights de Negocio**.
*   Demostrar **Habilidades Técnicas** en ingeniería de datos, especialmente con Databricks y Delta Lake.

#### **Descripción del Conjunto de Datos**
Detalla la fuente de datos utilizada.
El proyecto se basa en el conjunto de datos **'Uber Pickups in New York City' de Kaggle**.
*   **Periodo de los Datos**: Abril a septiembre de 2014.
*   **Volumen de Datos**: Más de **4.5 millones de registros** de recogidas de Uber.
*   **Formato de los Archivos**: Cada mes está contenido en un archivo CSV separado.
*   **Ubicación**: Ciudad de Nueva York.

Las columnas clave en los archivos mensuales son:
*   `Date/Time`: Fecha y hora exactas de la recogida del viaje.
*   `Lat`: Latitud geográfica del punto de recogida.
*   `Lon`: Longitud geográfica del punto de recogida.
*   `Base`: Código de la base de la empresa afiliada a la recogida de Uber.

Los archivos de origen son: `uber-raw-data-apr14.csv`, `uber-raw-data-aug14.csv`, `uber-raw-data-jul14.csv`, `uber-raw-data-jun14.csv`, `uber-raw-data-may14.csv`, `uber-raw-data-sep14.csv`.

#### **Arquitectura de la Solución: Enfoque Medallón**
Explica la arquitectura Medallón implementada.
La solución implementa una **arquitectura de lago de datos con el enfoque Medallón**, organizando los datos en tres capas distintas: Bronze (Crudo), Silver (Curado) y Gold (Consumible). Esta estructura promueve la calidad, la gobernanza y la facilidad de consumo de los datos.

**(Opcional: Si tienes un diagrama de arquitectura, insértalo aquí)**
`![Diagrama de Arquitectura Medallón](assets/architecture_diagram.png)`

##### **Descripción de las Capas:**
*   **Capa Bronze (Raw Data)**:
    *   **Propósito**: Ingesta de datos crudos desde las fuentes, preservando su formato original, actuando como un archivo histórico inmutable.
    *   **Contenido**: Datos de los archivos CSV de Uber tal cual, con metadatos de auditoría (timestamp de ingesta, nombre del archivo fuente, versión de la capa).
    *   **Formato**: Delta Lake.
*   **Capa Silver (Cleaned & Enriched)**:
    *   **Propósito**: Limpieza, validación y enriquecimiento de los datos de la capa Bronze, listos para un análisis más profundo y la creación de características.
    *   **Contenido**: Datos limpios, con tipos de datos corregidos, valores nulos manejados, duplicados eliminados y nuevas características generadas (ej. hora de recogida, día de la semana, tipo de día, categoría de tiempo).
    *   **Formato**: Delta Lake.
*   **Capa Gold (Business-Ready)**:
    *   **Propósito**: Agregación y modelado de datos para casos de uso específicos de negocio, optimizadas para el rendimiento de consultas y el consumo por herramientas de BI.
    *   **Contenido**: KPIs ejecutivos, métricas temporales (diarias, horarias, mensuales), rendimiento por base, y datos geoespaciales.
    *   **Formato**: Delta Lake.

#### **Fases del Pipeline ETL**
Detalla cada paso del pipeline, mencionando los notebooks utilizados.
El pipeline ETL se implementa a través de una serie de notebooks de Databricks, cada uno encargado de una fase específica.

*   **1. Extracción (E): Capa Bronze (`01_Uber_Bronze_Layer.ipynb`)**
    *   **Objetivo**: Ingestar los datos crudos de los archivos CSV en una tabla Delta en la capa Bronze.
    *   **Proceso**: Configuración de rutas, validación de archivos fuente, definición de esquema explícito, lectura de datos, adición de metadatos de auditoría (ej. `ingestion_timestamp`, `source_file`), y carga a Delta Lake.
    *   **Validación**: Verificación del recuento de registros y muestra de datos.
*   **2. Transformación (T): Capa Silver (`02_Uber_Silver_Layer.ipynb`)**
    *   **Objetivo**: Limpiar, validar y enriquecer los datos de la capa Bronze, preparándolos para el análisis.
    *   **Proceso**: Lectura de datos Bronze, análisis inicial de calidad de datos, **limpieza de datos** (renombrado de columnas, conversión de tipos, validación de rangos geográficos, manejo de nulos y duplicados), **ingeniería de características** (ej. `pickup_hour`, `day_type`, `trip_id`), y adición de metadatos de auditoría Silver.
    *   **Validación**: Verificación del esquema final, recuento de registros y muestra de datos limpios.
*   **3. Carga (L): Capa Gold (`03_Uber_Gold_Layer.ipynb`)**
    *   **Objetivo**: Crear agregaciones de negocio, KPIs y métricas analíticas desde la capa Silver, optimizadas para el consumo.
    *   **Proceso**: Lectura de datos Silver y creación de cinco tablas Gold especializadas:
        *   `daily_metrics` (Agregaciones Diarias)
        *   `base_hourly_metrics` (Métricas Horarias por Base)
        *   `monthly_kpis` (KPIs Mensuales)
        *   `spatial_metrics` (Métricas Geoespaciales)
        *   `executive_dashboard` (Resumen Ejecutivo Global)
    *   Cada DataFrame agregado se escribe como una tabla Delta separada en la capa Gold.
    *   **Validación**: Verificación del recuento de registros y muestra de datos de cada tabla Gold.

#### **Modelo de Datos**
Presenta el esquema de las tablas en cada capa. Puedes resumirlo o enlazar a secciones más detalladas.
El modelo de datos sigue la arquitectura Medallón, con esquemas que evolucionan en cada capa para mejorar la calidad y la utilidad de los datos.

*   **Capa Bronze (`uber_bronze`)**: `Date/Time` (StringType), `Lat` (DoubleType), `Lon` (DoubleType), `Base` (StringType), `ingestion_timestamp` (TimestampType), `source_file` (StringType), `bronze_layer_version` (StringType).
*   **Capa Silver (`uber_silver`)**: Incluye las columnas de Bronze transformadas (`pickup_datetime`, `latitude`, `longitude`, `base_code`), más numerosas **columnas enriquecidas** como `pickup_hour`, `pickup_day_of_week`, `time_category`, `day_type`, `trip_id`, y metadatos de auditoría Silver.
*   **Capa Gold (Tablas Agregadas)**:
    *   `daily_metrics`: Incluye métricas como `total_trips`, `active_bases`, `morning_rush_trips`, y dimensiones temporales.
    *   `base_hourly_metrics`: Métricas por `base_code` y `pickup_hour`, como `hourly_trips`, `weekday_percentage`, `weekend_percentage`.
    *   `monthly_kpis`: KPIs mensuales como `total_monthly_trips`, `mom_growth`, `rush_hours_percentage`.
    *   `spatial_metrics`: Agregaciones por `latitude_bin` y `longitude_bin` con `total_trips`, `trip_density`.
    *   `executive_dashboard`: Resumen de alto nivel como `total_trips_period`, `avg_daily_trips`, `rush_hours_share`, `weekend_vs_weekday_ratio`.

#### **Tecnologías y Herramientas**
Enumera y justifica las tecnologías clave utilizadas.
*   **Databricks Free Edition**: Plataforma unificada con Spark optimizado, soporte nativo para Delta Lake, y facilidades de colaboración, ideal para procesar grandes volúmenes de datos.
*   **Delta Lake**: Garantiza fiabilidad (transacciones ACID), esquema evolucionable, manejo de datos a escala, control de versiones y es nativo con Spark.
*   **Power BI**: Permite crear dashboards interactivos, se conecta directamente a Delta Lake y facilita la distribución de informes.

#### **Visualización y Hallazgos Clave**
Describe las visualizaciones importantes y los insights obtenidos.
La capa Gold está diseñada para ser directamente consumible por Power BI, permitiendo la creación de dashboards para la exploración de datos.

**Hallazgos Clave:**
*   **Crecimiento Mensual de Viajes**: Se observó un crecimiento sostenido, culminando en un **aumento del 24% en septiembre** de 2014, indicando una rápida adopción de Uber en NYC.
*   **Patrones de Demanda por Hora del Día**: Clara identificación de **"horas pico" entre las 17:00 y las 21:00**, crucial para la gestión de la flota y tarifas dinámicas.
*   **Rendimiento por Base de Operaciones**: Las bases **B02617, B02598 y B02682 dominan el volumen de viajes**, siendo pilares de la operación.
*   **Hotspots Geográficos de Demanda**: Identificación de zonas de alta concentración de recogidas como **Midtown Manhattan, el Distrito Financiero y el East Village**, sugiriendo dónde concentrar la oferta de vehículos.

**(Opcional: Si tienes capturas de pantalla de los dashboards o visualizaciones, insértalas aquí)**
`![Crecimiento Mensual de Viajes](assets/monthly_growth.png)`
`![Patrones de Demanda Horaria](assets/hourly_patterns.png)`

#### **Conclusiones**
Resume los logros del proyecto.
Este proyecto ha demostrado la capacidad de construir una canalización de datos ETL robusta y escalable, permitiendo la ingesta eficiente, la transformación de calidad, el modelado para el negocio y la habilitación de insights críticos sobre la demanda de Uber en NYC.

#### **Futuras Mejoras y Pasos Siguientes**
Sugiere cómo el proyecto podría evolucionar.
Para seguir evolucionando y extraer aún más valor de los datos, se proponen:
*   **Integración de Datos Adicionales**: Incorporar datos meteorológicos, eventos especiales, datos de tráfico o análisis de sentimiento de redes sociales.
*   **Análisis Predictivo**: Desarrollar modelos de Machine Learning para pronosticar la demanda o detectar anomalías.
*   **Optimización de Costos y Rendimiento**: Implementar particionamiento inteligente, Z-Ordering, o migrar a streaming de datos para análisis casi instantáneo.
*   **Gobernanza y Monitoreo**: Establecer controles automatizados de calidad de datos y un catálogo de datos.
*   **Expansión a la Plataforma Azure**: Utilizar Azure Data Factory para orquestación, Azure Databricks como motor de procesamiento, Azure SQL Database para almacenamiento final, Power BI para visualización, Azure Key Vault para gestión segura de credenciales, y Azure DevOps para CI/CD.

#### **Cómo Ejecutar el Proyecto (Configuración)**
Esta sección es crucial para un portafolio de GitHub, ya que permite a otros replicar tu trabajo.

1.  **Requisitos**:
    *   Una cuenta de **Databricks Free Edition** (o superior).
    *   Acceso a los archivos CSV de 'Uber Pickups in New York City' de Kaggle (disponibles en [https://www.kaggle.com/datasets/fivethirtyeight/uber-pickups-in-new-york-city](https://www.kaggle.com/datasets/fivethirtyeight/uber-pickups-in-new-york-city)).
    *   (Opcional) Power BI Desktop para la visualización final.

2.  **Configuración del Entorno en Databricks**:
    *   **Crear un clúster**: Configura un clúster de Spark compatible con Databricks Runtime.
    *   **Cargar los datos crudos**: Sube los seis archivos CSV (`uber-raw-data-apr14.csv` a `uber-raw-data-sep14.csv`) a una ubicación accesible dentro de Databricks (ej. DBFS o un montaje de almacenamiento en la nube). **Asegúrate de ajustar las rutas de origen en el notebook `01_Uber_Bronze_Layer.ipynb` para que apunten a la ubicación correcta de tus archivos CSV.**
    *   **Configurar Volúmenes**: Si estás utilizando la estructura de volúmenes de Databricks (como `/Volumes/workspace/default/uber_etl_azure/`), asegúrate de que estos estén configurados o adapta las rutas en los notebooks.

3.  **Ejecución de los Notebooks**:
    *   **Paso 1: Capa Bronze**
        *   Abre `notebooks/01_Uber_Bronze_Layer.ipynb`.
        *   Ejecuta todas las celdas para ingestar los datos crudos y crear la tabla `uber_bronze`.
    *   **Paso 2: Capa Silver**
        *   Abre `notebooks/02_Uber_Silver_Layer.ipynb`.
        *   Ejecuta todas las celdas para limpiar, validar y enriquecer los datos, creando la tabla `uber_silver`.
    *   **Paso 3: Capa Gold**
        *   Abre `notebooks/03_Uber_Gold_Layer.ipynb`.
        *   Ejecuta todas las celdas para crear las cinco tablas agregadas de la capa Gold (`daily_metrics`, `base_hourly_metrics`, `monthly_kpis`, `spatial_metrics`, `executive_dashboard`).
    *   **Paso 4: Visualización (Databricks)**
        *   Abre `notebooks/04_Uber_Dashboard_Databricks.ipynb`.
        *   Ejecuta las celdas para explorar los datos de la capa Gold y ver visualizaciones preliminares.

4.  **Conexión con Power BI (Opcional)**:
    *   Conecta Power BI a las tablas Delta de la capa Gold a través del `Databricks SQL Analytics Endpoint`.


---

