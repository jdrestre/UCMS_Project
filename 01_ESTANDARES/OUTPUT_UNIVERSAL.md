# ESTÁNDAR DE SALIDA UNIVERSAL UCMS (v2.6.0)
**Estado:** PROPUESTO PARA DESPLIEGUE | **Referencia de conocimiento v2.6.0**

## SECCIÓN A: REGLAS MAESTRAS (GLOBALES)
*Estas reglas aplican a todo el ecosistema UCMS, independientemente de la Spoke.*

1. **Formato de Fecha:** El formato obligatorio es DD/MM/YYYY. No debe llevar apóstrofe para permitir el reconocimiento nativo en celdas de Google Sheets, Excel o hojas de cálculo.
2. **Formato Numérico:** Uso exclusivo de coma (,) como separador decimal. Está estrictamente prohibido el uso de puntos o separadores de miles.
3. **Principio de Integridad:** Se prohíbe la redundancia de datos numéricos o técnicos dentro de campos de observación tipo JSON si dichos datos ya poseen una columna asignada en la matriz de la Spoke.
4. **Relleno de Vacíos:** En filas de totalización o servicios que no apliquen, las columnas técnicas (43 a 74) deben contener "0,00" para mantener la integridad de la base de datos y evitar desplazamientos.
5. **Cierre Estático:** Las columnas de Alertas y JSON deben situarse siempre al final de la matriz, actuando como anclas de cierre de la fila.

---

## SECCIÓN B: MATRIZ DE REFERENCIA - SPOKE EPM (76 COLUMNAS)
*Estructura técnica y reglas de formato para la Granularidad Absoluta de EPM.*

### B.1 Reglas de Formato Específicas (EPM)
* **Identificadores Protegidos (IDs):** Es obligatorio el uso del prefijo apóstrofe (') al inicio de los datos para los campos: ID_Unico, Contrato, Ref_Pago, ID_Producto y Medidor.
* **Estructura del ID_Unico:** Debe seguir estrictamente el patrón `'PERIODO_EMPRESA_CONTRATO_SERVICIO`. (Ejemplo: `'JUN-2025_EPM_2651903_ACUE`).
* **Orden Jerárquico por Factura (OJF):** Las filas deben generarse en la secuencia física de cobro: ACUE -> ALCA -> ENERGIA -> GAS -> ASEO -> ALUM -> _TOTAL_OTRAS_ENTIDADES -> _TOTAL.
* **Regla de No-Redundancia (EPM):** El valor de la 'Constante de Gas' o 'Factor Medidor Energía' debe alojarse únicamente en la **Columna 48 (Const)**. Queda prohibida su duplicidad en la Columna 76 (Info_Reg_Json).
* **Relleno Técnico Forense:** En las filas de totalización (`_TOTAL_OTRAS_ENTIDADES` y `_TOTAL`), todas las columnas de desgloses unitarios y técnicos (49 a 74) deben rellenarse con "0,00".

### B.2 Grupos y Rangos (EPM)
1. **GRUPO I: IDENTIDAD (Cols 1 - 19):** Metadatos cronológicos, identidad del contrato y tiempos del ciclo.
2. **GRUPO II: FINANCIERO (Cols 20 - 42):** Liquidación de cobros variables, fijos y contribuciones por cada servicio. Sigue el orden OJF.
3. **GRUPO III: TÉCNICO (Cols 43 - 74):** Consumos, lecturas, constantes y desgloses de componentes de costo unitario y total.
4. **GRUPO IV: OBS (Cols 75 - 76):** Alertas de auditoría y contenedor JSON para sustento legal.

### B.3 Catálogo Detallado de Columnas (76)

#### --- GRUPO I: IDENTIDAD (Cols 1 a 19) ---
| Col | Nombre Variable | Descripción / Regla de Extracción |
| :--- | :--- | :--- |
| 1 | **ID_Unico** | 'PERIODO_EPM_CONTRATO_SERVICIO. Único por fila. |
| 2 | **Periodo** | Mes y Año de facturación (Ej: JUN-2025). |
| 3 | **Año** | Año calendario (Ej: 2025). |
| 4 | **Sem** | Semestre calendario (S1 o S2). |
| 5 | **Tri** | Trimestre del año (T1 a T4). |
| 6 | **Bim** | Bimestre del año (B1 a B6). |
| 7 | **Mes** | Nombre corto del mes (Ej: JUN). |
| 8 | **Num** | Número de mes (1 a 12). |
| 9 | **Fecha_Fact** | Fecha de expedición (DD/MM/YYYY). |
| 10 | **Fecha_Venc** | Fecha límite de pago (DD/MM/YYYY). |
| 11 | **Contrato** | 'Número de contrato suscrito con EPM. |
| 12 | **Ref_Pago** | 'Referencia única para pagos y convenios. |
| 13 | **ID_Producto** | 'Identificador del servicio o tag de totalización. |
| 14 | **Ciclo** | Ciclo de facturación asignado. |
| 15 | **Est** | Estrato socioeconómico (1 a 6). |
| 16 | **Tipo_Servicio** | Nombre del servicio o categoría de la fila (Ej: ACUE). |
| 17 | **Desde** | Fecha inicial del periodo de consumo. |
| 18 | **Hasta** | Fecha final del periodo de consumo. |
| 19 | **Dias** | Días transcurridos en el ciclo de lectura. |

#### --- GRUPO II: FINANCIERO (Cols 20 a 42) ---
| Col | Nombre Variable | Servicio / Componente |
| :--- | :--- | :--- |
| 20 | **Ac_Fin_Var** | ACUE: Consumo variable liquidado. |
| 21 | **Ac_Fin_Fijo** | ACUE: Cargo fijo mensual. |
| 22 | **Ac_Fin_Cont_Fijo** | ACUE: Contribución/Subsidio cargo fijo. |
| 23 | **Ac_Fin_Cont_Var** | ACUE: Contribución/Subsidio variable. |
| 24 | **Al_Fin_Var** | ALCA: Vertimiento variable liquidado. |
| 25 | **Al_Fin_Fijo** | ALCA: Cargo fijo mensual. |
| 26 | **Al_Fin_Cont_Fijo** | ALCA: Contribución/Subsidio cargo fijo. |
| 27 | **Al_Fin_Cont_Var** | ALCA: Contribución/Subsidio variable. |
| 28 | **E_Fin_Var** | ENER: Consumo kWh liquidado. |
| 29 | **E_Fin_Cont** | ENER: Contribución o Subsidio total. |
| 30 | **G_Fin_Var** | GAS: Consumo m3 liquidado. |
| 31 | **G_Fin_Fijo** | GAS: Cargo fijo mensual. |
| 32 | **G_Fin_Cont_Fijo** | GAS: Contribución/Subsidio cargo fijo. |
| 33 | **G_Fin_Cont_Var** | GAS: Contribución/Subsidio variable. |
| 34 | **As_Fin_Fijo** | ASEO: Cargo fijo de recolección. |
| 35 | **As_Fin_Var_Ap** | ASEO: Incentivo al aprovechamiento. |
| 36 | **As_Fin_Var_NoAp** | ASEO: Disposición residuos ordinarios. |
| 37 | **As_Fin_Cont** | ASEO: Contribución o Subsidio total. |
| 38 | **Alum_Fin** | ALUM: Impuesto Alumbrado Público. |
| 39 | **Otros** | Cobros de terceros / Financiaciones. |
| 40 | **Ajuste** | Ajuste decimal a la unidad ($). |
| 41 | **Saldo** | Saldo anterior pendiente. |
| 42 | **Total_Fila** | Total neto de la fila actual. |

#### --- GRUPO III: TÉCNICO (Cols 43 a 74) ---
| Col | Nombre Variable | Detalle Técnico / Granularidad |
| :--- | :--- | :--- |
| 43 | **Consumo_Cant** | Cantidad física (kWh, m3, Ton). |
| 44 | **Unidad_Medida** | Unidad (kWh, m3, Ton, Global). |
| 45 | **Medidor** | 'Serial del equipo. |
| 46 | **Lect_Ant** | Lectura anterior. |
| 47 | **Lect_Act** | Lectura actual. |
| 48 | **Const** | Constante corrección (Gas) / Factor (Energía). |
| 49 | **A_CU_Cmap_Cost** | ACUE: Costo medio administración ($/m3). |
| 50 | **A_CU_Cmpac_Unit** | ACUE: Tarifa unitaria Cmpac. |
| 51 | **A_CU_Cmpac_Tot** | ACUE: Liquidación total Cmpac. |
| 52 | **A_CU_Cmt_Unit** | ACUE: Tarifa unitaria Cmt. |
| 53 | **A_CU_Cmt_Tot** | ACUE: Liquidación total Cmt. |
| 54 | **Al_CU_Base_Cost** | ALCA: Costo base vertimiento ($/m3). |
| 55 | **Al_CU_Cmt_Unit** | ALCA: Tarifa unitaria Cmt. |
| 56 | **Al_CU_Cmt_Tot** | ALCA: Liquidación total Cmt. |
| 57 | **E_CU_G** | ENER: Generación ($/kWh). |
| 58 | **E_CU_T** | ENER: Transmisión ($/kWh). |
| 59 | **E_CU_D** | ENER: Distribución ($/kWh). |
| 60 | **E_CU_C** | ENER: Comercialización ($/kWh). |
| 61 | **E_CU_P** | ENER: Pérdidas ($/kWh). |
| 62 | **E_CU_R** | ENER: Restricciones ($/kWh). |
| 63 | **G_CU_Compr_V** | GAS: Compra variable ($/m3). |
| 64 | **G_CU_Dist_V** | GAS: Distribución variable ($/m3). |
| 65 | **G_CU_Transp7_V** | GAS: **Variable "Transporte 7"** ($/m3). |
| 66 | **G_CU_Conf_V** | GAS: Confiabilidad variable ($/m3). |
| 67 | **G_CU_Com_V** | GAS: Comercialización variable ($/m3). |
| 68 | **G_CU_Transp_F** | GAS: Transporte Gn (Cargo Fijo). |
| 69 | **G_CU_Compr8_F** | GAS: **Fijo "Compresión 8"** ($/factura). |
| 70 | **G_CU_Com_F** | GAS: Comercialización (Cargo Fijo). |
| 71 | **As_Ton_NoAp** | ASEO: Toneladas No Aprovechables. |
| 72 | **As_Ton_Barr** | ASEO: Toneladas barrido y limpieza. |
| 73 | **As_Ton_Limp** | ASEO: Toneladas limpieza urbana. |
| 74 | **As_Ton_Rech** | ASEO: Toneladas rechazados. |

#### --- GRUPO IV: OBS (Cols 75 a 76) ---
| Col | Nombre Variable | Descripción |
| :--- | :--- | :--- |
| 75 | **Alertas** | Tags: NORMAL, AUDITORIA, ALERTA. |
| 76 | **Info_Reg_Json** | Sustento legal/normativo. Sin datos técnicos. |
