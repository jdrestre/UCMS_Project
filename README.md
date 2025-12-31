# ⚡ UCMS - Utility Cost Management System

> **Sistema de Auditoría de Servicios Públicos basado en IA Modular Dinámica.**
> *Versión del Sistema: v2.5.1 (Estable - Foco en EPM & Cero Redundancia)*

---

## 📖 Visión General del Proyecto

El **UCMS** es un ecosistema de Agentes de IA (Spokes) especializado en la extracción forense, normalización y auditoría financiera de facturas de servicios públicos. 

En la versión **v2.5.1**, el sistema ha evolucionado hacia un modelo de **Bloque Único Dinámico**, donde la inteligencia de extracción se personaliza por proveedor, eliminando la redundancia de datos técnicos y garantizando que la información estructurada sea 100% analizable.

**Capacidades Actuales (v2.5.1):**
1.  **Arquitectura de Bloque Único:** Fusión de datos financieros y técnicos en una matriz plana de alta densidad.
2.  **Limpieza Técnica (No-Redundancia):** Eliminación de datos técnicos duplicados en el campo JSON para optimizar el peso de la base de datos.
3.  **Diferenciación de Estados:** Separación clara entre agentes en Producción (v2.5.1) y agentes Legacy pendientes de migración.
4.  **Auditoría de Conversión:** Captura de Constantes de Gas y Factores de Energía en la Columna 44 para análisis histórico.

---

## 🏗️ Arquitectura de Datos

El sistema opera bajo un núcleo de identidad común pero con extensiones técnicas adaptables:

### 1. Núcleo de Identidad (Global)
Las columnas 1 a 19 son estándar para todas las facturas y garantizan la trazabilidad del cliente, periodo y tipo de servicio.

### 2. Extensión Técnica Especializada (Spoke-Specific)
A partir de la columna 20, la matriz se adapta a la complejidad del proveedor. 
* **EPM (Piloto v2.5.1):** Matriz de 65 columnas con desglose de 6 servicios simultáneos.
* **Política de Datos:** Uso de la **Columna 44 (Const)** para valores técnicos críticos, excluyéndolos de la **Columna 65 (JSON)**.

---

## 🤖 Catálogo de Agentes (Spokes)

| Agente (Spoke) | Proveedor | Versión | Estado | Nivel de Soporte |
| :--- | :--- | :--- | :--- | :--- |
| **EPM** | Multiservicios | **v2.5.1** | 🟢 **PRODUCCIÓN** | Soporte Total (65 Cols / Cero Redundancia) |
| **ACUACAR** | Agua | v2.1.0 | 🟠 **LEGACY** | Pendiente Revisión y Migración v2.5 |
| **AFINIA** | Energía | v2.1.0 | 🟠 **LEGACY** | Pendiente Revisión y Migración v2.5 |
| **SURTIGAS** | Gas | v2.1.0 | 🟠 **LEGACY** | Pendiente Revisión y Migración v2.5 |
| **TIGO** | Telecom | v2.1.0 | 🟠 **LEGACY** | Pendiente Revisión y Migración v2.5 |

---

## 📂 Estructura del Repositorio (UCMS_Project)

```text
UCMS_Project/
├── 00_CONTEXTO
│   ├── GLOSARIO_TERMINOS.md
│   └── HISTORIA_PROYECTO.md
├── 01_ESTANDARES
│   └── OUTPUT_UNIVERSAL.md
├── 02_SPOKES_PROMPTS
│   ├── PROMPT_ACUACAR.md
│   ├── PROMPT_AFINIA.md
│   ├── PROMPT_EPM.md
│   ├── PROMPT_SURTIGAS.md
│   └── PROMPT_TIGO.md
├── 03_OPERACIONES
│   ├── CHANGELOG_ERRORES.md
│   └── MANUAL_OPERACIONES_UCMS.md
├── 04_DATA
│   ├── DB_MAESTRA_UCMS.csv
│   ├── HISTORICO_LEGACY
│   │   ├── ... (Archivos de soporte y bitácoras legacy)
│   └── SAMPLE
│       ├── ACUACAR/
│       ├── AFINIA/
│       ├── EPM/
│       ├── SURTIGAS/
│       └── TIGO_UNE/
└── README.md

## 🛠️ Protocolo de Mantenimiento v2.5.1

### Reglas Maestras Globales
1.  **Formato Universal:** Fechas en `DD/MM/YYYY` y decimales con **COMA (`,`)**. Prohibido el uso de puntos de miles.
2.  **Protección de IDs (EPM):** Todo Identificador debe iniciar con **Apóstrofe (`'`)** para preservar la integridad en Excel.
3.  **Integridad de Datos:** Si un dato es numérico y tiene una columna asignada, **no debe** aparecer en el JSON de la columna 65.

### Mejora Continua
El sistema evoluciona mediante la retroalimentación del Admin. Si se detecta ruido o redundancia, el Prompt de la Spoke debe ser refactorizado inmediatamente para mantener la higiene de la base de datos.
