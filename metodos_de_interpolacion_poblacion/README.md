# Desincronización de Frecuencias en Series Temporales: Análisis Comparativo de Métodos de Interpolación y Suavizado
---
## Resumen (Abstract)

El presente informe técnico aborda un desafío común en el análisis de datos socioeconómicos y demográficos: la integración de registros mensuales de alta frecuencia con proyecciones poblacionales de publicación anual. 

A tal fin, se evalúan tres enfoques metodológicos: **Interpolación Lineal**, **Tasa Intercensal Exponencial** y **Promedio Móvil Centrado**. El estudio utiliza como base las estadísticas oficiales publicadas por el [Banco Mundial para el período 1960-2024](https://datos.bancomundial.org/indicador/SP.POP.TOTL?locations=AR), complementadas con los datos provisorios proyectados para el año 2025 extraídos de [Worldometers](https://www.worldometers.info/es/poblacion-mundial/poblacion-argentina/).

El objetivo principal es cuantificar la **"materialidad"** del error de estimación derivado de la elección del denominador, determinar si la aplicación (o ausencia) de estos métodos puede generar desvíos que conduzcan a un análisis erróneo de la realidad social, y sugerir un estándar de trabajo que garantice la auditabilidad y la suavidad de las series resultantes, eliminando los "saltos artificiales" que suelen ocurrir en los cierres de cada período anual.

---
## 1. Introducción

El presente análisis surge a partir del procesamiento y estudio de los datos oficiales publicados por la **Administración Nacional de la Seguridad Social (ANSES)**, específicamente aquellos referidos a la cobertura de la Asignación Universal por Hijo (AUH) y la Asignación por Embarazo para Protección Social (AxE), detallados en el [Boletín de Asignaciones de Octubre 2025](https://www.anses.gob.ar/estudiosyestadisticas/boletin-asignaciones-para-proteccion-social-octubre-2025).

En el proceso de enriquecer este dataset mediante el cálculo de indicadores propios —como variaciones intermensuales y actualización de importes reales—, se identificó la relevancia de construir un **Índice de Minoridad**. Este indicador tiene como objetivo medir la tasa de cobertura de las asignaciones sobre el total de la población objetivo en Argentina. Para su construcción, se utilizó la información demográfica anual emitida por el **Banco Mundial**, la cual presenta una periodicidad de cierre a diciembre de cada año.

Al intentar cruzar ambas fuentes, se presentó el desafío técnico de la desincronización de frecuencias: datos administrativos con granularidad mensual frente a denominadores poblacionales con actualización anual. Una alternativa simplista hubiera sido replicar el valor anual de población en cada uno de los doce meses del ejercicio; sin embargo, se consideró imperativo evaluar métodos alternativos de interpolación para dotar al índice de una mayor precisión técnica. 

En última instancia, la solidez de la arquitectura de los datos redunda en indicadores más robustos, lo que permite un análisis más exacto de la realidad social y minimiza las distorsiones estadísticas en las conclusiones de gestión.
