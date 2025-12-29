# MANUAL DE OPERACIONES UCMS
**Versión del Sistema:** v2.1.3
**Fecha:** 29-Dic-2025

---

### 1. ARQUITECTURA DE DATOS
(Mantiene lógica Core + Vertical de la v2.1.1)

---

### 2. PROTOCOLOS DE MANTENIMIENTO Y ACTUALIZACIÓN (v2.1.3)

#### A. PROTOCOLO DE ACTUALIZACIÓN DIFERENCIAL (Lección Aprendida)
* **Principio de Continuidad:** Al actualizar un PROMPT de una Spoke, el GEM Admin debe leer la versión existente en el repositorio y proponer un "Patch" o cambio incremental.
* **Prohibición de Sobrescritura Ciega:** No se deben generar prompts desde cero si ya existe una versión funcional, para evitar la pérdida de reglas de negocio específicas ya validadas por el usuario.

#### B. ESTÁNDAR REGIONAL DE INTERFAZ
* El sistema opera por defecto para usuarios en **Colombia**.
* La salida de datos debe ser compatible con la configuración regional de Google Sheets (Coma decimal).

#### C. BLINDAJE DE DATOS (OBSERVACIÓN 2)
* Toda columna de tipo "Periodo" o "ID" debe ser precedida por un apóstrofe (`'`) para forzar el tratamiento como texto en hojas de cálculo y evitar que el software de terceros altere el dato (ej: convertir "SEP-2025" en una fecha de sistema).

---

### 3. CATÁLOGO DE VERSIONES ESTABLES
* **GEM Admin:** v2.1.3
* **EPM Spoke:** v2.1.3
* **Tigo Spoke:** v2.1.0 (Pendiente actualizar a estándar de coma decimal)
