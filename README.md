# 📊 Análisis de Órdenes de Instalación Canceladas - Dashboard Operacional

Dashboard de Power BI diseñado para analizar y optimizar el proceso de instalaciones de servicios mediante el seguimiento de órdenes canceladas, performance de técnicos y cumplimiento de SLA.

**Análisis operacional en tiempo real para mejorar la eficiencia de instalaciones y gestión de recursos técnicos**

<img width="1463" height="813" alt="image" src="https://github.com/user-attachments/assets/edeb0761-ca64-467a-aee6-d7f00fee4624" />


## 📌 Objetivo del Proyecto

El objetivo de este proyecto es analizar el desempeño operacional de instalaciones de servicios durante el período del **1 al 7 de diciembre de 2025**, identificando:

- **Órdenes exitosas vs no exitosas** y sus causas raíz
- **Tiempos de cierre** y cumplimiento de SLA (Service Level Agreement)
- **Performance de técnicos y contratistas** mediante un sistema de categorización multi-criterio
- **Patrones geográficos** de concentración y problemas de instalación
- **Motivos de cierre** para priorizar mejoras operacionales

El proyecto combina análisis operacional, KPIs de gestión de recursos humanos y métricas de calidad de servicio para traducir datos crudos de órdenes de trabajo en **insights accionables** mediante un dashboard interactivo desarrollado en **Power BI**.

**El foco no está solo en "cuántas órdenes se cerraron", sino en cómo se cerraron, quiénes las realizaron, cuánto tardaron y qué tan estables son los resultados.**

---

## 🧠 Preguntas Clave que Responde el Dashboard

El dashboard fue diseñado para responder las siguientes preguntas operacionales:

### **📈 Performance General**
- ¿Cuál es el porcentaje de éxito de las instalaciones?
- ¿Cuántas órdenes se cierran diariamente y cómo varía día a día?
- ¿Cuál es el promedio de días para cerrar una orden?

### **⏱️ Cumplimiento de SLA**
- ¿Qué porcentaje de órdenes excede el tiempo de SLA establecido (5 días)?
- ¿Cuántas órdenes son críticas (>10 días sin cerrar)?
- ¿Qué localidades tienen mayor incumplimiento de SLA?

### **👷 Gestión de Recursos**
- ¿Qué técnicos tienen mejor performance (categorización)?
- ¿Existe concentración de carga en ciertos técnicos?
- ¿Qué contratistas tienen mejor tasa de éxito?
- ¿Cuántos técnicos están en cada categoría de desempeño?

### **🗺️ Análisis Geográfico**
- ¿Qué provincias y localidades concentran más órdenes?
- ¿Existen zonas con mayor tasa de fallos?
- ¿Hay diferencias en tiempos de cierre por región?

### **❌ Causas de Fallos**
- ¿Cuáles son los motivos principales de órdenes no exitosas?
- ¿Qué problemas se repiten con mayor frecuencia?
- ¿Hay patrones temporales en los tipos de fallo?

---

## 🗂️ Dataset Utilizado

El dataset contiene información operacional detallada de órdenes de instalación, con las siguientes características:

### **Tabla Principal: "INST CANCELADAS 1-12 A 7-12 (2)"**
**36 columnas** | **12,577 registros** | **Período: 1-7 de diciembre de 2025**

#### **Dimensiones clave:**
- **Identificación:** NRO. OT, NRO. SERVICIO, NRO. CLIENTE
- **Temporal:** FECHA CREACIÓN, FECHA CIERRE, DÍAS DE DIF. E/ CREAC. Y CIERRE
- **Geográfica:** PROVINCIA, LOCALIDAD, DOMICILIO
- **Recursos:** TÉCNICO, CONTRATISTA, ASESOR
- **Operacional:** ESTADO, MOTIVO CIERRE, TECNOLOGÍA, TIPO DE SERVICIO
- **Gestión:** REINC. (reincidencia), GARANTÍA, SEGMENTO

### **Tabla de Métricas: "Metricas calculadas"**
**25+ medidas DAX** organizadas por categoría:

#### **Métricas Base:**
- Total órdenes, Total órdenes exitosas, Total órdenes no exitosas
- Porcentaje de éxito, Promedio días de cierre

#### **Métricas de SLA:**
- Órdenes fuera de SLA (>5 días)
- % Órdenes fuera de SLA
- Órdenes críticas (>10 días)
- % Órdenes críticas

#### **Métricas de Performance:**
- Promedio órdenes por técnico
- Ranking de técnicos por % éxito
- Concentración % (distribución de carga)
- Variación día a día (DoD)

#### **Métricas de Categorización:**
- Categoría Técnico (6 niveles: Sobresaliente, Excelente, Adecuado, A mejorar, Situación grave, Muy grave)
- Conteo por categoría (Técnicos Sobresalientes, Técnicos Excelentes, etc.)
- Tasa de reincidencia

#### **Métricas Comparativas:**
- Promedio días de cierre nacional
- Promedio nacional vs localidad
- Promedio cantidad por técnico vs total

---

## 🔧 Herramientas y Tecnologías Utilizadas

### **Power BI Desktop**

**Power Query (ETL):**
- Limpieza de datos y transformación de formatos
- Creación de columnas calculadas (DIAS DE DIF., FECHA CIERRE S/HORA)
- Estandarización de nombres (Text.Proper)
- Manejo de tipos de datos

**DAX (Data Analysis Expressions):**
- Cálculo de variación interanual y día sobre día
- Métricas agregadas con contextos de filtro complejos
- Sistema de categorización multi-criterio
- Rankings dinámicos y métricas de comparación
- Manejo de contextos con CALCULATE, REMOVEFILTERS, ALL, ALLEXCEPT

**Modelado de Datos:**
- Modelo orientado a análisis operacional
- Jerarquías geográficas (Provincia → Localidad → Calle)
- Separación de medidas en tabla independiente
- Optimización para performance con filtros cruzados

---

## 📊 Estructura del Dashboard (🔹) y Decisiones de Diseño (👉)

## 🔹 **KPIs Principales (Cards Superiores)**

En la parte superior del dashboard se presentan indicadores de contexto inmediato:

- **Órdenes Cerradas:** Total del período analizado
- **Órdenes Exitosas:** Cantidad de instalaciones completadas correctamente
- **Órdenes No Exitosas:** Fallos que requieren análisis
- **Porcentaje de Éxito:** Métrica principal de calidad (87.55%)

👉 **Decisión de diseño:** Estos KPIs funcionan como **punto de referencia** para interpretar todos los demás gráficos. El color amarillo corporativo (#F39C12) refuerza la identidad visual y mantiene coherencia en todo el dashboard.

---

## 🔹 **Evolución Temporal (Gráfico de Línea)**

**Gráfico:** Cantidad de OT cerradas por día  
**Período:** 7 días (1-7 de diciembre)

👉 **Por qué este gráfico:**
- Identifica **patrones semanales** (ej: caída drástica el día 7 = domingo)
- Detecta **anomalías diarias** para investigación
- Permite evaluar **capacidad operativa** por día

**Tooltip interactivo incluye:**
- Total de órdenes del día
- Promedio semanal (1,796.71 órdenes/día)
- Variación vs promedio semanal
- Promedio de días de cierre
- Fecha exacta

---

## 🔹 **Matriz de Motivos de Cierre (Heatmap con Iconos)**

**Visualización:** Tabla matriz con iconos de estado (✅❌⚠️)  
**Dimensiones:** Motivo de cierre × Día de la semana

👉 **Por qué esta visualización:**
- Los **iconos visuales** permiten detectar patrones sin leer números
- Identificar **días críticos** con alta concentración de fallos
- Entender **causas raíz** de órdenes no exitosas:
  - Cliente desiste del servicio
  - Domicilio erróneo
  - Cliente ausente
  - Duplicidad de carga
  - Sin permisos linderos
  - Cliente posterga fecha

**Código de colores:**
- 🔴 ❌ = Ordenes canceladas por encima del promedio
- 🟡 ⚠️ = Ordenes canceladas cerca de superar el promedio
- 🟢 ✅ = Ordenes canceladas por debajo del promedio

---

## 🔹 **Performance de Técnicos (Tabla Multi-Columna)**

**Columnas principales:**
- Técnico
- Porcentaje de éxito
- **Categoría** (Sobresaliente, Excelente, Adecuado, etc.)
- Total de órdenes
- Promedio órdenes por técnico
- Promedio cantidad por técnico vs total
- % Órdenes fuera de SLA
- % Órdenes críticas

👉 **Sistema de Categorización (Multi-Criterio):**

El sistema evalúa técnicos en **4 dimensiones simultáneas:**
1. **% Éxito** (≥100%, ≥85%, ≥70%, etc.)
2. **Productividad vs Promedio** (>0% = sobre promedio)
3. **Cumplimiento SLA** (≤20%, ≤25%, ≤35%)
4. **Órdenes Críticas** (≤20%, ≤25%, ≤35%)

**6 Categorías resultantes:**
- 🏆 **Sobresaliente** (32 técnicos): 100% éxito + 0% fuera SLA + alta productividad
- ⭐ **Excelente** (288 técnicos): 100% éxito + ≤20% fuera SLA
- ✔️ **Adecuado** (330 técnicos): ≥85% éxito + SLA aceptable
- ⚠️ **A Mejorar** (162 técnicos): ≥70% éxito pero requiere mejoras
- 🟠 **Situación Grave** (7 técnicos): Bajo desempeño persistente
- 🔴 **Muy Grave** (29 técnicos): <50% éxito o >50% fuera SLA

👉 **Valor de negocio:**
- Identificar **top performers** para reconocimiento/bonificación
- Detectar técnicos que requieren **capacitación urgente**
- **Redistribuir carga** entre técnicos sobrecargados
- **Tomar decisiones** sobre renovaciones de contrato

---

## 🔹 **Distribución Geográfica (Múltiples Visualizaciones)**

### **Gráfico de Barras: Cantidad de OT por Localidad**
Top 10 localidades con mayor volumen de órdenes

### **Jerarquía Geográfica (para Treemap o Drill-down):**
Provincia → Localidad → Calle

👉 **Por qué jerarquía geográfica:**
- Permite **drill-down interactivo** de nivel macro a micro
- Identifica **concentración de problemas** en calles específicas
- Detecta **problemas de infraestructura** (ej: múltiples órdenes fallidas en la misma calle = problema de red)

**Tooltip geográfico incluye:**
- Promedio días de cierre de la localidad
- Promedio nacional (2.86 días)
- % diferencia vs nacional
- Casos atípicos explicados (ej: LOS POLVORINES con 43 días promedio debido a problemas físicos)

---

## 🔹 **Top Asesores y Contratistas (Gráficos de Barras Horizontales)**

**Métricas por Asesor:**
- Cantidad de órdenes cerradas
- Ranking de productividad

**Métricas por Contratista:**
- Cantidad de órdenes
- % Éxito
- Tooltip con análisis comparativo:
  - Promedio días de cierre del contratista
  - Promedio nacional
  - % diferencia vs total

👉 **Uso operacional:**
- Evaluar **contratos y renovaciones**
- Identificar **mejores proveedores**
- Detectar contratistas con **bajo desempeño** para renegociación o cambio

---

## 🎯 Decisiones de Diseño Críticas

### **❓ ¿Por qué NO incluí un mapa geográfico de Argentina?**

**Evaluación realizada:**
- ✅ **Gráfico de barras por localidad** es más preciso para comparaciones numéricas
- ✅ **Jerarquía drill-down** aporta más insight analítico que un mapa estático
- ✅ **Tooltips geográficos** contextualizan mejor las diferencias regionales
- ❌ Un mapa solo confirmaría lo obvio (Córdoba y Bs. As. dominan)
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
- Día con -96.89% de variación → Domingo (operación reducida) ✅ Normal
- Día con +16.77% de variación → Aumento de demanda ⚠️ Investigar causa

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

### **❓ ¿Por qué iconos (✅❌⚠️) en la matriz de motivos?**

**Razón:** Lectura visual **3x más rápida** que interpretar números o colores:
- ❌ (rojo) = problema identificado instantáneamente
- ✅ (verde) = no requiere atención
- ⚠️ (amarillo) = monitorear

**Beneficio:** Supervisores pueden escanear la matriz en **segundos** y detectar patrones sin leer cada celda.

---

## 🚀 Insights Principales y Conclusiones

### **📊 Performance General**
- **Tasa de éxito: 87.55%** (11,011 exitosas de 12,577 totales)
- **Promedio de cierre: 2.86 días** (por debajo del SLA de 5 días)
- **Variación diaria: -19% a +17%** (con caída esperada los domingos)

### **👷 Gestión de Técnicos**
- **35% de técnicos son "Excelente" o superior** (320 de 909 técnicos)
- **18% requieren mejora activa** (162 técnicos en "A mejorar")
- **4% en situación crítica** (36 técnicos entre "Situación grave" y "Muy grave")
- **Concentración de carga:** Algunos técnicos manejan 3 veces más volumen de órdenes que el promedio

**🎯 Acción recomendada:** Redistribuir carga y capacitar al 18% en categoría "A mejorar" antes de que empeoren.

### **⏱️ Cumplimiento de SLA**
- **~15% de órdenes exceden el SLA** (>5 días)
- **Localidades críticas:** LOS POLVORINES (43 días promedio), CAMPANA (26.5 días)
- **Causa principal:** Problemas físicos de infraestructura (postes, capacidad)?

**🎯 Acción recomendada:** Invertir en infraestructura en localidades con alto promedio de demora.

### **❌ Causas Raíz de Fallos**
**Top 3 motivos de cierre negativo:**
1. **Cliente desiste del servicio** (330 órdenes)
2. **Domicilio erróneo** (293 órdenes)
3. **Cliente ausente** (276 órdenes)

**Total de órdenes no exitosas:** 1,566 (12.45%)

**🎯 Acción recomendada:**
- Implementar **validación de domicilio** antes de enviar técnico
- **Confirmar cita** 24h antes para reducir ausencias
- Analizar causas de desistimiento (precio, competencia, demora)

### **🗺️ Concentración Geográfica**
- **Córdoba concentra el 9.63%** del total de órdenes (1,211 órdenes)
- **Top 3 localidades:** Córdoba, Rosario, Mar del Plata
- **Variabilidad regional:** Promedio de demora varía de 1.4 a 43 días según localidad

### **🏢 Performance de Contratistas**
- **NETMED:** 806 órdenes, 90.94% éxito, promedio 2.50 días ✅ Top performer
- **TECHMOVIL:** 1,159 órdenes, -12.61% vs promedio nacional ⚠️ Requiere atención
- **Concentración de riesgo:** 3 contratistas manejan el 24% del volumen total

**🎯 Acción recomendada:** Diversificar cartera de contratistas para reducir riesgo operacional.
