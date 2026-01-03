# CHANGELOG DE ERRORES Y MEJORAS UCMS

Este archivo constituye la memoria técnica forense del sistema. Registra la trazabilidad completa desde los inicios (v1.0.0) hasta la arquitectura modular de alta densidad, diferenciando responsabilidades Globales de las lógicas específicas de cada GEM Spoke.

## 📄 REGISTRO HISTÓRICO UNIFICADO (CRONOLÓGICO)

| Fecha | GEM | Versión | Tipo | Descripción |
| :--- | :--- | :--- | :--- | :--- |
| **02/01/2026** | **GLOBAL** | **v2.6.0** | **HITO** | **Salto a 76 columnas**: Implementación de Granularidad Absoluta, Protocolo OJF y Relleno Técnico (0,00). |
| 02/01/2026 | **GLOBAL** | v2.6.0 | **AJUSTE** | Estandarización de la variable técnica (Constante/Factor) exclusivamente en la **Columna 48**. |
| 02/01/2026 | **EPM** | v2.6.0 | **SOLUCIONADO** | Mapeo forense de IDs dinámicos Gas (Transporte 7, Compresión 8) y 4 Toneladas de Aseo (71-74). |
| **31/12/2025** | **GLOBAL / EPM** | **v2.5.0** | **HITO** | **Migración al modelo de Bloque Único Dinámico**. Definición de matriz de 65 columnas para EPM. |
| 30/12/2025 | **EPM** | v2.3.2 | **SOLUCIONADO** | Compatibilidad fechas Google Sheets ('SEPT') y precisión en componentes Aseo (CBL/CRT). |
| 30/12/2025 | **EPM** | v2.3.1 | **SOLUCIONADO** | Corrección año heredado en fechas, cargo fijo y alertas en fila Total. |
| 30/12/2025 | **EPM** | v2.3.0 | **MEJORADO** | Soporte para Contribuciones (Estrato 6), mapeo componentes Gas y eliminación de saludos. |
| 29/12/2025 | **GLOBAL** | v2.2.0 | **HITO** | **Implementación "Triángulo de Seguridad"**: Desglose de costos y uso de JSON para future-proofing. |
| 28/12/2025 | **GLOBAL** | v2.1.3 | **SOLUCIONADO** | Estandarización COL: Coma decimal (,), prohibición de miles y apóstrofe en IDs. |
| 28/12/2025 | **SISTEMA** | v2.1.0 | **HITO** | **Migración Completa**: 100% de GEMs operando en Arquitectura Relacional. |
| 28/12/2025 | **AFINIA / SURTIGAS / ACUACAR** | v2.1.0 | **FEAT** | Migración a Arquitectura Core + Vertical (Adaptación a estándar de 22 columnas). |
| 28/12/2025 | **GLOBAL** | v2.1.1 | **HITO** | Cambio de Arquitectura a Bases Relacionales (Maestra + Extensiones). |
| 28/12/2025 | **EPM / TIGO** | v2.1.0 | **FEAT** | Implementación de Doble Bloque (EPM: Fila Totalizadora / TIGO: Detalle de Plan). |
| 27/12/2025 | **GLOBAL** | v2.0.0 | **HITO** | **Estándar de 22 columnas**. Obligatoriedad de migración para todas las GEMs. |
| 27/12/2025 | **TIGO** | v1.1.0 | **FEAT** | Detección de avisos de alza en pie de página (Evolución desde v1.0.0). |

---

## 🛠️ GUÍA FUNCIONAL PARA ACTUALIZACIÓN (MANTENIMIENTO)
Para asegurar que este archivo mantenga su integridad y sea procesable por el Admin del Sistema, siga estas reglas mandatorias:

1. **Orden Descendente:** Las actualizaciones se insertan siempre en la parte superior (la fecha más reciente primero).
2. **Identificación GEM:** - Usar **GLOBAL** para cambios que afecten a la matriz universal o al núcleo de inteligencia.
   - Usar el nombre de la Spoke (Ej: **EPM**, **TIGO**) para cambios específicos de lógica de negocio o prompts.
3. **Tipificación de Entrada:**
   - **HITO:** Cambios arquitectónicos mayores o saltos de versión principal.
   - **FEAT:** Nuevas funcionalidades de extracción o soporte de datos.
   - **SOLUCIONADO:** Corrección de errores de mapeo, alucinaciones o bugs de formato.
   - **AJUSTE:** Cambios menores de estandarización o configuración.
   - **MEJORADO:** Optimización de prompts para mayor velocidad o precisión.
4. **Respaldo Forense:** Cada entrada debe ser validada contra el `HISTORIA_PROYECTO.md` antes de ser consolidada.
