# ⚡ UCMS - Utility Cost Management System

> **Sistema de Auditoría Forense de Servicios Públicos basado en IA Modular Dinámica.**
> *Versión del Sistema: v2.6.0 (Granularidad Absoluta y Arquitectura Bicapa)*

---

## 🚀 El Sistema UCMS
El **Utility Cost Management System (UCMS)** es un ecosistema de ingeniería de datos diseñado para la extracción, normalización y auditoría técnica de facturas de servicios públicos complejos. A diferencia de un extractor convencional, el UCMS opera como un sistema modular que separa las reglas de negocio globales de la lógica específica de cada proveedor.

### 🏗️ Arquitectura del Sistema: Global vs. Específico

El éxito de la **v2.6.0** radica en la división clara de responsabilidades:

#### 1. Capa Global (Core System)
Es el núcleo del sistema que garantiza la integridad de la Base de Datos Maestra. Define:
* **Estándar Universal de Salida:** Matriz unificada de **76 columnas**.
* **Protocolos de Integridad:** Uso de apóstrofes (`'`) para protección de IDs, coma decimal (`,`) para compatibilidad regional y **Relleno Técnico (0,00)** para estabilidad estructural.
* **Glosario y Operaciones:** Definiciones técnicas unificadas y manual de mantenimiento.
* **Ubicación:** `/00_CONTEXTO`, `/01_ESTANDARES`, `/03_OPERACIONES`.

#### 2. Capa Específica (GEM Spokes)
Son módulos de inteligencia personalizada para cada Proveedor (GEM). Definen:
* **Lógica de Negocio Local:** Mapeo de términos específicos (ej. Gas Compra = Generación).
* **Granularidad Absoluta:** Captura de datos técnicos profundos en las columnas **43 a 74** (ej. IDs dinámicos de Gas o desglose de Toneladas en Aseo).
* **Protocolo OJF:** Instrucciones de inspección visual siguiendo el orden físico de la factura.
* **Ubicación:** `/02_SPOKES_PROMPTS`.

---

## 📈 Estado del Repositorio

El sistema se encuentra en fase de despliegue de **Alta Densidad**. El Spoke EPM es actualmente el modelo de referencia para la migración del resto de la arquitectura.

| Módulo (Spoke) | Tipo de Servicio | Versión | Estado | Nivel de Detalle |
| :--- | :--- | :--- | :--- | :--- |
| **EPM** | Multiservicio | **v2.6.0** | 🟢 **PRODUCCIÓN** | Granularidad Absoluta (76 Cols) |
| **ACUACAR** | Aguas | v2.1.0 | 🟠 **LEGACY** | Pendiente Migración v2.6.0 |
| **AFINIA** | Energía | v2.1.0 | 🟠 **LEGACY** | Pendiente Migración v2.6.0 |
| **SURTIGAS** | Gas | v2.1.0 | 🟠 **LEGACY** | Pendiente Migración v2.6.0 |
| **TIGO** | Telecom | v2.1.0 | 🟠 **LEGACY** | Pendiente Migración v2.6.0 |

---

## 📂 Estructura Orgánica del Proyecto

```text
UCMS_Project/
├── 00_CONTEXTO/            # Inteligencia de Negocio
│   ├── GLOSARIO_TERMINOS.md
│   └── HISTORIA_PROYECTO.md
├── 01_ESTANDARES/          # Reglas del Sistema (Global)
│   └── OUTPUT_UNIVERSAL.md  # Matriz de 76 Columnas
├── 02_SPOKES_PROMPTS/      # Motores de Extracción (Específico)
│   ├── PROMPT_EPM.md        # Referencia v2.6.0
│   └── ... (Spokes Legacy)
├── 03_OPERACIONES/         # Trazabilidad y Mantenimiento
│   ├── CHANGELOG_ERRORES.md
│   └── MANUAL_OPERACIONES_UCMS.md
├── 04_DATA/                # Repositorio de Datos
│   ├── DB_MAESTRA_UCMS.csv
│   └── SAMPLE/              # Facturas de muestra por GEM
└── README.md
