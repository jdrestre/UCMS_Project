# MANUAL DE OPERACIONES UCMS (v2.5.1)
**Estado:** VIGENTE | **Referencia de Ejecución Directa para el Admin**

## 1. FLUJO OPERATIVO ESTÁNDAR
El proceso de extracción y auditoría sigue una secuencia de tres capas para garantizar la integridad de los datos:

1.  **Capa de Ingesta:** El usuario carga el documento PDF en la Spoke (GEM) correspondiente.
2.  **Capa de Extracción (Spoke):** La Spoke ejecuta su `PROMPT_*.md` específico. Su objetivo es mapear los datos a la matriz definida (Ej: 65 columnas para EPM).
3.  **Capa de Validación (Admin):** El Admin (IA) recibe la salida y valida el cumplimiento de las **REGLAS MAESTRAS (GLOBALES)** del archivo `OUTPUT_UNIVERSAL.md`.

---

## 2. CONTROL DE CALIDAD Y KPIs (AUDITORÍA ADMIN)
*El Admin utiliza estos indicadores para validar el éxito de cada operación y mitigar la saturación de datos:*

### 2.1 Eficacia de Limpieza (Regla de No-Redundancia)
* **Criterio:** El Admin debe verificar que ningún dato técnico o numérico que ya posea una columna asignada (como la Constante de Gas en Col 44) esté presente en el campo `Info_Reg_Json`.
* **Meta:** 100% de datos técnicos estructurados fuera del JSON.

### 2.2 Integridad Forense de Datos
* **Criterio:** El campo JSON debe ser utilizado exclusivamente para sustento legal y normativo (Resoluciones CRA/CREG, avisos de tarifas, decretos).
* **Meta:** El JSON debe aportar valor de auditoría, no ruido de datos repetidos.

### 2.3 Precisión de Identidad y Formato
* **Criterio:** Verificación de formatos globales (Fechas DD/MM/YYYY y comas decimales) y formatos particulares de Spoke (Apóstrofes en IDs de EPM).

---

## 3. GESTIÓN DE APRENDIZAJE Y MEJORA CONTINUA
*El sistema UCMS es un organismo vivo que evoluciona con cada factura procesada:*

1.  **Detección de Desviación:** Si el Admin detecta una falla recurrente o una redundancia, debe reportarlo en el `CHANGELOG_ERRORES.md`.
2.  **Ajuste de Spoke:** Basado en el reporte del Admin, el usuario debe actualizar el `PROMPT` de la Spoke afectada para corregir el comportamiento en el siguiente ciclo.
3.  **Registro Histórico:** El archivo `HISTORIA_PROYECTO.md` documentará estos hitos de aprendizaje para evitar retrocesos en la arquitectura del sistema.

---

## 4. DIFERENCIACIÓN DE RESPONSABILIDADES
* **Responsabilidad Global:** El Admin vela por el cumplimiento de las Reglas Maestras (Sección A de `OUTPUT_UNIVERSAL.md`).
* **Responsabilidad de Spoke:** Cada GEM es responsable de su propia lógica de inspección visual y mapeo de columnas técnicas según su servicio.
