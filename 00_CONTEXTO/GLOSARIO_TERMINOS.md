# GLOSARIO DE TÉRMINOS UCMS (v2.5.1)
**Propósito:** Definición de conceptos y variables con trazabilidad de origen para asegurar que el Admin diferencie las reglas del Sistema de las particularidades de cada Spoke.

| Término | Definición | Origen / Contexto |
| :--- | :--- | :--- |
| **Bloque Único Dinámico** | Modelo de datos plano donde toda la información financiera y técnica viaja en una sola fila por cada servicio extraído. | **GLOBAL (Sistema)** |
| **Regla de No-Redundancia** | Principio de limpieza que prohíbe duplicar datos en campos JSON si ya existe una columna técnica asignada para ese dato. | **GLOBAL (Sistema)** |
| **Agnosticismo Estructural** | Capacidad del Admin para validar diferentes formatos y números de columnas según el PROMPT de la Spoke activa. | **GLOBAL (Admin)** |
| **Smart Alerts** | Etiquetas en mayúsculas (Tags) situadas en la columna de alertas para identificar anomalías técnicas o financieras. | **GLOBAL (Sistema)** |
| **Mejora Continua** | Proceso de ajuste de los Prompts de las Spokes basado en los errores o redundancias detectadas por el Admin. | **GLOBAL (Sistema)** |
| **Formato UCMS Ready** | Estándar global de fechas (DD/MM/YYYY) y decimales con coma (,) sin separadores de miles. | **GLOBAL (Sistema)** |
| **Const (Col 44)** | Variable técnica de conversión específica. En Energía: Factor Multiplicador. En Gas: Constante de Corrección. | **SPOKE (EPM)** |
| **Info_Reg_Json (Col 65)** | Contenedor JSON para texto legal y resoluciones. En EPM, tiene prohibido contener el valor de la Columna 44. | **SPOKE (EPM)** |
| **Identificadores Protegidos** | Requisito de usar apóstrofe (') en IDs (Contrato, Medidor, etc.) para preservar el formato en herramientas de celdas. | **SPOKE (EPM)** |
| **Umbral de Desviación** | Lógica de KPI que define cuánto puede variar un dato técnico antes de disparar una Smart Alert. | **SPOKE (EPM)** |
| **Vertical de Servicio** | Clasificación de la fila según el tipo de cobro (ENERGIA, GAS, ACUE, ALCA, ASEO, ALUM). | **SPOKE (EPM)** |
