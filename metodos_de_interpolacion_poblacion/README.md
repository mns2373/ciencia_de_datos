# Desincronización de Frecuencias en Series Temporales Demográficas: Comparación de Métodos de Interpolación Mensual a partir de Datos Anuales

**Autor:** [Martin Nicolas Serafini](https://www.linkedin.com/in/martin-nicolas-serafini-05224923b/)

---
## 1. Abstract
El presente trabajo aborda el problema de la desincronización de frecuencias en series temporales socioeconómicas, específicamente en la integración de datos mensuales con estimaciones poblacionales anuales. Se utilizan datos de población de la República Argentina provenientes del Banco Mundial para el período 1960–2024, los cuales corresponden a estimaciones de mitad de año (mid-year), lo que introduce una desalineación temporal respecto de series de fin de período.

Sobre esta base, se evalúan distintos métodos de interpolación —Interpolación Lineal, Interpolación Exponencial y Promedio Móvil Centrado— con el objetivo de construir series mensuales consistentes. El análisis se centra en cuantificar el impacto de estas metodologías sobre indicadores derivados, introduciendo el concepto de **materialidad del error de estimación** como criterio de evaluación.

Los resultados evidencian que la elección del método de interpolación puede generar diferencias significativas, afectando la interpretación de la dinámica socioeconómica. En consecuencia, se proponen lineamientos metodológicos orientados a mejorar la consistencia, comparabilidad y auditabilidad de las series temporales utilizadas en análisis aplicados.

---
## 2. Introducción
El análisis de indicadores socioeconómicos frecuentemente requiere la integración de fuentes de datos con distinta periodicidad. Un caso representativo es la combinación de registros administrativos de frecuencia mensual con estimaciones poblacionales disponibles únicamente en frecuencia anual, lo que plantea desafíos metodológicos en la construcción de indicadores consistentes.

El presente trabajo surge a partir del estudio de datos publicados por la Administración Nacional de la Seguridad Social (ANSES), en particular aquellos vinculados a la cobertura de la Asignación Universal por Hijo (AUH) y la Asignación por Embarazo para Protección Social (AxE). En este contexto, la correcta especificación del denominador poblacional resulta relevante para la adecuada interpretación de los indicadores que se construyan.

El principal desafío técnico radica en la desincronización de frecuencias, donde la población total —publicada anualmente por el [Banco Mundial](https://datos.bancomundial.org/indicador/SP.POP.TOTL?locations=AR) para el período 1960-2024— debe ser adaptada a una escala mensual. Adicionalmente, dichas estimaciones corresponden a valores de mitad de año (mid-year population), lo que implica que cada observación anual se encuentra centrada aproximadamente en el mes de julio y no representa directamente niveles de población a fin de período.

En consecuencia, el problema abordado no se limita a una simple interpolación temporal (desagregación de frecuencia), sino que también involucra una desalineación en la referencia temporal de la serie. Esto introduce un desfase intra-anual que debe ser considerado en la construcción del denominador poblacional. Una aproximación simplificada consiste en replicar el valor anual en cada mes; sin embargo, este enfoque genera discontinuidades artificiales y puede distorsionar el análisis de tendencias, afectando la interpretación de la dinámica bajo análisis.

Frente a este escenario, el presente trabajo evalúa distintos métodos de interpolación y suavizado con el objetivo de construir series mensuales consistentes, comparables y metodológicamente robustas. En particular, se propone analizar el impacto de cada enfoque sobre indicadores derivados, introduciendo el concepto de **materialidad del error de estimación** como criterio para determinar la relevancia práctica de las diferencias observadas.

La contribución del estudio radica en la comparación sistemática de estos métodos y en la formulación de un criterio metodológico orientado a mejorar la calidad analítica, la consistencia temporal y la auditabilidad de las series utilizadas en el análisis de fenómenos socioeconómicos.

---
## 3. Fuente de Datos

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

---
## 4. Problema metodológico
### 4.1 Desincronización de frecuencias
El problema central abordado en este trabajo se inscribe en el marco de la **desagregación temporal de series (temporal disaggregation)**, donde se requiere transformar una serie de baja frecuencia en una de mayor frecuencia manteniendo consistencia con los valores originales.
En particular, se dispone de una serie anual de población y se busca construir una representación mensual que permita su utilización como denominador en indicadores socioeconómicos de frecuencia mensual.
Esta desincronización de frecuencias implica que:
- la variable explicativa (población) se encuentra disponible en frecuencia anual  
- las variables de interés (registros administrativos) se observan en frecuencia mensual  
lo que genera una incompatibilidad directa para el cálculo de indicadores.

### 4.2 Definición formal del problema
Sea \( P_t \) la población anual correspondiente al año \( t \), disponible en frecuencia anual, y sea \( P_{t,m} \) la población correspondiente al mes \( m \) del año \( t \), no observada.
El objetivo consiste en estimar la serie mensual \( \{P_{t,m}\} \) tal que:
- preserve coherencia con los valores anuales observados  
- represente adecuadamente la dinámica intra-anual del fenómeno  
- permita el cálculo consistente de indicadores mensuales  
Adicionalmente, la serie anual disponible presenta una particularidad relevante: las estimaciones corresponden a valores de **mitad de año (mid-year)**, lo que introduce una **desalineación en la referencia temporal** respecto de una serie mensual de fin de período.
En consecuencia, el problema metodológico involucra dos dimensiones simultáneas:
1. **Desagregación temporal** (anual → mensual)  
2. **Alineación temporal** (mid-year → end-of-period)  

### 4.3 Implicancias estadísticas
La utilización directa de la serie anual sin tratamiento introduce diversas distorsiones en los indicadores derivados.

#### a) Discontinuidades artificiales
La replicación del valor anual en cada mes genera una estructura escalonada, caracterizada por saltos discretos en los cambios de año. Estas discontinuidades no reflejan la dinámica real del fenómeno y constituyen artefactos del proceso de construcción de la serie.

#### b) Sesgos en tasas e indicadores
La utilización de un denominador poblacional no ajustado temporalmente puede generar sesgos en:
- tasas de cobertura  
- ratios per cápita  
- indicadores de evolución  
Estos sesgos pueden ser sistemáticos, especialmente en contextos de crecimiento o decrecimiento poblacional sostenido.

#### c) Pérdida de consistencia temporal
La falta de suavidad en la serie mensual resultante puede afectar la coherencia intertemporal, dificultando el análisis de tendencias y la interpretación de variaciones de corto plazo.

#### d) Desfase temporal sistemático
Dado que la serie anual corresponde a valores de mitad de año, su utilización directa en una estructura mensual implica asignar a cada período valores que no representan correctamente el momento temporal considerado, introduciendo un error de alineación que se distribuye de manera sistemática a lo largo del año.

### 4.4 Alcance del problema
En este contexto, el presente trabajo no busca reestimar la serie poblacional anual, sino evaluar distintos métodos de interpolación para su desagregación mensual, analizando el impacto de dichas metodologías sobre la consistencia temporal y la precisión de los indicadores derivados.

---
## 5. Metodología

En esta sección se presentan los métodos utilizados para la desagregación temporal de la serie anual de población a frecuencia mensual. Cada enfoque implica distintos supuestos sobre la dinámica intra-anual del fenómeno y genera resultados con propiedades diferenciadas en términos de consistencia temporal y precisión.

### 5.1 Interpolación lineal
#### Definición
La interpolación lineal asume que la población evoluciona a una tasa constante entre dos observaciones anuales consecutivas. Bajo este supuesto, la variación total entre años se distribuye uniformemente entre los 12 meses.

$$
P_{t,m} = P_t + \frac{m}{12}\left(P_{t+1} - P_t\right)
$$

Donde:

$$
\begin{aligned}
m        &:\ \text{mes dentro del año, con } m = 0,1,\dots,12 \\
P_t      &:\ \text{población en el año } t \\
P_{t+1}  &:\ \text{población en el año siguiente} \\
P_{t,m}  &:\ \text{población estimada en el mes } m \text{ del año } t
\end{aligned}
$$

#### Supuestos
- Crecimiento poblacional lineal dentro del año  
- Distribución uniforme del cambio anual  
- Ausencia de variaciones intra-anuales significativas  
#### Ventajas
- Simplicidad de implementación  
- Interpretación directa  
- Garantiza continuidad entre años  
- Bajo costo computacional  
#### Limitaciones
- No refleja crecimiento compuesto  
- Puede generar sesgos si la dinámica es no lineal  
- No contempla explícitamente la alineación temporal (mid-year)  

---

### 5.2 Interpolación exponencial (tasa intercensal)

#### Definición

Este método asume que la población crece a una tasa constante en términos relativos (crecimiento exponencial), lo cual resulta consistente con modelos demográficos estándar.

Primero se calcula la tasa de crecimiento anual continua:

$$
r_t = \ln\left(\frac{P_{t+1}}{P_t}\right)
$$

Luego, la población mensual se estima como:

$$
P_{t,m} = P_t \cdot e^{\left(\frac{r_t \cdot m}{12}\right)}, \quad m = 0,1,\dots,12
$$

Donde:

$$
\begin{aligned}
P_t      &:\ \text{población en el año } t,\ \text{utilizada como condición inicial} \\
P_{t+1}  &:\ \text{población en el año siguiente} \\
r_t      &:\ \text{tasa de crecimiento continua anual} \\
m        &:\ \text{mes dentro del año, con } m = 0,1,\dots,12 \\
\frac{m}{12} &:\ \text{proporción del año transcurrida} \\
e        &:\ \text{base del logaritmo natural, que permite modelizar crecimiento exponencial}
\end{aligned}
$$

La expresión \(r_t \cdot \frac{m}{12}\) representa el crecimiento acumulado hasta el mes \(m\) en términos continuos, mientras que la función exponencial transforma dicha tasa en un factor multiplicativo aplicado sobre la población inicial.

Este enfoque garantiza que la serie interpolada preserve los valores anuales originales, cumpliendo que \(P_{t,0} = P_t\) y \(P_{t,12} = P_{t+1}\).

---

#### Supuestos

- Crecimiento proporcional (exponencial)  
- Tasa de crecimiento constante dentro del año  
- Evolución demográfica suave  

---

#### Ventajas

- Mayor realismo demográfico  
- Captura crecimiento compuesto  
- Evita subestimaciones en contextos de crecimiento sostenido  
- Genera trayectorias más naturales  

---

#### Limitaciones

- Mayor complejidad conceptual  
- Sensible a errores en datos extremos  
- Puede amplificar variaciones pequeñas  
- No corrige explícitamente la desalineación temporal  

---

### 5.3 Promedio móvil centrado

#### Definición

El promedio móvil centrado es un método de suavizado que reduce la variabilidad de corto plazo promediando observaciones adyacentes. En este contexto, se aplica sobre una serie mensual previamente interpolada.

Para una ventana de tamaño k = 2h + 1, el promedio móvil centrado se define como:

P~_{t,m} = (1 / (2h + 1)) * Σ_{j=-h}^{h} P_{t,m+j}

Caso particular (ventana de 3 meses):


---

#### Supuestos

- La serie presenta ruido o variaciones no estructurales  
- La tendencia subyacente es suave  
- Las variaciones de corto plazo no son relevantes  

---

#### Ventajas

- Reduce ruido y oscilaciones artificiales  
- Mejora la suavidad de la serie  
- Incrementa la consistencia temporal  
- Fácil implementación  

---

#### Limitaciones

- No genera una serie base (requiere interpolación previa)  
- Introduce pérdida de información en extremos  
- Puede suavizar en exceso cambios reales  
- Puede generar rezagos en la serie  

---

### 5.4 Consideraciones generales

Los métodos presentados responden a distintos supuestos sobre la evolución intra-anual de la población. Mientras que la interpolación lineal y exponencial constituyen enfoques de desagregación directa, el promedio móvil centrado actúa como técnica de suavizado complementaria.

La elección del método adecuado dependerá del equilibrio entre:

- realismo demográfico  
- simplicidad operativa  
- consistencia temporal  
- impacto sobre indicadores derivados  
