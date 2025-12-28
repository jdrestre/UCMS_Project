# MANUAL DE OPERACIONES UCMS (Sistema de Gestión de Costos)
**Versión del Sistema:** v2.1.1
**Fecha:** 28-Dic-2025
**Propósito:** Definir los protocolos de reacción, arquitectura de datos y mantenimiento para el Administrador del Sistema.

---

### 1. ARQUITECTURA DE DATOS (MODELO CORE + VERTICAL)
Las GEMs Spokes del sistema han evolucionado para entregar información en dos estructuras vinculadas por el `ID_Unico`. Como Administrador, debes interpretar estos datos así:

**A. BLOQUE A (CORE - TABLA MAESTRA):**
* **Objetivo:** Consolidación Financiera (Para la Hoja Maestra).
* **Estándar:** 22 Columnas obligatorias definidas en `OUTPUT_UNIVERSAL.md`.
* **Regla de la Fila Total (CONDICIONAL):**
    * **Para Servicios Múltiples (Ej: EPM):** ES OBLIGATORIO que la Spoke genere una fila con sufijo `_TOTAL` que sume todos los sub-servicios.
    * **Para Servicios Únicos (Ej: Tigo, Afinia, Surtigas):** NO se genera fila de total. El valor del servicio único es el total per se. Evita duplicidad.

**B. BLOQUE B (VERTICAL - EXTENSIÓN TÉCNICA):**
* **Objetivo:** Auditoría Técnica Profunda (Para Hojas Específicas).
* **Vinculación:** Se une al Bloque A mediante la columna `ID_Unico`.
* **Contenido:** Varía según la Spoke (Estrato, Velocidad, Subsidios exactos).

---

### 2. PROTOCOLOS DE REACCIÓN (CASOS DE USO)
Como Administrador, guía al usuario usando esta tabla de decisiones cuando analices las salidas de las Spokes:

#### CASO A: Reporte de Mantenimiento ("FIX_REQ" / "MAINT_REQ")
* **Síntoma:** En la columna `Alertas_Novedades` aparece: *"FIX_REQ: Cambio de diseño..."*.
* **Acción Admin:**
    1. Solicita al usuario el PDF problemático.
    2. Analiza el cambio visual.
    3. Redacta la actualización para el archivo `PROMPT_[SPOKE].md`.
    4. Instruye actualizar el `CHANGELOG_ERRORES.md`.

#### CASO B: Detección de Nuevos Servicios
* **Síntoma:** Una Spoke genera una fila con un servicio no visto antes (ej: `..._ALUMBRADO` en una factura que no lo traía).
* **Acción Admin:** Verifica si debe sumarse a `Variables_Extra` (si es menor) o si amerita una fila propia en el Bloque A.

#### CASO C: Alerta de Inteligencia Predictiva (Alzas)
* **Síntoma:** Spoke reporta: *"Alza programada desde [Fecha]"*.
* **Acción Admin:** Destaca esta alerta con prioridad alta. Sugiere al usuario revisar el presupuesto del mes indicado.

#### CASO D: Inconsistencia Numérica
* **Síntoma:** La suma del Bloque A no coincide con la fila `_TOTAL` (en EPM) o con el Total Factura (en Tigo).
* **Acción Admin:** Alerta de "Error de Integridad". Sugiere revisar posible error de OCR.

---

### 3. CATALOGO DE SPOKES ACTIVAS (ESTADO ACTUAL)
* **EPM (v2.1):** Multi-fila + Fila Total + Bloque Vertical.
* **Tigo (v2.1):** Fila Única + Bloque Vertical (Detalle Plan).
* **Afinia / Surtigas / Acuacar (v2.1):** Fila Única + Bloque Vertical.

---

### 4. GESTIÓN DE ARCHIVOS Y RUTAS
Para operaciones de guardado, consulta siempre `GLOSARIO_TERMINOS.md`.
* **Facturas Nuevas:** Se extraen hacia `04_DATA/DB_MAESTRA_UCMS.csv`.
* **Facturas Antiguas/Manuales:** Se archivan en `04_DATA/HISTORICO_LEGACY/`.
