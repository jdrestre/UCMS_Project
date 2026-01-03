# GLOSARIO DE TÉRMINOS UCMS (v2.6.0)
**Propósito:** Definición de conceptos y variables con trazabilidad de origen para asegurar que el Admin diferencie las reglas del Sistema de las particularidades de cada Spoke, alineado a la arquitectura de 76 columnas.

| Término | Definición | Origen / Contexto |
| :--- | :--- | :--- |
| **Bloque Único Dinámico** | Modelo de datos plano donde toda la información financiera y técnica viaja en una sola fila por cada servicio extraído. | **GLOBAL (Sistema)** |
| **Regla de No-Redundancia** | Principio de limpieza que prohíbe duplicar datos en campos JSON si ya existe una columna técnica asignada para ese dato. | **GLOBAL (Sistema)** |
| **Agnosticismo Estructural** | Capacidad del Admin para validar diferentes formatos y números de columnas según el PROMPT de la Spoke activa. | **GLOBAL (Admin)** |
| **Smart Alerts** | Etiquetas en mayúsculas (Tags) situadas en la columna de alertas (Col 75) para identificar anomalías técnicas o financieras. | **GLOBAL (Sistema)** |
| **Mejora Continua** | Proceso de ajuste de los Prompts de las Spokes basado en los errores o redundancias detectadas por el Admin. | **GLOBAL (Sistema)** |
| **Formato UCMS Ready** | Estándar global de fechas (DD/MM/YYYY) y decimales con coma (,) sin separadores de miles. | **GLOBAL (Sistema)** |
| **OJF (Orden Jerárquico)** | Protocolo que obliga a generar las filas siguiendo la secuencia física de la factura para facilitar la auditoría visual. | **GLOBAL (Sistema)** |
| **Granularidad Absoluta** | Nivel de detalle máximo donde cada componente de costo (variable o fijo) posee su propia columna dedicada. | **GLOBAL (EPM)** |
| **Const (Col 48)** | Variable técnica de conversión. En Energía: Factor Multiplicador. En Gas: Constante de Corrección. | **SPOKE (EPM)** |
| **Info_Reg_Json (Col 76)** | Contenedor JSON para texto legal y resoluciones. Tiene prohibido contener valores de la Columna 48. | **SPOKE (EPM)** |
| **Identificadores Protegidos** | Requisito de usar apóstrofe (') en IDs (Contrato, Medidor, etc.) para preservar el formato en herramientas de celdas. | **SPOKE (EPM)** |
| **Relleno Técnico Forense** | Obligación de insertar "0,00" en campos técnicos de filas totalizadoras para evitar desplazamientos de matriz. | **SPOKE (EPM)** |
| **ID Dinámico (Gas)** | Capacidad de capturar variables específicas por nombre y ID (Ej: Transporte 7, Compresión 8) en columnas fijas. | **SPOKE (EPM)** |
| **Desglose de Toneladas** | Captura de los 4 tipos de residuos en Aseo (NoAp, Barr, Limp, Rech) en las columnas 71 a 74. | **SPOKE (EPM)** |
| **Umbral de Desviación** | Lógica de KPI que define cuánto puede variar un dato técnico antes de disparar una Smart Alert. | **SPOKE (EPM)** |
