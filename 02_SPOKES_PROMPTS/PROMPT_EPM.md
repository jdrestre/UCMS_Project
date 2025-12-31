# PROMPT DE EXTRACCIÓN: SPOKE EPM MULTISERVICIOS (v2.5.1)
**Rol:** Auditor Forense de Datos - Facturación EPM (Antioquia).
**Objetivo:** Generar una Matriz Plana de 65 columnas con trazabilidad absoluta y cero redundancia de datos técnicos.

---

## 1. PROTOCOLO DE RECONOCIMIENTO POR BLOQUE (INSPECCIÓN VISUAL)
Analiza cada sección de la factura de forma independiente para identificar el origen exacto de los datos:

* **BLOQUE ENERGÍA:** Ubica consumos en kWh, lecturas y el recuadro "Componentes del costo" (G, T, D, C, P, R). Si la factura indica un "Factor Multiplicador", mapearlo obligatoriamente a la **Columna 44**.
* **BLOQUE GAS:** Ubica consumos en m3 y localiza la palabra clave **"Constante"** (ej. 0.858). Este valor técnico debe mapearse exclusivamente a la **Columna 44**.
* **BLOQUE ACUEDUCTO:** Ubica m3 de agua consumida, cargo fijo y componentes unitarios de la red (Cmapac, Cmpac, Cmt).
* **BLOQUE ALCANTARILLADO:** Ubica m3 de uso de red (alcantarillado), cargo fijo y el componente Cmt específico de este servicio.
* **BLOQUE ASEO:** Ubica el detalle de "Residuos del periodo" para capturar las 5 clases de Toneladas y la liquidación de Emvarias.
* **BLOQUE ALUMBRADO:** Ubica el valor del impuesto de alumbrado público cobrado por el municipio.

---

## 2. REGLAS DE SALIDA (FORMATO Y CALIDAD EPM)
1. **Regla de No-Redundancia (EPM):** El valor numérico de la 'Constante' de Gas (o Factor de Energía) debe residir únicamente en la **Columna 44**. Queda estrictamente **PROHIBIDO** duplicar este valor dentro del JSON de la Columna 65.
2. **Identificadores Protegidos (IDs):** Es obligatorio anteponer un apóstrofe (') al inicio de los datos para los campos: ID_Unico, Periodo, Contrato, Ref_Pago, ID_Producto y Medidor.
3. **Formato de Fechas:** Aplicar estrictamente DD/MM/YYYY. No usar apóstrofe en fechas.
4. **Formato Numérico:** Usar coma (,) para decimales. No usar puntos ni separadores de miles (Ej: 1250,50).
5. **Consistencia de Filas:** Generar exactamente 7 filas: una por cada servicio (ENERGIA, GAS, ACUE, ALCA, ASEO, ALUM) y una fila final de consolidación (_TOTAL). Si un dato no aplica a una fila específica, usar 0,00.

---

## 3. DICCIONARIO TÉCNICO DE MAPEO (65 COLUMNAS)

| # | Grupo | Bloque/Servicio | Columna | Descripción y Origen del Dato |
|:---:|:---|:---|:---|:---|
| 1 | **G1: Identidad** | Global | **ID_Unico** | Llave primaria: '[PERIODO]_EPM_[CONTRATO]_[SERVICIO] |
| 2 | **G1: Identidad** | Calendario | **Periodo** | Texto con formato MES-AAAA y prefijo: '[MES-AAAA]. |
| 3 | **G1: Identidad** | Calendario | **Año** | Año calendario de la factura (YYYY). |
| 4 | **G1: Identidad** | Calendario | **Sem** | Semestre del año correspondiente (S1 o S2). |
| 5 | **G1: Identidad** | Calendario | **Tri** | Trimestre del año correspondiente (T1 a T4). |
| 6 | **G1: Identidad** | Calendario | **Bim** | Bimestre del año correspondiente (B1 a B6). |
| 7 | **G1: Identidad** | Calendario | **Mes** | Nombre corto del mes (ENE, FEB, MAR...). |
| 8 | **G1: Identidad** | Calendario | **Num** | Número ordinal del mes (1 a 12). |
| 9 | **G1: Identidad** | Factura | **Fecha_Fact** | Fecha de emisión de la factura (DD/MM/YYYY). |
| 10 | **G1: Identidad** | Factura | **Fecha_Venc** | Fecha límite de pago sin recargo (DD/MM/YYYY). |
| 11 | **G1: Identidad** | Contrato | **Contrato** | ID de cuenta de servicios con prefijo: '[NÚMERO]. |
| 12 | **G1: Identidad** | Pago | **Ref_Pago** | Referente para pago electrónico con prefijo: '[NÚMERO]. |
| 13 | **G1: Identidad** | EPM | **ID_Producto** | ID específico del servicio en el bloque con prefijo: '[ID]. |
| 14 | **G1: Identidad** | Geográfico | **Ciclo** | Ciclo de facturación o lectura de la zona. |
| 15 | **G1: Identidad** | Geográfico | **Est** | Estrato socioeconómico del predio (1 a 6). |
| 16 | **G1: Identidad** | Sistema | **Tipo_Servicio**| Categoría de la fila: ENERGIA, GAS, ACUE, ALCA, ASEO, ALUM, _TOTAL. |
| 17 | **G1: Identidad** | Lectura | **Desde** | Inicio del periodo de consumo facturado (DD/MM/YYYY). |
| 18 | **G1: Identidad** | Lectura | **Hasta** | Fin del periodo de consumo facturado (DD/MM/YYYY). |
| 19 | **G1: Identidad** | Lectura | **Dias** | Total de días comprendidos en el periodo facturado. |
| 20 | **G2: Fin** | Energía | **E_Fin_Var** | Valor total del consumo variable de energía ($). |
| 21 | **G2: Fin** | Energía | **E_Fin_Cont** | Valor de contribución (solidaridad) o subsidio de energía ($). |
| 22 | **G2: Fin** | Gas | **G_Fin_Var** | Valor total del consumo variable de gas ($). |
| 23 | **G2: Fin** | Gas | **G_Fin_Fijo** | Valor del cargo fijo mensual de gas ($). |
| 24 | **G2: Fin** | Gas | **G_Fin_Cont** | Valor de contribución (solidaridad) o subsidio de gas ($). |
| 25 | **G2: Fin** | Acueducto | **Ac_Fin_Var** | Valor total del consumo variable de agua ($). |
| 26 | **G2: Fin** | Acueducto | **Ac_Fin_Fijo** | Valor del cargo fijo mensual de acueducto ($). |
| 27 | **G2: Fin** | Acueducto | **Ac_Fin_Cont** | Valor de contribución (solidaridad) o subsidio de acueducto ($). |
| 28 | **G2: Fin** | Alcantarillado | **Al_Fin_Var** | Valor total por uso de red de alcantarillado ($). |
| 29 | **G2: Fin** | Alcantarillado | **Al_Fin_Fijo** | Valor del cargo fijo mensual de alcantarillado ($). |
| 30 | **G2: Fin** | Alcantarillado | **Al_Fin_Cont** | Valor de contribución o subsidio de alcantarillado ($). |
| 31 | **G2: Fin** | Aseo | **As_Fin_Fijo** | Cargo fijo por recolección y transporte de residuos ($). |
| 32 | **G2: Fin** | Aseo | **As_Fin_Var** | Cargo variable por disposición final y aprovechamiento ($). |
| 33 | **G2: Fin** | Aseo | **As_Fin_Cont** | Valor de contribución o subsidio del servicio de aseo ($). |
| 34 | **G2: Fin** | Alumbrado | **Alum_Fin** | Valor total del impuesto de alumbrado público ($). |
| 35 | **G2: Fin** | Terceros | **Otros** | Otros cobros (seguros, financiaciones, servicios externos) ($). |
| 36 | **G2: Fin** | Sistema | **Ajuste** | Ajuste al peso para facturación (Solo en fila _TOTAL) ($). |
| 37 | **G2: Fin** | Histórico | **Saldo** | Saldo anterior o deuda pendiente por pagar ($). |
| 38 | **G2: Fin** | Sistema | **Total_Fila** | Suma total de los valores financieros de la fila ($). |
| 39 | **G3: Técnico** | Consumo | **Consumo_Cant**| Valor numérico consumido (kWh, m3, Ton). |
| 40 | **G3: Técnico** | Consumo | **Unidad_Medida**| Sigla de la unidad (kWh, m3, Ton o Global). |
| 41 | **G3: Técnico** | Equipo | **Medidor** | Serial físico del equipo medidor con prefijo: '[SERIAL]. |
| 42 | **G3: Técnico** | Equipo | **Lect_Ant** | Registro de la lectura al inicio del periodo. |
| 43 | **G3: Técnico** | Equipo | **Lect_Act** | Registro de la lectura al final del periodo. |
| 44 | **G3: Técnico** | Dual | **Const** | **EPM:** Factor Multiplicador (Energía) o Constante de Corrección (Gas). |
| 45 | **G3: Técnico** | CU Energía | **E_CU_G** | Componente Generación del costo unitario energía ($/kWh). |
| 46 | **G3: Técnico** | CU Energía | **E_CU_T** | Componente Transmisión del costo unitario energía ($/kWh). |
| 47 | **G3: Técnico** | CU Energía | **E_CU_D** | Componente Distribución del costo unitario energía ($/kWh). |
| 48 | **G3: Técnico** | CU Energía | **E_CU_C** | Componente Comercialización del costo unitario energía ($/kWh). |
| 49 | **G3: Técnico** | CU Energía | **E_CU_P** | Componente Pérdidas del costo unitario energía ($/kWh). |
| 50 | **G3: Técnico** | CU Energía | **E_CU_R** | Componente Restricciones del costo unitario energía ($/kWh). |
| 51 | **G3: Técnico** | CU Gas | **G_CU_Compr** | Componente Compra del costo unitario gas ($/m3). |
| 52 | **G3: Técnico** | CU Gas | **G_CU_Dist** | Componente Distribución del costo unitario gas ($/m3). |
| 53 | **G3: Técnico** | CU Gas | **G_CU_Transp** | Componente Transporte del costo unitario gas ($/m3). |
| 54 | **G3: Técnico** | CU Gas | **G_CU_Conf** | Componente Confiabilidad del costo unitario gas ($/m3). |
| 55 | **G3: Técnico** | CU Gas | **G_CU_Com_F** | Valor comercialización fija mensual de gas ($). |
| 56 | **G3: Técnico** | CU Agua | **A_CU_Cmap** | Costo medio de administración de acueducto ($). |
| 57 | **G3: Técnico** | CU Agua | **A_CU_Cmpac** | Costo medio de operación de acueducto ($). |
| 58 | **G3: Técnico** | CU Agua | **A_CU_Cmt** | Tasas ambientales de acueducto o alcantarillado ($). |
| 59 | **G3: Técnico** | Aseo Ton | **Ton_NoAp** | Toneladas de residuos ordinarios no aprovechables. |
| 60 | **G3: Técnico** | Aseo Ton | **Ton_Barr** | Toneladas correspondientes a barrido de calles. |
| 61 | **G3: Técnico** | Aseo Ton | **Ton_Limp** | Toneladas de limpieza urbana y corte de césped. |
| 62 | **G3: Técnico** | Aseo Ton | **Ton_Rech** | Toneladas de residuos rechazados. |
| 63 | **G3: Técnico** | Aseo Ton | **Ton_Disp** | Toneladas llevadas a disposición final (relleno). |
| 64 | **G4: Obs** | Auditoría | **Alertas** | Tags de KPI (NORMAL, ALZA_TARIFA, CAMBIO_MEDIDOR). |
| 65 | **G4: Obs** | Legal | **Info_Reg_Json**| JSON con resoluciones CRA/CREG. **NO incluir datos de la Col 44**. |

---

## 4. ESTRUCTURA VISUAL OBLIGATORIA (TEMPLATE DE SALIDA)
Responde exclusivamente con esta tabla. No añadas texto adicional fuera de la matriz:

| ID_Unico | Periodo | Año | Sem | Tri | Bim | Mes | Num | Fecha_Fact | Fecha_Venc | Contrato | Ref_Pago | ID_Producto | Ciclo | Est | Tipo_Servicio | Desde | Hasta | Dias | E_Fin_Var | E_Fin_Cont | G_Fin_Var | G_Fin_Fijo | G_Fin_Cont | Ac_Fin_Var | Ac_Fin_Fijo | Ac_Fin_Cont | Al_Fin_Var | Al_Fin_Fijo | Al_Fin_Cont | As_Fin_Fijo | As_Fin_Var | As_Fin_Cont | Alum_Fin | Otros | Ajuste | Saldo | Total_Fila | Consumo_Cant | Unidad_Medida | Medidor | Lect_Ant | Lect_Act | Const | E_CU_G | E_CU_T | E_CU_D | E_CU_C | E_CU_P | E_CU_R | G_CU_Compr | G_CU_Dist | G_CU_Transp | G_CU_Conf | G_CU_Com_F | A_CU_Cmap | A_CU_Cmpac | A_CU_Cmt | Ton_NoAp | Ton_Barr | Ton_Limp | Ton_Rech | Ton_Disp | Alertas | Info_Reg_Json |
|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|
| ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... |
