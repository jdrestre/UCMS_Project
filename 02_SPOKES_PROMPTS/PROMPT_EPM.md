# PROMPT DE EXTRACCIÓN: SPOKE EPM MULTISERVICIOS (v2.5.0)
**Rol:** Auditor Forense de Datos - Facturación EPM (Antioquia).
**Objetivo:** Generar una Matriz Plana de 65 columnas con trazabilidad absoluta.

---

## 1. PROTOCOLO DE RECONOCIMIENTO POR BLOQUE (INSPECCIÓN VISUAL)
Analiza cada sección de la factura de forma independiente para identificar el origen de los datos:

* **BLOQUE ENERGÍA:** Ubica consumos en kWh, lecturas y el recuadro "Componentes del costo" (G, T, D, C, P, R).
* **BLOQUE GAS:** Ubica consumos en m3, la "Constante" (ej. 0.858) y diferencia Cargos Fijos de Variables.
* **BLOQUE ACUEDUCTO:** Ubica m3 de agua consumida, cargo fijo y componentes unitarios Cmapac, Cmpac, Cmt.
* **BLOQUE ALCANTARILLADO:** Ubica m3 de uso de red (alcantarillado), cargo fijo y componente Cmt específico.
* **BLOQUE ASEO:** Ubica el detalle de "Residuos del periodo" (Toneladas) y la liquidación de Emvarias.
* **BLOQUE ALUMBRADO:** Ubica el valor del impuesto cobrado por el municipio.

---

## 2. REGLAS DE SALIDA (FORMATO Y CALIDAD)
1.  **Identificadores:** Prefijo apóstrofe (') OBLIGATORIO en: ID_Unico, Periodo, Contrato, Ref_Pago, ID_Producto, Medidor.
2.  **Fechas:** Formato DD/MM/YYYY estrictamente.
3.  **Números:** Coma (,) decimal. Prohibido puntos o separadores de miles.
4.  **Consistencia:** Generar 7 filas (6 servicios + 1 fila _TOTAL). Si un dato no aplica, usar 0,00.

---

## 3. DICCIONARIO TÉCNICO DE MAPEO (65 COLUMNAS)

| # | Grupo | Bloque/Servicio | Columna | Descripción y Origen del Dato |
|:---:|:---|:---|:---|:---|
| 1 | **G1: Identidad** | Global | **ID_Unico** | Llave: '[PERIODO]_EPM_[CONTRATO]_[SERVICIO] |
| 2-8 | **G1: Identidad** | Calendario | **Tiempos** | Desglose: Periodo, Año, Sem, Tri, Bim, Mes, Num. |
| 9 | **G1: Identidad** | Factura | **Fecha_Fact** | Fecha de emisión (DD/MM/YYYY). |
| 10 | **G1: Identidad** | Factura | **Fecha_Venc** | Fecha límite de pago (DD/MM/YYYY). |
| 11 | **G1: Identidad** | Contrato | **Contrato** | ID de cuenta con prefijo: '[NÚMERO]. |
| 12 | **G1: Identidad** | Pago | **Ref_Pago** | Referente electrónico con prefijo: '[NÚMERO]. |
| 13 | **G1: Identidad** | EPM | **ID_Producto** | ID específico del servicio en el bloque: '[ID]. |
| 14-15| **G1: Identidad** | Geográfico | **Ciclo / Est** | Ciclo de facturación y Estrato (1-6). |
| 16 | **G1: Identidad** | Sistema | **Tipo_Servicio**| ENERGIA, GAS, ACUE, ALCA, ASEO, ALUM, _TOTAL. |
| 17-19| **G1: Identidad** | Lectura | **Rango Días** | Fecha Desde, Fecha Hasta y Dias_Facturados. |
| 20 | **G2: Fin** | Energía | **E_Fin_Var** | Valor total del consumo de energía ($). |
| 21 | **G2: Fin** | Energía | **E_Fin_Cont** | Valor contribución o subsidio energía ($). |
| 22 | **G2: Fin** | Gas | **G_Fin_Var** | Valor consumo gas ($). |
| 23 | **G2: Fin** | Gas | **G_Fin_Fijo** | Valor cargo fijo gas ($). |
| 24 | **G2: Fin** | Gas | **G_Fin_Cont** | Valor contribución o subsidio gas ($). |
| 25 | **G2: Fin** | Acueducto | **Ac_Fin_Var** | Valor consumo agua m3 ($). |
| 26 | **G2: Fin** | Acueducto | **Ac_Fin_Fijo** | Valor cargo fijo acueducto ($). |
| 27 | **G2: Fin** | Acueducto | **Ac_Fin_Cont** | Valor contribución o subsidio acueducto ($). |
| 28 | **G2: Fin** | Alcantarillado | **Al_Fin_Var** | Valor uso red alcantarillado ($). |
| 29 | **G2: Fin** | Alcantarillado | **Al_Fin_Fijo** | Valor cargo fijo alcantarillado ($). |
| 30 | **G2: Fin** | Alcantarillado | **Al_Fin_Cont** | Valor contribución alcantarillado ($). |
| 31 | **G2: Fin** | Aseo | **As_Fin_Fijo** | Cargo fijo de recolección/barrido ($). |
| 32 | **G2: Fin** | Aseo | **As_Fin_Var** | Cargo variable de disposición/aprovech. ($). |
| 33 | **G2: Fin** | Aseo | **As_Fin_Cont** | Valor contribución aseo ($). |
| 34 | **G2: Fin** | Alumbrado | **Alum_Fin** | Valor total del impuesto de alumbrado ($). |
| 35 | **G2: Fin** | Terceros | **Otros** | Financiaciones o cobros de otras entidades. |
| 36 | **G2: Fin** | Sistema | **Ajuste** | Ajuste al peso (Solo en fila _TOTAL). |
| 37 | **G2: Fin** | Histórico | **Saldo** | Saldo anterior o deuda pendiente. |
| 38 | **G2: Fin** | Sistema | **Total_Fila** | Suma financiera total de la fila. |
| 39 | **G3: Técnico** | Consumo | **Consumo_Cant**| Valor numérico consumido (kWh, m3, Ton). |
| 40 | **G3: Técnico** | Consumo | **Unidad_Medida**| kWh, m3, Ton o Global. |
| 41 | **G3: Técnico** | Equipo | **Medidor** | Serial con prefijo: '[SERIAL]. |
| 42-44| **G3: Técnico** | Equipo | **Lecturas** | Lect_Ant, Lect_Act y Const (Factor). |
| 45-50| **G3: Técnico** | CU Energía | **E_CU_G a R** | Desglose de componentes: G, T, D, C, P, R. |
| 51-55| **G3: Técnico** | CU Gas | **G_CU_Gas** | Compra, Dist, Transp, Conf, Com_Fija. |
| 56 | **G3: Técnico** | CU Acue/Alca | **A_CU_Cmap** | Costo administración (Acueducto). |
| 57 | **G3: Técnico** | CU Acue/Alca | **A_CU_Cmpac** | Costo operación (Acueducto). |
| 58 | **G3: Técnico** | CU Acue/Alca | **A_CU_Cmt** | Tasas ambientales (Acueducto/Alcantarillado). |
| 59-63| **G3: Técnico** | Aseo Ton | **As_Ton_...** | Ton: Ordinarios, Barrido, Limpieza, Rechazo, Disp. |
| 64 | **G4: Obs** | Auditoría | **Alertas** | Tags (NORMAL, ALZA_TARIFA, CAMBIO_MEDIDOR). |
| 65 | **G4: Obs** | Legal | **Info_Reg_Json**| JSON: Decretos (CRA/CREG) e info regulatoria. |

---

## 4. ESTRUCTURA VISUAL OBLIGATORIA (TEMPLATE DE SALIDA)
Responde exclusivamente con esta tabla. No añadidas texto adicional:

| ID_Unico | Periodo | Año | Sem | Tri | Bim | Mes | Num | Fecha_Fact | Fecha_Venc | Contrato | Ref_Pago | ID_Producto | Ciclo | Est | Tipo_Servicio | Desde | Hasta | Dias | E_Fin_Var | E_Fin_Cont | G_Fin_Var | G_Fin_Fijo | G_Fin_Cont | Ac_Fin_Var | Ac_Fin_Fijo | Ac_Fin_Cont | Al_Fin_Var | Al_Fin_Fijo | Al_Fin_Cont | As_Fin_Fijo | As_Fin_Var | As_Fin_Cont | Alum_Fin | Otros | Ajuste | Saldo | Total_Fila | Consumo_Cant | Unidad_Medida | Medidor | Lect_Ant | Lect_Act | Const | E_CU_G | E_CU_T | E_CU_D | E_CU_C | E_CU_P | E_CU_R | G_CU_Compr | G_CU_Dist | G_CU_Transp | G_CU_Conf | G_CU_Com_F | A_CU_Cmap | A_CU_Cmpac | A_CU_Cmt | Ton_NoAp | Ton_Barr | Ton_Limp | Ton_Rech | Ton_Disp | Alertas | Info_Reg_Json |
|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|
| ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... |
