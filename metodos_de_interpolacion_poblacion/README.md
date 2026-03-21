# Desincronización de Frecuencias en Series Temporales Demográficas: Comparación de Métodos de Interpolación Mensual a partir de Datos Anuales

**Autor:** [Martin Nicolas Serafini](https://www.linkedin.com/in/martin-nicolas-serafini-05224923b/)

---
## Abstract

El presente informe técnico aborda un problema recurrente en el análisis de series temporales socioeconómicas: la integración de datos de distinta frecuencia, específicamente registros mensuales con estimaciones poblacionales de periodicidad anual.

Se comparan tres enfoques metodológicos para la desagregación temporal de la población: **Interpolación Lineal**, **Interpolación Exponencial basada en tasa intercensal** y **Suavizado mediante Promedio Móvil Centrado**. El análisis se basa en datos oficiales del Banco Mundial para el período 1960–2024, complementados con estimaciones provisorias para 2025.

La contribución principal del trabajo consiste en evaluar el impacto cuantitativo de estos métodos sobre indicadores derivados, introduciendo el concepto de **materialidad del error de estimación** como criterio de validación. 

Los resultados permiten identificar diferencias  entre enfoques y sugerir lineamientos metodológicos orientados a mejorar la consistencia, suavidad y auditabilidad de las series temporales utilizadas en análisis socioeconómicos.

## 1. Introducción

El análisis de indicadores socioeconómicos frecuentemente requiere la integración de fuentes de datos con distinta periodicidad. Un caso representativo es la combinación de registros administrativos mensuales con estimaciones poblacionales disponibles únicamente en frecuencia anual.

Este trabajo surge a partir del estudio de datos publicados por la Administración Nacional de la Seguridad Social (ANSES), en particular aquellos vinculados a la cobertura de la Asignación Universal por Hijo (AUH) y la Asignación por Embarazo para Protección Social (AxE). En este contexto, la utilización de un denominador poblacional adecuado resulta de utilidad para la correcta interpretación de los indicadores.

El principal desafío técnico radica en la **desincronización de frecuencias**, donde la población total —publicada anualmente por el Banco Mundial— debe ser adaptada a una escala mensual. Una aproximación simplificada consiste en replicar el valor anual en cada mes; sin embargo, este enfoque introduce discontinuidades artificiales y puede distorsionar el análisis de tendencias.

Frente a este problema, el presente trabajo evalúa distintos métodos de interpolación y suavizado, con el objetivo de construir series mensuales consistentes y comparables. En particular, se propone analizar el impacto de cada metodología sobre los indicadores derivados, introduciendo el concepto de **materialidad del error** como criterio para determinar la relevancia práctica de las diferencias observadas.

La contribución pretendida al preparar el presente estudio radica en la comparación sistemática de estos enfoques y en la propuesta de un criterio metodológico que permita mejorar la calidad analítica y la auditabilidad de las series utilizadas en estudios socioeconómicos.
