# 📊 Análisis de Órdenes de Instalación - Dashboard Operacional

Este Dashboard de Power BI analiza y optimiza el proceso de instalaciones de servicios mediante el seguimiento de órdenes cerradas, performance de técnicos y cumplimiento de SLA. Se trata de una versión anonimizada y optimizada basada en métricas operacionales reales del sector telecomunicaciones.

**Análisis operacional en tiempo real para mejorar la eficiencia de instalaciones y gestión de recursos técnicos**

<img width="1447" height="814" alt="image" src="https://github.com/user-attachments/assets/dfb9f1c0-8bf4-4b3d-af76-e59f16e1f66d" />

## 📌 Objetivo del Proyecto

El objetivo de este proyecto es analizar el desempeño operacional de instalaciones de servicios durante el período del **1 al 7 de diciembre de 2025**, identificando:

* Calidad Operativa: Órdenes exitosas vs. no exitosas y sus causas raíz.

* Gestión de Tiempos: Cumplimiento de SLA (Service Level Agreement) y detección de órdenes críticas.

* Performance Técnica: Categorización de técnicos y contratistas mediante un sistema de evaluación multi-criterio.

* Inteligencia Geográfica: Patrones de concentración y problemas de infraestructura por región y localidad.

El proyecto combina análisis operacional, KPIs de gestión de recursos humanos y métricas de calidad de servicio para traducir datos crudos de órdenes de trabajo en **insights accionables** mediante un dashboard interactivo desarrollado en **Power BI**.

**El foco no está solo en "cuántas órdenes se cerraron", sino en cómo se cerraron, quiénes las realizaron, cuánto tardaron y qué tan estables son los resultados.**

---

## 🧠 Preguntas Clave que Responde el Dashboard

¿Cuál es la salud de la operación? (Tasa de éxito del 87.58%).

¿Qué técnicos superan los estándares? (Sistema de categorización por performance).

¿Dónde están los cuellos de botella? (Localidades con mayor incumplimiento de SLA).

¿Por qué fallan las instalaciones? (Matriz de motivos de cierre con indicadores visuales).

## 🗂️ Arquitectura de Datos

### Dataset y Modelado
Tabla Principal: INST CANCELADAS 1-12 A 7-12 (12,527 registros).

Modelo de Datos: Se utiliza un modelo de tabla plana para fines de demostración en portfolio. El proyecto está diseñado contemplando la lógica de un Esquema en Estrella (Star Schema) para escalabilidad futura, minimizando el overhead de escaneo y optimizando el motor de búsqueda de Power BI.

Organización: Métricas DAX agrupadas en Carpetas de Visualización (Calidad, Cantidad, Comparación, Categorización) para garantizar la mantenibilidad del proyecto.

### Métricas DAX Destacadas
Sistema de Categorización: Lógica compleja que evalúa simultáneamente % de Éxito, Productividad vs. Promedio y Cumplimiento de SLA.

Métricas Comparativas: Promedio nacional vs. Localidad y desempeño de técnico vs. media del equipo.

Variación Temporal: Cálculo de variación día sobre día (DoD) para detectar anomalías operacionales.

## 🔧 Herramientas Utilizadas
Power BI Desktop

Power Query (ETL): Limpieza, tipado y estandarización de datos.

DAX Avanzado: Filtros cruzados, contextos complejos (CALCULATE, ALL) y lógica de categorización.

## 📊 Decisiones de Diseño y UX

### 🎨 Jerarquía Visual y Color
Paleta de Colores: Se utilizó el amarillo corporativo como color de acento en KPIs y encabezados para mantener la identidad de marca. Para los gráficos de densidad (Treemap), se optó por una paleta de tonos fríos y neutros (Azules/Grises) para evitar la fatiga visual y separar claramente la información de volumen de las alertas operacionales.

Matriz de Motivos: Implementación de iconos (✅❌⚠️) para permitir una lectura 3x más rápida de los patrones de fallo.

### 🗺️ Treemap con Jerarquía Geográfica
En lugar de un mapa estático, se implementó un Treemap interactivo con jerarquía:

Región

Provincia

Localidad
Esto permite un análisis de "Drill-down" para identificar concentraciones de carga y problemas de red en zonas específicas de manera más precisa que una visualización geográfica tradicional.

### ⏱️ Análisis de Anomalías
Nota de Contexto (Domingo 07-12): Se identificó y señalizó una caída en el volumen de órdenes (17 registros). Se añadió una notación aclaratoria: este descenso responde a la guardia mínima del área de Mesa de Despacho y no a una falla de carga o pérdida de datos.

**Código de colores:**
- 🔴 ❌ = Ordenes canceladas por encima del promedio
- 🟡 ⚠️ = Ordenes canceladas cerca de superar el promedio
- 🟢 ✅ = Ordenes canceladas por debajo del promedio

## 🎯 Decisiones de Diseño Críticas

### **❓ ¿Por qué NO incluí un mapa geográfico de Argentina?**

**Evaluación realizada:**
- ✅ **Gráfico de barras por región** es más útil para comparaciones numéricas
- ✅ **Jerarquía drill-down** aporta más insight analítico que un mapa estático
- ✅ **Tooltips geográficos** contextualizan mejor las diferencias regionales
- ❌ Ocupa mucho espacio sin aportar valor analítico adicional

**Resultado:** Prioricé **utilidad analítica** sobre estética geográfica.

---

### **❓ ¿Por qué un sistema de categorización de técnicos?**

**Problema identificado:** 
Un simple "% de éxito" no cuenta la historia completa. Un técnico puede tener 100% de éxito pero:
- Estar fuera de SLA en el 50% de órdenes
- Tener baja productividad (pocas órdenes)
- Generar órdenes críticas (>10 días)

**Solución:** Sistema **multi-criterio** que evalúa:
1. Calidad (% éxito)
2. Cumplimiento de SLA
3. Productividad
4. Criticidad de demoras

**Resultado:** Categorización más **justa y accionable** para gestión de RRHH.

---

### **❓ ¿Por qué métricas de "Variación Día a Día" y no solo totales?**

**Razón:** Identificar **anomalías diarias** que requieren investigación:
- Día con -98.82% de variación → Domingo (operación reducida) ✅ Normal
- Día con +16.57% de variación → Aumento de demanda ⚠️ Investigar causa

**Beneficio:** Permite **reaccionar proactivamente** ante cambios operacionales.

---

### **❓ ¿Por qué separar órdenes "Fuera de SLA" y "Críticas"?**

**Razón:** Diferentes niveles de urgencia requieren diferentes acciones:

| Categoría | Días | % del Total | Acción Requerida |
|-----------|------|-------------|------------------|
| **Dentro de SLA** | ≤5 días | ~85% | ✅ Seguimiento normal |
| **Fuera de SLA** | 6-10 días | ~12% | ⚠️ Atención gerencial |
| **Críticas** | >10 días | ~3% | 🚨 Escalamiento urgente |

**Resultado:** Priorización clara de recursos de supervisión.

---

## 🚀 Insights Principales

1 - Performance de Red: Tasa de éxito sólida del 87.58% con un promedio de cierre de 2.94 días, cumpliendo el SLA estándar (5 días).

2 - Gestión de Talento: Identificación de 7 Técnicos Sobresalientes (100% éxito + alta productividad). El sistema permite detectar rápidamente al 4% del personal en situación crítica para re-capacitación.

3 - Eficiencia de Contratistas: El Contratista 5 lidera en volumen (1,157 órdenes), permitiendo evaluar la capacidad instalada de los proveedores externos.

4 - Causas de Fallo: Los motivos 5 y 4 representan los principales puntos de fricción, sugiriendo la necesidad de una validación previa de datos más rigurosa.

### **👷 Gestión de Técnicos**
- **5.3% de técnicos son "Excelente" o superior** (47 de 887 técnicos)
- **27.73% requieren mejora activa** (246 técnicos en "A mejorar")
- **5.4% en situación crítica** (48 técnicos entre "Situación grave" y "Muy grave")
- **Concentración de carga:** Algunos técnicos manejan casi 3 veces más volumen de órdenes que el promedio

**🎯 Acción recomendada:** Redistribuir carga y capacitar al 27.73% en categoría "A mejorar" antes de que empeoren.

### **⏱️ Cumplimiento de SLA**
- **~15% de órdenes exceden el SLA** (>5 días)
- **Localidades críticas:** LOS POLVORINES (43 días promedio), CAMPANA (26.5 días)
- **Causa principal:** Problemas físicos de infraestructura (postes, capacidad)?

**🎯 Acción recomendada:** Invertir en infraestructura en localidades con alto promedio de demora.

### **🏢 Performance de Contratistas**
- **CONTRATISTA 5  :** 1157 órdenes, 88.94% éxito, promedio 3.31 días ✅ Top performer
- **CONTRATISTA 1:** 18 órdenes, 136.45% demora de días de cierre vs promedio nacional ⚠️ Requiere atención
- **Concentración de riesgo:** 3 contratistas manejan el 24% del volumen total

**🎯 Acción recomendada:** Diversificar cartera de contratistas para reducir riesgo operacional.
