# ⚡ UCMS - Utility Cost Management System

> **Sistema de Auditoría de Servicios Públicos basado en IA Modular.**
> *Versión del Sistema: v2.3.0 (Estable - Soporte Estrato Alto & Triángulo de Seguridad)*

---

## 📖 Visión General del Proyecto

El **UCMS** es un ecosistema de Agentes de IA (GEMs) diseñado para la extracción, normalización y auditoría financiera de facturas de servicios públicos.

Su arquitectura **Hub & Spoke** permite procesar documentos no estructurados (PDFs de diferentes proveedores) y convertirlos en bases de datos relacionales estrictas, agnósticas al formato visual de la factura.

**Capacidades Actuales (v2.3.0):**
1.  **Auditoría Financiera Global:** Consolidación de costos en una tabla maestra estándar.
2.  **Blindaje Técnico:** Extracción profunda de componentes tarifarios (Generación, Transmisión, etc.) y lectura de medidores físicos.
3.  **Soporte Socioeconómico Completo:** Manejo matemático de Subsidios (Estratos 1-3) y Contribuciones/Sobrecostos (Estratos 5-6 y Comerciales).

---

## 🏗️ Arquitectura de Datos (Doble Bloque)

El sistema opera bajo dos principios de inmutabilidad de datos:

### 1. Bloque A: Core Financiero (Horizontal)
Tabla maestra de **22 Columnas** estandarizada para todos los servicios (Energía, Agua, Internet, Gas).
* **Objetivo:** Comparabilidad financiera y flujo de caja.
* **Regla:** Idéntica estructura para EPM, Tigo, Afinia, etc.

### 2. Bloque B: Extensión Técnica (Vertical)
Tabla de detalle específica por proveedor, diseñada bajo la estrategia de **"Triángulo de Seguridad"** para evitar obsolescencia por cambios de formato:
* **Nivel 1 (Hard Fields):** Datos físicos auditorables (Seriales de medidor, Lecturas anterior/actual).
* **Nivel 2 (Structured Fields):** Desglose tarifario en columnas explícitas (Comp. Generación, Distribución, Tasas).
* **Nivel 3 (Flexible Fields):** JSON para captura de textos regulatorios, justificaciones de desviación y alertas visuales.

---

## 🤖 Catálogo de Agentes (Spokes)

Estado actual de los módulos de extracción:

| Agente (Spoke) | Proveedor | Versión | Estado | Capacidades |
| :--- | :--- | :--- | :--- | :--- |
| **EPM** | Multiservicios | **v2.3.0** | 🟢 **Estable** | Soporte Estrato 6, Mapeo de Gas, JSON Regulatorio. |
| **Tigo** | Telecom | v2.1.0 | 🟠 *Legacy* | Pendiente actualización a estándar v2.3. |
| **Afinia** | Energía (Costa) | v2.1.0 | 🟠 *Legacy* | Pendiente actualización a estándar v2.3. |
| **Surtigas** | Gas (Costa) | v2.1.0 | 🟠 *Legacy* | Pendiente actualización a estándar v2.3. |
| **Acuacar** | Agua (Costa) | v2.1.0 | 🟠 *Legacy* | Pendiente actualización a estándar v2.3. |

---

## 📂 Estructura del Repositorio

* **`00_CONTEXTO/`**: Memoria técnica.
    * `GLOSARIO_TERMINOS.md`: Definiciones oficiales y lógica de negocio.
    * `HISTORIA_PROYECTO.md`: Registro de decisiones arquitectónicas.
* **`01_ESTANDARES/`**: La "Constitución" del sistema.
    * `OUTPUT_UNIVERSAL.md`: Definición estricta de columnas y formatos.
* **`02_SPOKES_PROMPTS/`**: Cerebros autónomos.
    * Contiene los archivos `.md` que actúan como "System Prompt" para cada IA.
    * *Nota v2.3:* Los prompts son autónomos y no requieren instrucciones externas.
* **`03_OPERACIONES/`**: Mantenimiento y Análisis.
    * `METRICAS_KPI.md`: Fórmulas de análisis financiero por Spoke.
    * `MANUAL_OPERACIONES_UCMS.md`: Protocolos de actualización y contingencia.
    * `CHANGELOG_ERRORES.md`: Bitácora de versionamiento.
* **`04_DATA/`**: (Ignorado por Git) Almacén de PDFs crudos y CSVs generados.

---

## 🛠️ Protocolo de Mantenimiento

### Reglas de Actualización (v2.3)
1.  **Principio de Autonomía:** Al actualizar una Spoke, toda la lógica debe residir en su archivo `PROMPT_[NOMBRE].md`. No depender de instrucciones en la configuración del modelo.
2.  **Validación Regional:** Todo dato numérico debe usar **COMA (`,`)** decimal. Todo ID debe iniciar con **Apóstrofe (`'`)**.
3.  **Integridad Histórica:** No sobrescribir reglas de negocio probadas sin consultar `HISTORIA_PROYECTO.md`.

### Cómo reportar errores
Si una factura cambia de diseño y la extracción falla:
1.  Identificar si es un error de **Lectura** (OCR fallido) o de **Lógica** (Columna nueva).
2.  Actualizar el Prompt correspondiente en `02_SPOKES_PROMPTS/`.
3.  Registrar el cambio en `CHANGELOG_ERRORES.md`.
