# BITÁCORA DE CAMBIOS Y ERRORES (CHANGELOG)
**Formato de registro:** Fecha | GEM | Versión | Tipo | Descripción

| Fecha | GEM | Versión Afectada | Tipo (Fix/Feat) | Descripción del Cambio |
|:---|:---|:---|:---|:---|
| 2025-12-27 | Tigo | v1.0.0 | Feat | Se añade detección de avisos de alza en pie de página. Pasa a v1.1.0 |
| 2025-12-27 | Global | Todas | Major | Se define estándar de 22 columnas. Todas las GEMs deben migrar a v2.0.0 |
| 2025-12-28 | EPM | v2.1.0 | Feat | Implementación de Doble Bloque (Core+Vertical) y Fila Totalizadora. |
| 2025-12-28 | Tigo | v2.1.0 | Feat | Implementación de Doble Bloque (Detalle de Plan en Vertical). Se elimina fila total por redundancia. |
| 2025-12-28 | Global | v2.1.1 | Major | Cambio de Arquitectura a Bases Relacionales (Maestra + Extensiones). |
2025-12-28,Afinia,v2.1.0,Feat,Migración a Arquitectura Core + Vertical. Adaptación a estándar de 22 columnas.
2025-12-28,Surtigas,v2.1.0,Feat,Migración a Arquitectura Core + Vertical.
2025-12-28,Acuacar,v2.1.0,Feat,Migración a Arquitectura Core + Vertical.
2025-12-28,Sistema,v2.1.0,Milestone,Hito de Migración Completa: 100% de GEMs operando en Arquitectura Relacional.
| 2025-12-28 | Global | v2.1.3 | Fix | Estandarización regional COL: Coma decimal (,) y punto de miles prohibido. Blindaje de Periodo con apóstrofe. |
| 2025-12-29 | Global | v2.2.0 | Major | Implementación del "Triángulo de Seguridad" en Bloque B. Desglose detallado de componentes de costo en columnas y uso de JSON para future-proofing. |
| 2025-12-30 | EPM | v2.3.0 | Fix | Reingeniería de Prompt: Soporte para Contribuciones (Estrato 6) y Mapeo explícito de componentes de Gas. Eliminación de saludos. |
| 2025-12-30 | EPM | v2.3.1 | Fix | Corrección de mapeo de fechas (Año heredado) y separación explícita de Cargo Fijo. Inclusión de Alertas en fila Total. |
| 2025-12-30 | EPM | v2.3.2 | Fix | Corrección de compatibilidad fechas Google Sheets ('SEPT') y precisión de componentes Aseo (CBL/CRT).|
31/12/2025,Global / EPM,v2.5.0,MAJOR,Migración global al modelo de Bloque Único Dinámico. Definición de la matriz de 65 columnas para Spoke EPM. Estandarización de fechas (DD/MM/YYYY) e IDs con apóstrofe (').
