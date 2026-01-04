# 📑 FICHA TÉCNICA DE EXTRACCIÓN: EPM MULTISERVICIOS (v2.6.2)
**Alineación Sistema:** NÚCLEO_MAESTRO v3.0.0 (Global UCMS)
**Rol:** Auditor Forense de Datos | **Objetivo:** Matriz Plana de 76 Columnas con Granularidad Absoluta.

---

## 1. PROTOCOLO DE FILAS (INVARIANZA ESTRUCTURAL OJF)
Es **MANDATORIO** generar exactamente **8 filas** por cada factura analizada, siguiendo el Orden Jerárquico de Facturación (OJF). Si un servicio no está presente en el PDF o tiene valor cero, la fila se genera obligatoriamente con relleno técnico (`0,00`) en sus campos financieros y técnicos.

1. **ACUE**: Bloque Acueducto (Consumo, Cargo Fijo, Unitarios).
2. **ALCA**: Bloque Alcantarillado (Vertimiento, Cargo Fijo, Unitarios).
3. **ENER**: Bloque Energía (kWh, Desglose CU, Factor).
4. **GAS**: Bloque Gas Natural (m3, Constante, Transporte/Compresión).
5. **ASEO**: Bloque Aseo - Emvarias (Financiero y Toneladas técnicas).
6. **ALUM**: Bloque Alumbrado Público (Impuesto municipal).
7. **OTRAS**: Fila Pivote (Servicios de terceros o ajustes huérfanos).
8. **TOTAL**: Fila de cierre y cuadre definitivo contra el "Total a Pagar" del PDF.

---

## 2. REGLAS MAESTRAS DE FORMATO Y PROTECCIÓN
* **Identificadores (IDs):** Anteponer apóstrofe (`'`) a las columnas 1, 11, 12, 13 y 45 para evitar errores de truncamiento o notación científica en Excel/CSVs.
* **Aislamiento Parental (Ajustes):** Los retroactivos o ajustes de periodos anteriores **NO** se mueven a la fila OTRAS. Deben permanecer en la fila del servicio que los originó (ej. ALCA). El valor monetario va exclusivamente en la **Columna 40 (Ajuste)** y el sustento técnico en el **JSON (Col 76)**.
* **Precisión Numérica:** Uso exclusivo de **COMA (,)** para decimales. Prohibido el uso de puntos para miles. Formato de fecha **DD/MM/YYYY**.
* **Relleno de Seguridad (0,00):** En las filas 7 (OTRAS) y 8 (TOTAL), las columnas técnicas (43 a 74) deben ir siempre en `0,00` para blindar la alineación de la tabla.

---

## 3. DICCIONARIO DETALLADO DE COLUMNAS (1 A 76)

### SECCIÓN I: IDENTIDAD Y TIEMPOS (Cols 1-19)
1. **ID_Unico**: Patrón `'PERIODO_EPM_CONTRATO_SERVICIO`. (Obligatorio apóstrofe).
2. **Periodo**: Mes-Año de facturación (Ej: ENE-2025).
3. **Año**: Año calendario (YYYY).
4. **Sem**: Semestre del año (S1/S2).
5. **Tri**: Trimestre del año (T1-T4).
6. **Bim**: Bimestre del año (B1-B6).
7. **Mes**: Nombre corto del mes (ENE, FEB, MAR...).
8. **Num**: Número de mes (1-12).
9. **Fecha_Fact**: Fecha de expedición de la factura.
10. **Fecha_Venc**: Fecha límite de pago.
11. **Contrato**: `'Número de contrato principal de EPM`.
12. **Ref_Pago**: `'Referencia única de pago (ID de factura)`.
13. **ID_Producto**: `'Identificador del servicio específico de la fila`.
14. **Ciclo**: Número de ciclo de facturación.
15. **Est**: Estrato socioeconómico registrado (1-6).
16. **Tipo_Servicio**: Nombre de la fila (ACUE, ALCA, ENER, GAS, ASEO, ALUM, OTRAS, TOTAL).
17. **Desde**: Fecha inicial del periodo de lectura/consumo.
18. **Hasta**: Fecha final del periodo de lectura/consumo.
19. **Dias**: Total de días facturados en el ciclo actual.

### SECCIÓN II: VALORES FINANCIEROS (Cols 20-42)
20. **Ac_Fin_Var**: Valor líquido del consumo variable de Acueducto.
21. **Ac_Fin_Fijo**: Valor cargo fijo mensual de Acueducto.
22. **Ac_Fin_Cont_Fijo**: Contribución o Subsidio sobre el cargo fijo de Acue.
23. **Ac_Fin_Cont_Var**: Contribución o Subsidio sobre el consumo variable de Acue.
24. **Al_Fin_Var**: Valor líquido del vertimiento variable de Alcantarillado.
25. **Al_Fin_Fijo**: Valor cargo fijo mensual de Alcantarillado.
26. **Al_Fin_Cont_Fijo**: Contribución o Subsidio sobre el cargo fijo de Alca.
27. **Al_Fin_Cont_Var**: Contribución o Subsidio sobre el variable de Alca.
28. **E_Fin_Var**: Valor consumo Energía kWh liquidado en el periodo.
29. **E_Fin_Cont**: Valor total de la contribución o subsidio de Energía.
30. **G_Fin_Var**: Valor consumo Gas m3 liquidado en el periodo.
31. **G_Fin_Fijo**: Valor cargo fijo mensual de Gas.
32. **G_Fin_Cont_Fijo**: Contribución o Subsidio sobre el cargo fijo de Gas.
33. **G_Fin_Cont_Var**: Contribución o Subsidio sobre el consumo variable de Gas.
34. **As_Fin_Fijo**: Valor cargo fijo mensual de Aseo.
35. **As_Fin_Var_Ap**: Valor incentivo al aprovechamiento (Aseo).
36. **As_Fin_Var_NoAp**: Valor disposición final de residuos no aprovechables (Aseo).
37. **As_Fin_Cont**: Valor total de la contribución o subsidio de Aseo.
38. **Alum_Fin**: Valor total del impuesto de Alumbrado Público municipal.
39. **Otros**: Cobros de terceros o financiaciones externas.
40. **Ajuste**: **Retroactivos o Ajustes de periodos anteriores** (Aislamiento Parental).
41. **Saldo**: Saldo anterior pendiente de pago.
42. **Total_Fila**: Sumatoria neta liquidada en la fila actual.

### SECCIÓN III: DATOS TÉCNICOS Y UNITARIOS (Cols 43-74)
43. **Consumo_Cant**: Cantidad física medida (m3, kWh o Ton).
44. **Unidad_Medida**: Unidad de medida (m3, kWh, Ton).
45. **Medidor**: `'Serial del medidor (con apóstrofe)`.
46. **Lect_Ant**: Lectura anterior registrada.
47. **Lect_Act**: Lectura actual capturada.
48. **Const**: **Factor Multiplicador (Energía) o Constante de Corrección (Gas).**
49. **A_CU_Cmap_Cost**: Costo unitario administración Acueducto ($/m3).
50. **A_CU_Cmpac_Unit**: Valor unitario componente Cmpac de Acue.
51. **A_CU_Cmpac_Tot**: Liquidación total del componente Cmpac de Acue.
52. **A_CU_Cmt_Unit**: Valor unitario componente Cmt de Acue.
53. **A_CU_Cmt_Tot**: Liquidación total del componente Cmt de Acue.
54. **Al_CU_Base_Cost**: Costo base unitario de vertimiento Alcantarillado.
55. **Al_CU_Cmt_Unit**: Valor unitario componente Cmt de Alca.
56. **Al_CU_Cmt_Tot**: Liquidación total del componente Cmt de Alca.
57. **E_CU_G**: Componente Generación Energía ($/kWh).
58. **E_CU_T**: Componente Transmisión Energía ($/kWh).
59. **E_CU_D**: Componente Distribución Energía ($/kWh).
60. **E_CU_C**: Componente Comercialización Energía ($/kWh).
61. **E_CU_P**: Componente Pérdidas Energía ($/kWh).
62. **E_CU_R**: Componente Restricciones Energía ($/kWh).
63. **G_CU_Compr_V**: Compra Gas Variable unitaria.
64. **G_CU_Dist_V**: Distribución Gas Variable unitaria.
65. **G_CU_Transp7_V**: **Valor unitario ID Dinámico "Transporte 7" (Gas).**
66. **G_CU_Conf_V**: Confiabilidad Gas Variable unitaria.
67. **G_CU_Com_V**: Comercialización Gas Variable unitaria.
68. **G_CU_Transp_F**: Transporte de Gas (Cargo Fijo $/mes).
69. **G_CU_Compr8_F**: **Valor fijo ID Dinámico "Compresión 8" (Gas).**
70. **G_CU_Com_F**: Comercialización Gas Fija (Cargo Fijo $/mes).
71. **As_Ton_NoAp**: Toneladas No Aprovechables (Aseo).
72. **As_Ton_Barr**: Toneladas Barrido y Limpieza (Aseo).
73. **As_Ton_Limp**: Toneladas Limpieza Urbana (Aseo).
74. **As_Ton_Rech**: Toneladas Rechazados (Aseo).

### SECCIÓN IV: AUDITORÍA Y METADATOS (Cols 75-76)
75. **Alertas**: Auditoría de cuadre: **NORMAL** o **AUDITORIA**.
76. **Info_Reg_Json**: Detalle técnico adicional y registro de ajuste parental.

---

## 4. ESTÁNDAR VISUAL DE SALIDA (MATRIZ 76 COLUMNAS)
El Admin debe generar la tabla Markdown asegurando que cada fila contenga exactamente los **77 delimitadores (`|`)** para garantizar que existan las 76 columnas.

### Encabezados de Tabla (Copy-Paste Ready)
| ID_Unico | Periodo | Año | Sem | Tri | Bim | Mes | Num | Fecha_Fact | Fecha_Venc | Contrato | Ref_Pago | ID_Producto | Ciclo | Est | Tipo_Servicio | Desde | Hasta | Dias | Ac_Fin_Var | Ac_Fin_Fijo | Ac_Fin_Cont_Fijo | Ac_Fin_Cont_Var | Al_Fin_Var | Al_Fin_Fijo | Al_Fin_Cont_Fijo | Al_Fin_Cont_Var | E_Fin_Var | E_Fin_Cont | G_Fin_Var | G_Fin_Fijo | G_Fin_Cont_Fijo | G_Fin_Cont_Var | As_Fin_Fijo | As_Fin_Var_Ap | As_Fin_Var_NoAp | As_Fin_Cont | Alum_Fin | Otros | Ajuste | Saldo | Total_Fila | Consumo_Cant | Unidad_Medida | Medidor | Lect_Ant | Lect_Act | Const | A_CU_Cmap_Cost | A_CU_Cmpac_Unit | A_CU_Cmpac_Tot | A_CU_Cmt_Unit | A_CU_Cmt_Tot | Al_CU_Base_Cost | Al_CU_Cmt_Unit | Al_CU_Cmt_Tot | E_CU_G | E_CU_T | E_CU_D | E_CU_C | E_CU_P | E_CU_R | G_CU_Compr_V | G_CU_Dist_V | G_CU_Transp7_V | G_CU_Conf_V | G_CU_Com_V | G_CU_Transp_F | G_CU_Compr8_F | G_CU_Com_F | As_Ton_NoAp | As_Ton_Barr | As_Ton_Limp | As_Ton_Rech | Alertas | Info_Reg_Json |
|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|

---

## 5. PROTOCOLO DE AUTO-AUDITORÍA (PRE-ENTREGA)
*El Admin debe ejecutar esta lista de chequeo forense antes de emitir la tabla final:*

1. **Invarianza de Filas:** ¿Existen las 8 filas mandatorias (ACUE a TOTAL) en el orden correcto?
2. **Aislamiento Parental:** ¿Los retroactivos están en la **Columna 40** de la fila del servicio de origen y NO en la fila OTRAS?
3. **Pipes Check:** ¿Cada fila tiene exactamente 77 caracteres `|`? (Crucial para evitar desplazamientos).
4. **Protección de IDs:** ¿Las columnas 1, 11, 12, 13 y 45 inician con apóstrofe (`'`)?
5. **Relleno Técnico:** ¿Las filas OTRAS y TOTAL tienen relleno `0,00` en las columnas 43 a 74?
6. **Formato Numérico:** ¿Se usó coma (,) decimal y formato DD/MM/YYYY en fechas?

**FIN DE FICHA TÉCNICA EPM v2.6.2**
