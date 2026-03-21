# Desincronización de Frecuencias en Series Temporales Demográficas: Comparación de Métodos de Interpolación Mensual a partir de Datos Anuales

**Autor:** [Martin Nicolas Serafini](https://www.linkedin.com/in/martin-nicolas-serafini-05224923b/)

---
## 1. Abstract

El presente informe técnico aborda un problema recurrente en el análisis de series temporales socioeconómicas: la integración de datos de distinta frecuencia, específicamente registros mensuales con estimaciones poblacionales de periodicidad anual.

Se comparan tres enfoques metodológicos para la desagregación temporal de la población: **Interpolación Lineal**, **Interpolación Exponencial basada en tasa intercensal** y **Suavizado mediante Promedio Móvil Centrado**. El análisis se basa en datos oficiales del Banco Mundial para el período 1960–2024, complementados con estimaciones provisorias para 2025.

La contribución principal del trabajo consiste en evaluar el impacto cuantitativo de estos métodos sobre indicadores derivados, introduciendo el concepto de **materialidad del error de estimación** como criterio de validación. 

Los resultados permiten identificar diferencias  entre enfoques y sugerir lineamientos metodológicos orientados a mejorar la consistencia, suavidad y auditabilidad de las series temporales utilizadas en análisis socioeconómicos.

---
## 2. Introducción

El análisis de indicadores socioeconómicos frecuentemente requiere la integración de fuentes de datos con distinta periodicidad. Un caso representativo es la combinación de registros administrativos mensuales con estimaciones poblacionales disponibles únicamente en frecuencia anual.

Este trabajo surge a partir del estudio de datos publicados por la Administración Nacional de la Seguridad Social (ANSES), en particular aquellos vinculados a la cobertura de la Asignación Universal por Hijo (AUH) y la Asignación por Embarazo para Protección Social (AxE). En este contexto, la utilización de un denominador poblacional adecuado resulta de utilidad para la correcta interpretación de los indicadores.

El principal desafío técnico radica en la **desincronización de frecuencias**, donde la población total —publicada anualmente por el Banco Mundial— debe ser adaptada a una escala mensual. Una aproximación simplificada consiste en replicar el valor anual en cada mes; sin embargo, este enfoque introduce discontinuidades artificiales y puede distorsionar el análisis de tendencias.

Frente a este problema, el presente trabajo evalúa distintos métodos de interpolación y suavizado, con el objetivo de construir series mensuales consistentes y comparables. En particular, se propone analizar el impacto de cada metodología sobre los indicadores derivados, introduciendo el concepto de **materialidad del error** como criterio para determinar la relevancia práctica de las diferencias observadas.

La contribución pretendida al preparar el presente estudio radica en la comparación sistemática de estos enfoques y en la propuesta de un criterio metodológico que permita mejorar la calidad analítica y la auditabilidad de las series utilizadas en estudios socioeconómicos.

---
## 3. Datos (Data Sources)

### 3.1 Variable de análisis

La variable central del presente estudio es la **población total de la República Argentina**, expresada originalmente en frecuencia anual. Estas estimaciones son posteriormente transformadas a frecuencia mensual mediante distintos métodos de interpolación.

### 3.2 Fuentes de datos

Dado que la Argentina no dispone de estimaciones oficiales mensuales de población —y considerando que los censos nacionales realizados por el INDEC tienen una periodicidad aproximada de 10 años—, se recurre a fuentes internacionales estandarizadas.

#### Fuente principal

Se utiliza el indicador:
- [Población total (SP.POP.TOTL) – Banco Mundial](https://datos.bancomundial.org/indicador/SP.POP.TOTL?locations=AR)

El mismo provee una serie anual continua para el período **1960–2024**.

De acuerdo con la documentación oficial del Banco Mundial:
- Las estimaciones corresponden a **población de mitad de año (mid-year population)**  
- Representan población “de facto”, es decir, incluyen a todos los residentes independientemente de su estatus legal  
- Se construyen a partir de múltiples fuentes, principalmente censos nacionales y datos de organismos internacionales  

Ver referencias metodológicas:
- [Metadata del indicador SP.POP.TOTL](https://databank.worldbank.org/metadataglossary/world-development-indicators/series/SP.POP.TOTL)  
- [Notas metodológicas – World Development Indicators](https://datatopics.worldbank.org/world-development-indicators/)  

En términos metodológicos, el Banco Mundial basa sus estimaciones en las proyecciones de población de Naciones Unidas:
- [UN World Population Prospects](https://population.un.org/wpp/)

Estas proyecciones se elaboran mediante el **método de componentes demográficos (cohort-component method)**, que modeliza la evolución poblacional en función de:
- Fecundidad  
- Mortalidad  
- Migración  

Asimismo, en ausencia de datos observados directos para determinados períodos, el Banco Mundial aplica técnicas de interpolación, extrapolación y modelización estadística para la construcción de series anuales consistentes.

En este trabajo, la serie anual es tomada como dato de entrada (input) y no es modificada. El análisis se centra exclusivamente en la **desagregación temporal intra-anual**, mediante métodos de interpolación que permiten obtener estimaciones mensuales consistentes con los valores anuales observados.

#### Fuente complementaria

Para extender el análisis al año 2025, se incorporan estimaciones provisorias provenientes de:
- [Población de Argentina – Worldometers](https://www.worldometers.info/es/poblacion-mundial/poblacion-argentina/)

Esta fuente:
- No constituye un organismo estadístico oficial  
- Se basa en estimaciones derivadas de Naciones Unidas y otras bases internacionales  
- Debe ser considerada como una aproximación preliminar sujeta a revisión  

### 3.3 Periodo temporal

El análisis abarca el período:
- **1960 – 2025**

donde:
- 1960–2024: datos del Banco Mundial  
- 2025: estimación provisoria  

### 3.4 Limitaciones de los datos

El uso de estas fuentes implica ciertas restricciones relevantes:
1. **Frecuencia anual**  
   - No existen datos oficiales mensuales de población  
2. **Referencia temporal (mid-year)**  
   - Las estimaciones corresponden a valores centrados aproximadamente en el mes de julio  
   - No representan población a fin de período  
3. **Naturaleza estimada**  
   - Los valores no son observaciones directas, sino resultados de modelos demográficos  
4. **Dependencia de supuestos estructurales**  
   - Las proyecciones dependen de hipótesis sobre fecundidad, mortalidad y migración  
5. **Uso de datos no oficiales para 2025**  
   - Introduce un nivel adicional de incertidumbre  

### 3.5 Implicancias para el análisis

Estas características justifican la necesidad de:
- Transformar la serie desde una referencia temporal de mitad de año a una representación mensual  
- Aplicar métodos de interpolación consistentes  
- Evaluar el impacto de dichas transformaciones sobre los indicadores derivados  

lo cual constituye el eje metodológico del presente trabajo.
