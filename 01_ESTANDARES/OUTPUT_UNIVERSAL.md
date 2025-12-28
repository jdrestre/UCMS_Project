# ESTÁNDAR DE SALIDA UNIVERSAL (UCMS)
**Versión:** 2.1.1 (Arquitectura Core + Vertical + Total Condicional)
**Estado:** VIGENTE
**Fecha:** 28-Dic-2025

Todas las GEMs Spokes deben generar su extracción en DOS BLOQUES vinculados por el `ID_Unico`.

---

### BLOQUE A: TABLA MAESTRA (CORE)
**Destino:** Hoja `MASTER_CONSOLIDADA`
**Columnas:** 22 columnas obligatorias e inmutables.

| # | ID Columna | Descripción |
|:---|:---|:---|
| 1 | **ID_Unico** | `PERIODO` + `_` + `PROVEEDOR` + `_` + `CONTRATO` [+ `_SERVICIO` si aplica] |
| 2 | **Periodo** | `'` + 3 letras Mes (MAY) + Año. Septiembre es `'SEPT`. (Ej: `'OCT2025`) |
| 3 | **Año** | AAAA (Ej: `2025`) |
| 4 | **Mes** | Nombre completo (Ej: `Octubre`) |
| 5 | **Ciudad** | (Ej: `Cartagena`, `Medellín`) |
| 6 | **Servicio** | `Energía`, `Gas`, `Agua`, `Telecomunicaciones`, `Aseo`, `TOTAL_FACTURA` |
| 7 | **Proveedor** | (Ej: `Afinia`, `EPM`, `Tigo`) |
| 8 | **Contrato** | Número de suscriptor |
| 9 | **Fecha_Inicio** | `dmmm` (Ej: `1oct`) |
| 10 | **Fecha_Fin** | `dmmm` (Ej: `31oct`) |
| 11 | **Dias_Fact** | Número entero |
| 12 | **Consumo_Cant** | Cantidad consumida o "1" (fijo) |
| 13 | **Unidad_Medida**| `kWh`, `m3`, `Plan`, `GLOBAL` |
| 14 | **Valor_Unitario**| Precio unidad o Valor Plan Base |
| 15 | **Costo_Consumo** | `Consumo` * `Unitario` |
| 16 | **Variables_Extra**| Otros cobros (Alumbrado, Netflix, Aseo) |
| 17 | **Deducciones** | Valor POSITIVO de subsidios/descuentos |
| 18 | **Total_Pagar** | Valor final |
| 19 | **Estado_Pago** | `Al día`, `En Mora`, `Pendiente` |
| 20 | **Fecha_Limite** | `dmmm` (Vencimiento) |
| 21 | **Lectura_Plan** | Lectura medidor o Velocidad Plan |
| 22 | **Alertas_Novedades**| Inteligencia Predictiva o "Normal" |

**Regla de la Fila Total:**
* **Facturas Multi-Servicio (EPM):** OBLIGATORIO generar una fila final con sufijo `_TOTAL` y servicio `TOTAL_FACTURA`.
* **Facturas Mono-Servicio (Tigo/Gas):** NO generar fila total (es redundante).

---

### BLOQUE B: EXTENSIÓN TÉCNICA (VERTICAL)
**Destino:** Hojas Específicas (`EXT_EPM`, `EXT_TIGO`, etc.)
**Objetivo:** Datos profundos que no caben en el Core.

* **Requisito:** Debe incluir siempre la columna `ID_Unico` para cruzar con el Bloque A.
* **Contenido:** Libre según la necesidad de la Spoke (Ej: Estrato, Factores de corrección, Detalle de Apps).
