# 📑 FICHA TÉCNICA DE EXTRACCIÓN: EPM MULTISERVICIOS
**Rol:** Auditor Forense de Datos | **Objetivo:** Matriz Plana con Granularidad Absoluta.

---
## 1. PROTOCOLO DE FILAS
Es **MANDATORIO** generar exactamente **8 filas** por cada factura analizada, siguiendo el Orden Jerárquico de Facturación (OJF). Si un servicio no está presente en el PDF o tiene valor cero, la fila se genera obligatoriamente con relleno técnico (`0,00`) en sus campos financieros y técnicos.
### OJF - Orden Jerárquico de Facturación
1. **ACUE**: Bloque Acueducto
2. **ALCA**: Bloque Alcantarillado
3. **ENER**: Bloque Energía
4. **GAS**: Bloque Gas Natural.
5. **ASEO**: Bloque Aseo - Emvarias.
6. **ALUM**: Bloque Alumbrado Público.
7. **OTRAS**: Fila Pivote (Servicios de terceros para sumatoria de OTRAS ENTIDADES (Suma de los totales de Aseo y Alumbrado)).
8. **TOTAL**: Fila de cierre y cuadre definitivo contra el "Total a Pagar" del PDF

## 2. DICCIONARIO DETALLADO DE COLUMNAS

### SECCIÓN I: IDENTIDAD Y TIEMPOS (Cols 1-19)
1. **ID_Unico**: Patrón `'PERIODO_EPM_CONTRATO_SERVICIO`. (Obligatorio apóstrofe).
2. **Periodo**: Mes-Año de facturación (Ej: 'ENE-2025). (Obligatorio apóstrofe).
3. **Año**: Año calendario (YYYY).
4. **Sem**: Semestre del año (S1/S2).
5. **Tri**: Trimestre del año (T1/T2/T3/T4).
6. **Bim**: Bimestre del año (B1/B2/B3/B4/B5/B6).
7. **Mes**: Nombre corto del mes (ENE, FEB, MAR, ABR, MAY, JUN, JUL, AGO, SEPT, OCT, NOV, DIC).
8. **Mes_Num**: Número de mes (1-12).
9.  **Fecha_Fact**:  `Fecha de generación` Fecha de expedición de la factura. (DD/MM/YYYY).
10. **Fecha_Venc**: `Pagar hasta el DD/MM/YYYY` Fecha límite de pago. (DD/MM/YYYY).
11. **Contrato**: `'Número de contrato principal de EPM`. (Obligatorio apóstrofe).
12. **Ref_Pago**: `'Referencia única de pago (ID de factura)`. (Obligatorio apóstrofe).
13. **ID_Producto**: `'Identificador del servicio específico de la fila`. (Obligatorio apóstrofe).
14. **Ciclo**: Número de ciclo de facturación.
15. **Est**: Estrato socioeconómico registrado (1-6).
16. **Tipo_Servicio**: Nombre de la fila (ACUE, ALCA, ENER, GAS, ASEO, ALUM, OTRAS, TOTAL).
17. **Desde**: Fecha inicial del periodo de lectura/consumo. (DD/MM/YYYY).
18. **Hasta**: Fecha final del periodo de lectura/consumo. (DD/MM/YYYY).
19. **Dias**: Total de días facturados en el ciclo actual.

### SECCIÓN II: VALORES FINANCIEROS

#### Valores facturados Acueducto
1. **Ac_Consumo** `Consumo mmm-yy` Calculado: m3 x Costo ($) Acueducto.
2. **Ac_Cargo_Fijo**: `Cargo fijo mmm-yy` Valor cargo fijo mensual de Acueducto.
3. **Ac_Contr_Cargo_Fijo**: `Contr cargo fijo mi %` Valor de la contribución o subsidio sobre el cargo fijo de Acueducto.
4. **Ac_Cont_Consumo**: `Contrib consumo min %` Valor de la contribución o subsidio sobre el consumo variable de Acueducto.

### Valores facturados Alcantarillado
1. **Al_Consumo** `Consumo mmm-yy` Calculado: m3 x Costo ($) Alcantarillado.
2. . **Al_Cargo_Fijo**: `Cargo fijo mmm-yy` Valor cargo fijo mensual de Alcantarillado.
3. **Al_Cont_Cargo_Fijo**: `Contr cargo fijo mi %` Valor de la contribución o subsidio sobre el cargo fijo de Alcantarillado.
4. **Al_Cont_Consumo**: `Contrib consumo min %` Valor de la contribución o subsidio sobre el consumo variable de Alcantarillado.

### Valores facturados Energía
1. **E_Energía**: `Energía mmm-yy` Valor consumo Energía kWh liquidado en el periodo.
2. **E_Contr_Activa**: `Contribución activa %` Valor de la contribución o subsidio sobre el consumo de Energía.
### Valores facturados Gas Natural
3. **G_Consumo**: `Consumo mmm-yy` Valor consumo Gas m3 liquidado en el periodo.
4. **G_Cargo_Fijo**: `Cargo fijo mmm-yy` Valor cargo fijo mensual de Gas Natural.
5. **G_Cont_Consumo**: `Contrib consumo %` Valor de la contribución o subsidio sobre el cargo fijo de Gas Natural.
6. **G_Cont_Cargo_Fijo**: `Contrib cargo fijo %` Valor de la contribución o subsidio sobre el cargo fijo de Gas Natural.

### Valores facturados Aseo
1. **As_Cargo_Fijo**: `Cargo Fijo` Valor cargo fijo mensual de Aseo.
2. **As_Variable_Apro**: `Cargo Variable Aprovechable` Valor consumo de toneladas aprovechables de Aseo.
3. **As_Contrib**: `Contribucion 100%` Contribución sobre toneladas de Aseo.
4. **As_Cargo_Var**: `Cargo Variable` Valor consumo total de Aseo.

### Valores facturados Alumbrado Público
1. **Al_Alum_Pub**: `Alumbrado Público` Valor total de Alumbrado Público.

### Columna Ajuste del peso
1. **Ajuste_Peso**: Columna técnica para ajuste interno del peso de la factura (si aplica). Relleno técnico (`0,00`) si no aplica. Se debe incluir en la Fila TOTAL.

### Columna de Totalización Final por Fila según OJF
1. **Total_Fila**: Sumatoria neta liquidada en la fila actual. (`Total Acueducto`, `Total Alcantarillado`, `Total Energía`, `Total Gas`, `Total Aseo`, `Total Alumbrado`, `Total Otras Entidades`, `Total a pagar Factura`).
 

### SECCIÓN III: VALORES TÉCNICOS Y COSTOS UNITARIOS

#### Componentes comunes a Acueducto, Alcantarillado, Energía y Gas
Estos valores son cruciales para auditorías detalladas y análisis de desglose de costos. Y se ubican de acuerdo al bloque de servicio correspondiente.

1. **Costo**:  `Costo ($)` Costo unitario del servicio principal (Acueducto, Alcantarilla, Energía, Gas, Aseo y Alumbrado no tienen este Costo).
2. **Consumo_Cant**: Cantidad física medida (Acueducto y Alcantarillado `m3`, Energía `kWh`, Gas `m3`. Para Aseo y Alumbrando no aplica, no hay un valor definido para este item).
3. **Unidad_Medida**: Unidad de medida (m3, kWh, Ton).
4.  **Medidor**: `'Serial del medidor (con apóstrofe)`. Solo aplica para Acueducto, Energía y Gas.
5.  **Lect_Ant**: `Lectura anterior` Lectura anterior registrada. Solo aplica para Acueducto, Energía y Gas.
6.  **Lect_Act**: `Lectura actual` Lectura actual capturada. Solo aplica para Acueducto, Energía y Gas.
7.  **Const**: Factor Multiplicador (Energía) o Constante de Corrección (Gas).

#### Componentes del Costo Acueducto
1.  **Ac_Cmapac_Cost**: `Cmapac - Cost` (valor unitario de administración Acueducto).
2.  **Ac_Cmpac_Unitari**: `Cmpac Unitari`. (valor unitario Cmpac).
3.  **Ac_Cmpac_Total**: `Cmpac Total`. (valor total Cmpac).
4.  **Ac_Cmt Unitario**: `Cmt Unitario`. (valor unitario Cmt).
5.  **Ac_Cmt_Total**: `Cmt Total`. (valor total Cmt).

### Componentes del Costo Alcantarillado
1.  **Al_Cmt_Unitario**: `Cmt Unitario` (valor unitario Cmt Alcantarillado).
2.  **Al_Cmt_Total**: `Cmt Total` (valor total Cmt Alcantarillado).

### Componentes del Costo Energía
1. **E_CU_G**: `Generación` Componente Generación Energía ($/kWh).
2. **E_CU_T**: `Transmisión` Componente Transmisión Energía ($/kWh).
3. **E_CU_D**: `Distribución` Componente Distribución Energía ($/kWh).
4. **E_CU_C**: `Comercializac` Componente Comercialización Energía ($/kWh).
5. **E_CU_P**: `Pérdidas` Componente Pérdidas Energía ($/kWh).
6. **E_CU_R**: `Restricciones`Componente Restricciones Energía ($/kWh).

### Componentes del Costo Gas Natural
1. **G_CU_Compr_V**: `Compra` Compra Gas Variable unitaria.
2. **G_CU_Dist_V**: `Distribución` Distribución Gas Variable unitaria.
3. **G_CU_Transp7_V**: `Transporte 7` Valor unitario ID Dinámico (Gas).
4. **G_CU_Conf_V**: `Confiabilidad` Confiabilidad Gas Variable unitaria.
5. **G_CU_Com_V**: `Comercializac` Comercialización Gas Variable unitaria.
6. **G_CU_Transp_Gn_F**: `Transporte Gn` Valor fijo de transporte (Gas).
7. **G_CU_Compr8_F**: `Compresión 8` Valor fijo compresión (Gas).
8. **G_CU_Com_F**: `Comercializac` Comercialización Gas Fija 

### Componentes Residuos del periodo (ton) Aseo
1.  **As_Ton_NoAp**: `No Aprov - Ordinarios` Toneladas No Aprovechables (Aseo).
2.  **As_Ton_Barr**: `Barrido y limpieza` Toneladas Barrido y Limpieza (Aseo).
3.  **As_Ton_Limp**: `Limpieza urbana` Toneladas Limpieza Urbana (Aseo).
4.  **As_Ton_Rech**: `Rechazados` Toneladas Rechazados (Aseo).

### Componentes de Alumbrado Público
*No aplica desglose técnico adicional para Alumbrado Público.* Diligenciar relleno (`0,00`) en las columnas técnicas.

### SECCIÓN IV: AUDITORÍA Y METADATOS
1. **Alertas**: Auditoría de cuadre: **NORMAL** o **AUDITORIA**.
2. **Info_Reg_Json**: En formato JSON. Detalles adicionales no considerados y que no tengan una columna específica asignada.

---

## 3. ESTÁNDAR VISUAL DE SALIDA
*Formato obligatorio para la tabla Markdown final:*
El Admin debe generar la tabla Markdown asegurando que cada fila contenga exactamente los **delimitadores (`|`)** para garantizar que existan todas las  columnas. Las columnas son las definidas en el DICCIONARIO DETALLADO DE COLUMNAS y el nombre es el que se encuentra entre los **[NOMBRE COLUMNA]**. Respetar también el orden del protocolo de filas (OJF).

### Encabezados de Tabla (Copy-Paste Ready)
| ID_Unico | Periodo | Año | Sem | Tri | Bim | Mes | Mes_Num | Fecha_Fact | Fecha_Venc | Contrato | Ref_Pago | ID_Producto | Ciclo | Est | Tipo_Servicio | Desde | Hasta | Dias | Ac_Consumo | Ac_Cargo_Fijo | Ac_Contr_Cargo_Fijo | Ac_Cont_Consumo | Al_Consumo | Al_Cargo_Fijo | Al_Cont_Cargo_Fijo | Al_Cont_Consumo | E_Energía | E_Contr_Activa | G_Consumo | G_Cargo_Fijo | G_Cont_Consumo | G_Cont_Cargo_Fijo | As_Cargo_Fijo | As_Variable_Apro | As_Contrib | As_Cargo_Var | Al_Alum_Pub | Ajuste_Peso | Total_Fila | Costo | Consumo_Cant | Unidad_Medida | Medidor | Lect_Ant | Lect_Act | Const | Ac_Cmapac_Cost | Ac_Cmpac_Unitari | Ac_Cmpac_Total | Ac_Cmt Unitario | Ac_Cmt_Total | Al_Cmt_Unitario | Al_Cmt_Total | E_CU_G | E_CU_T | E_CU_D | E_CU_C | E_CU_P | E_CU_R | G_CU_Compr_V | G_CU_Dist_V | G_CU_Transp7_V | G_CU_Conf_V | G_CU_Com_V | G_CU_Transp_Gn_F | G_CU_Compr8_F | G_CU_Com_F | As_Ton_NoAp | As_Ton_Barr | As_Ton_Limp | As_Ton_Rech | Alertas | Info_Reg_Json |
|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|

### REGLA MAESTRA DE ESTRUCTURA Y AUDITORÍA (INTEGRIDAD TOTAL)
Esta sección rige la arquitectura final de la salida. El incumplimiento de esta estructura invalida la auditoría.

#### Regla de Extensión e Integridad Horizontal
Indivisibilidad: La Matriz Plana es una tabla única de N columnas que abarca desde ID_Unico hasta Info_Reg_Json.

Prohibición de Truncamiento: No se permite dividir la tabla, usar bloques de texto adicionales para "Valores Técnicos" o resumir datos fuera de las celdas. Si el dato existe en el PDF, debe ser una columna.

Relleno Técnico Obligatorio: Si una columna técnica (ej. E_CU_G) no aplica al servicio de la fila (ej. ACUE), o si el dato no está en el PDF, se debe registrar obligatoriamente como 0,00. Esto garantiza que todas las filas tengan exactamente la misma cantidad de columnas y alineación.

Flujo de Datos: La información debe fluir horizontalmente: Identidad → Financieros → Técnicos → Auditoría.

#### Definición de Columnas de Control (Sección IV)
Para las columnas finales de la matriz, se deben seguir estos criterios forenses:

Columna: Alertas

Función: Registro de hallazgos y anomalías detectadas.

Extracción: Debe listar: 1) Avisos de incrementos tarifarios futuros; 2) Mensajes de seguridad o fraude (ej. Ley 500); 3) Desviaciones de consumo significativas; 4) Errores de consistencia (ej. servicios con valor 0,00 que aparecen en el texto).

Formato: Texto corto separado por punto y coma (;). Si es limpio, colocar Sin Alertas.

Columna: Info_Reg_Json

Función: Encapsulamiento de metadatos técnicos y regulatorios.

Extracción: Crear un objeto JSON plano con llaves encontradas en los bloques de "Información Técnica" (usualmente al final del PDF).

Campos Requeridos (si existen): {"niu": "...", "circuito": "...", "transfor": "...", "ind_presion": "...", "software_facturacion": "..."}.

Formato: Cadena JSON válida. No usar bloques de código Markdown dentro de la celda, solo el texto del JSON.

## 4. PROTOCOLO DE AUTO-AUDITORÍA (PRE-ENTREGA)
*El Admin debe ejecutar esta lista de chequeo forense antes de emitir la tabla final:*
- [ ] Verificación de 8 filas por factura según OJF.
- [ ] Confirmación de que todas las columnas están presentes y en el orden correcto.
- [ ] Revisión de formatos de fecha (DD/MM/YYYY) y valores numéricos (uso de comas decimal).
- [ ] Comprobación de que los valores financieros y técnicos coinciden con los cálculos esperados.
- [ ] Validación de que las filas de servicios no presentes en el PDF tienen valores rellenados con `0,00`.
- [ ] Revisión de la columna "Alertas" para asegurar que refleja correctamente el estado de auditoría.
- [ ] Confirmación de que la columna "Info_Reg_Json" contiene información adicional relevante en formato JSON.

**FIN DE FICHA TÉCNICA EPM**
