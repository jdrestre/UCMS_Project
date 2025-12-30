# MANUAL DE OPERACIONES UCMS (Sistema de Gestión de Costos)
**Versión del Sistema:** v2.3.0
**Fecha:** 30-Dic-2025
**Propósito:** Definir los protocolos de reacción, arquitectura de datos y mantenimiento.

---

### 1. ARQUITECTURA DE DATOS (MODELO CORE + VERTICAL)

**A. BLOQUE A (CORE - TABLA MAESTRA):**
* **Objetivo:** Consolidación Financiera (22 Columnas).
* **Regla de la Fila Total (CONDICIONAL):** Obligatoria para EPM (Multiservicio), prohibida para Tigo (Monoservicio).

**B. BLOQUE B (VERTICAL - EXTENSIÓN TÉCNICA):**
* **Objetivo:** Auditoría Técnica Profunda.
* **Estrategia de Blindaje (Triángulo de Seguridad):**
    1.  **Hard Fields:** Datos físicos inmutables (Medidores, Lecturas).
    2.  **Structured Fields:** Desglose de tarifa.
    3.  **Flexible Fields (JSON):** Notas y regulaciones.

**(NUEVO v2.3) ESTRATEGIA DE SUBSIDIOS Y CONTRIBUCIONES:**
El sistema debe ser agnóstico al estrato socioeconómico.
* **Estratos 1, 2, 3:** Generan `Subsidios` (Valores negativos que restan a la factura).
* **Estratos 5, 6:** Generan `Contribuciones` (Valores positivos que suman a la factura).
* **Protocolo:** La columna `Valor_Subsidio` del Bloque B almacena el valor absoluto con su signo matemático correspondiente.

---

### 2. PROTOCOLOS DE MANTENIMIENTO Y ACTUALIZACIÓN

#### A. PROTOCOLO DE ACTUALIZACIÓN DIFERENCIAL
* **Principio de Continuidad:** Al actualizar un PROMPT, basarse siempre en la versión estable anterior. Nunca sobrescribir sin leer primero la lógica existente.

#### B. ESTÁNDAR REGIONAL (COLOMBIA)
* **Formato Numérico:** El sistema debe entregar decimales con COMA (`,`) para compatibilidad directa con Google Sheets en configuración regional Colombia. Los separadores de miles están prohibidos.

#### C. PROTECCIÓN DE TIPOS DE DATOS
* El uso del apóstrofe (`'`) al inicio de campos de ID y Periodo es obligatorio para evitar que el software de hoja de cálculo altere el dato (ej: convertir texto a fecha).

---

### 3. CATÁLOGO DE VERSIONES ESTABLES
* **GEM Admin:** v2.3.0
* **EPM Spoke:** v2.3.0 (Soporte Estrato 6 + Mapeo Gas).
* **Tigo Spoke:** v2.1.0 (Pendiente actualización a estándar v2.3.0).
* **Afinia / Surtigas:** v2.1.0 (Pendiente actualización a estándar v2.3.0).
