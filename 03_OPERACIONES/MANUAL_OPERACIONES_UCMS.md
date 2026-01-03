# MANUAL DE OPERACIONES UCMS (v2.6.0)
**Estado:** VIGENTE | **Referencia de Ejecución Directa para el Admin**

## 1. SISTEMA MODULAR Y ARQUITECTURA DE DATOS
El UCMS es un **Sistema Modular** diseñado para escalar. El Admin (IA) debe operar bajo un pensamiento de capas, diferenciando estrictamente qué reglas son universales y cuáles pertenecen a la lógica de negocio de una Spoke específica:

1.  **Capa Global (Núcleo):** Reglas de formato, fechas, decimales y estructura de matriz que no varían. Es el estándar de calidad del sistema.
2.  **Capa de Spoke (Módulos):** Granularidad técnica, desgloses unitarios y variables dinámicas propias de cada proveedor (Ej: EPM, Tigo).

---

## 2. OPERACIONES GLOBALES (APLICAN A TODAS LAS SPOKES)
*Instrucciones de cumplimiento obligatorio para mantener la integridad del sistema modular:*

### 2.1 Estandarización de Formatos (UCMS Ready)
* **Decimales:** Uso exclusivo de coma (,) decimal. Prohibido el uso de puntos para miles.
* **Fechas:** Formato DD/MM/YYYY obligatorio en todas las columnas cronológicas.
* **Alineación de Cierre:** Las columnas de Alertas y JSON son anclas estáticas que deben finalizar cada fila para evitar desplazamientos.

### 2.2 Principio de No-Redundancia e Integridad
* **Mapeo Único:** Si un dato financiero o técnico tiene una columna dedicada en la matriz, está terminantemente prohibido duplicarlo en el campo JSON.
* **Relleno de Seguridad:** En servicios no aplicables o filas de totalización, los campos técnicos deben rellenarse con "0,00".

---

## 3. OPERACIONES ESPECÍFICAS (SPOKE EPM)
*Protocolos exclusivos para la gestión de granularidad absoluta en EPM Antioquia:*

### 3.1 Protocolo OJF (Orden Jerárquico por Factura)
* Generación obligatoria de filas en secuencia física: ACUE -> ALCA -> ENERGIA -> GAS -> ASEO -> ALUM -> _TOTAL_OTRAS -> _TOTAL.

### 3.2 Granularidad y IDs Dinámicos
* **Gas:** Captura obligatoria de componentes por ID (Transporte 7 en Col 65 y Compresión 8 en Col 69).
* **Aseo:** Desglose forense de las 4 clases de toneladas (Cols 71-74).
* **Constante (Col 48):** La Constante de Gas o Factor de Energía reside **únicamente** en la Columna 48.

---

## 4. GESTIÓN DE APRENDIZAJE Y CONFLICTOS

### 4.1 Global (Sistema)
* **Resolución de Conflictos:** Si una instrucción de Spoke contradice una Regla Global, el Admin debe priorizar la **Regla Global** y reportar el conflicto.
* **Estandarización:** Identificar patrones de error comunes entre diferentes Spokes para robustecer el núcleo del sistema.

### 4.2 Específico (Spoke EPM)
* **Afinación de Extracción:** Registrar fallos específicos en el mapeo de IDs dinámicos (como la "ceguera de granularidad") para sugerir ajustes en el `PROMPT_EPM.md`.
* **Trazabilidad de Commits:** Cada mejora aprobada en la granularidad de EPM debe quedar registrada en el repositorio local.

---

## 5. CONTROL DE CALIDAD (KPIs)

### 5.1 Global (Sistema)
* **KPI Estructural:** Coincidencia del 100% entre el número de columnas definidas y la salida generada (EPM: 76 columnas).
* **KPI de Formato:** Cero tolerancia a puntos como separadores decimales o formatos de fecha ISO/Inglés.

### 5.2 Específico (Spoke EPM)
* **KPI de Identidad:** Verificación de apóstrofes (') en todos los campos de identificación protegidos (Cols 1, 11, 12, 13, 45).
* **KPI de Granularidad:** Confirmación de presencia de datos en componentes de Gas (Col 65, 69) y Aseo (Cols 71-74) cuando la factura los detalla.
* **KPI de Auditoría:** Clasificación precisa de estados en la Columna 75 (NORMAL, AUDITORIA, ALERTA).
