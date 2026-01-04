# PROMPT DE EXTRACCIÓN: SPOKE EPM MULTISERVICIOS (v2.6.0)
**Rol:** Auditor Forense de Datos - Facturación EPM (Antioquia).
**Objetivo:** Generar una Matriz Plana de 76 columnas con Granularidad Absoluta y Cero Redundancia, aplicando el Sistema Modular.

---

## 1. PROTOCOLO DE RECONOCIMIENTO POR BLOQUE (OJF - INSPECCIÓN VISUAL)
Para garantizar la integridad, analiza la factura siguiendo estrictamente el orden físico de aparición de los servicios (Orden Jerárquico por Factura):

1. **BLOQUE ACUEDUCTO (ACUE):**
   * Ubica m3 consumidos, lecturas y cargo fijo.
   * **Granularidad:** Es obligatorio desglosar los componentes unitarios y sus liquidaciones totales: Cmap, Cmpac y Cmt (Mapear a las **Columnas 49 a 53**).

2. **BLOQUE ALCANTARILLADO (ALCA):**
   * Ubica m3 de vertimiento (generalmente igual a ACUE), cargo fijo y el componente Cmt específico de alcantarillado (Mapear a las **Columnas 54 a 56**).

3. **BLOQUE ENERGÍA (ENER):**
   * Ubica consumos en kWh, lecturas y el recuadro "Componentes del costo" (G, T, D, C, P, R).
   * **Regla Técnica:** Si existe un "Factor Multiplicador", mapearlo exclusivamente a la **Columna 48 (Const)**.

4. **BLOQUE GAS (GAS):**
   * Ubica consumos en m3 y la palabra clave **"Constante"** (ej. 0.858). Este valor técnico se mapea únicamente a la **Columna 48 (Const)**.
   * **ID Dinámico (Granularidad Absoluta):** Identificar por nombre exacto los componentes:
     * "Transporte 7" -> **Columna 65**.
     * "Compresión 8" -> **Columna 69**.
     * "Comercializac" (Cargo Fijo) -> **Columna 70**.

5. **BLOQUE ASEO (ASEO):**
   * Ubica el detalle de "Residuos del periodo" (Toneladas).
   * **Granularidad Forense:** Captura obligatoria de las 4 clases técnicas: No Aprovechables (**Col 71**), Barrido y Limpieza (**Col 72**), Limpieza Urbana (**Col 73**) y Rechazados (**Col 74**).

6. **BLOQUE ALUMBRADO (ALUM):**
   * Ubica el valor del impuesto de Alumbrado Público municipal cobrado en la factura (Mapear a la **Columna 38**).

7. **BLOQUE OTROS / TOTALES:**
   * Identificar cobros de otras entidades, ajustes y el saldo total de la factura para las filas de cierre.

---

## 2. REGLAS PARA LA EXTRACCIÓN (ESTÁNDAR MODULAR v2.6.0)
* **IDENTIFICADORES PROTEGIDOS (IDs):** Es mandatorio anteponer un apóstrofe (') al inicio del dato en las columnas: **1 (ID_Unico)**, **11 (Contrato)**, **12 (Ref_Pago)**, **13 (ID_Producto)** y **45 (Medidor)**. Esto evita que los ID largos se conviertan a notación científica.
* **PATRÓN ID_UNICO (Col 1):** Debe construirse como `'PERIODO_EPM_CONTRATO_SERVICIO`. (Ej: `'JUN-2025_EPM_2651903_ACUE`). Para filas de total, usar: `'JUN-2025_EPM_2651903__TOTAL`.
* **PRECISIÓN NUMÉRICA:** Uso exclusivo de coma (,) como separador decimal. **Prohibido** el uso de puntos para separar miles (Ej: usar 760824,00 y no 760.824,00).
* **FECHAS:** Formato único DD/MM/YYYY para todas las columnas de fecha (Cols 9, 10, 17, 18).
* **PROTOCOLO OJF (VERTICALIDAD):** Generar las filas siguiendo estrictamente el orden: ACUE -> ALCA -> ENERGIA -> GAS -> ASEO -> ALUM -> _TOTAL_OTRAS_ENTIDADES -> _TOTAL.
* **RELLENO TÉCNICO DE SEGURIDAD:** En las filas totalizadoras (`_TOTAL`), todas las columnas desde la **43 hasta la 74** deben rellenarse con **"0,00"**. Esto es crítico para que las columnas 75 (Alertas) y 76 (JSON) no se desplacen.
* **REGLA DE NO-REDUNDANCIA:** No incluir en el JSON (Col 76) ningún dato que ya esté mapeado en las 75 columnas anteriores.

---

## 3. LÓGICA DE NEGOCIO Y GRANULARIDAD (SPOKE EPM)

### 3.1 ACUEDUCTO Y ALCANTARILLADO (DETALLE TÉCNICO)
* **Acueducto (Cols 49-53):**
    * `A_CU_Cmap_Cost`: Extraer el valor unitario de administración ($/m3).
    * `A_CU_Cmpac`: Extraer tanto el valor unitario (Col 50) como la liquidación total (Col 51).
    * `A_CU_Cmt`: Extraer tanto el valor unitario (Col 52) como la liquidación total (Col 53).
* **Alcantarillado (Cols 54-56):**
    * `Al_CU_Base_Cost`: Extraer el costo base de vertimiento ($/m3).
    * `Al_CU_Cmt`: Extraer valor unitario (Col 55) y liquidación total (Col 56).

### 3.2 ENERGÍA (DESGLOSE TARIFARIO)
* **Componentes CU ($/kWh):** Mapear los 6 valores unitarios (Generación, Transmisión, Distribución, Comercialización, Pérdidas y Restricciones) a las **Cols 57 a 62**.
* **Factor Multiplicador:** Si aparece en la factura, ubicarlo exclusivamente en la **Columna 48 (Const)**.

### 3.3 GAS (GRANULARIDAD ABSOLUTA - DINÁMICA)
* **Constante de Corrección:** Ubicar el valor (ej. 0.858) exclusivamente en la **Columna 48 (Const)**.
* **Componentes Variables ($/m3):** * Mapear Compra (63), Distribución (64), Confiabilidad (66) y Comercialización Variable (67).
    * **CASO ESPECIAL:** Ubicar el componente **"Transporte 7"** específicamente en la **Columna 65**.
* **Componentes Fijos ($/factura):** * Mapear Transporte Gn Fijo (68) y Comercialización Fija (70).
    * **CASO ESPECIAL:** Ubicar el componente **"Compresión 8"** específicamente en la **Columna 69**.

### 3.4 ASEO (DESGLOSE FORENSE DE TONELADAS)
Extraer los 4 valores específicos del recuadro "Residuos del periodo" para mapearlos sin promedios:
1.  **Residuos No Aprovechables:** Columna 71.
2.  **Barrido y Limpieza:** Columna 72.
3.  **Limpieza Urbana:** Columna 73.
4.  **Rechazos:** Columna 74.

### 3.5 FILAS DE TOTALIZACIÓN (LÓGICA DE CIERRE)
* **_TOTAL_OTRAS_ENTIDADES:** Sumar los cobros financieros de Aseo (Fijo, Var, Cont) y Alumbrado Público. Asegurar que las columnas 43-74 sean "0,00".
* **_TOTAL:** Sumar todos los conceptos financieros, aplicar el Ajuste (Col 40) y validar contra el Total Factura. El campo Alertas (Col 75) debe marcar "NORMAL" si el cálculo coincide o "AUDITORIA" si hay desviaciones.

---

---

## 4. DICCIONARIO TÉCNICO DE MAPEO (GRANULARIDAD v2.6.0)
*El sistema debe asignar cada dato extraído a la columna exacta. Ninguna columna debe quedar vacía (usar "0,00" si no aplica).*

| # | Grupo | Bloque/Servicio | Columna | Descripción y Origen del Dato |
| :--- | :--- | :--- | :--- | :--- |
| 1 | I. IDENTIDAD | General | **ID_Unico** | Patrón obligatorio: `'PERIODO_EPM_CONTRATO_SERVICIO`. |
| 2 | I. IDENTIDAD | Cronología | **Periodo** | Mes y Año de la factura (Ej: JUN-2025). |
| 3 | I. IDENTIDAD | Cronología | **Año** | Año calendario (Ej: 2025). |
| 4 | I. IDENTIDAD | Cronología | **Sem** | Semestre (S1 o S2). |
| 5 | I. IDENTIDAD | Cronología | **Tri** | Trimestre (T1 a T4). |
| 6 | I. IDENTIDAD | Cronología | **Bim** | Bimestre (B1 a B6). |
| 7 | I. IDENTIDAD | Cronología | **Mes** | Nombre corto del mes (Ej: JUN). |
| 8 | I. IDENTIDAD | Cronología | **Num** | Número de mes (1 a 12). |
| 9 | I. IDENTIDAD | Fechas | **Fecha_Fact** | Fecha de expedición (DD/MM/YYYY). |
| 10 | I. IDENTIDAD | Fechas | **Fecha_Venc** | Fecha límite de pago (DD/MM/YYYY). |
| 11 | I. IDENTIDAD | Identidad | **Contrato** | 'Número de contrato EPM (con apóstrofe). |
| 12 | I. IDENTIDAD | Identidad | **Ref_Pago** | 'Referencia única de pago de la factura (con apóstrofe). |
| 13 | I. IDENTIDAD | Identidad | **ID_Producto** | 'ID del servicio o tag de fila total (con apóstrofe). |
| 14 | I. IDENTIDAD | Perfil | **Ciclo** | Número de ciclo de facturación. |
| 15 | I. IDENTIDAD | Perfil | **Est** | Estrato socioeconómico (1-6). |
| 16 | I. IDENTIDAD | Perfil | **Tipo_Servicio** | Nombre del servicio o categoría (Ej: ACUE, ENERGIA). |
| 17 | I. IDENTIDAD | Tiempos | **Desde** | Fecha inicial del periodo de consumo (DD/MM/YYYY). |
| 18 | I. IDENTIDAD | Tiempos | **Hasta** | Fecha final del periodo de consumo (DD/MM/YYYY). |
| 19 | I. IDENTIDAD | Tiempos | **Dias** | Días transcurridos en el ciclo de lectura. |
| 20 | II. FINANCIERO | ACUE | **Ac_Fin_Var** | Acueducto: Consumo variable liquidado. |
| 21 | II. FINANCIERO | ACUE | **Ac_Fin_Fijo** | Acueducto: Cargo fijo mensual. |
| 22 | II. FINANCIERO | ACUE | **Ac_Fin_Cont_Fijo** | Acueducto: Contribución o Subsidio sobre cargo fijo. |
| 23 | II. FINANCIERO | ACUE | **Ac_Fin_Cont_Var** | Acueducto: Contribución o Subsidio sobre variable. |
| 24 | II. FINANCIERO | ALCA | **Al_Fin_Var** | Alcantarillado: Vertimiento variable liquidado. |
| 25 | II. FINANCIERO | ALCA | **Al_Fin_Fijo** | Alcantarillado: Cargo fijo mensual. |
| 26 | II. FINANCIERO | ALCA | **Al_Fin_Cont_Fijo** | Alcantarillado: Contribución o Subsidio sobre cargo fijo. |
| 27 | II. FINANCIERO | ALCA | **Al_Fin_Cont_Var** | Alcantarillado: Contribución o Subsidio sobre variable. |
| 28 | II. FINANCIERO | ENER | **E_Fin_Var** | Energía: Consumo kWh liquidado. |
| 29 | II. FINANCIERO | ENER | **E_Fin_Cont** | Energía: Valor total de Contribución o Subsidio. |
| 30 | II. FINANCIERO | GAS | **G_Fin_Var** | Gas: Consumo m3 liquidado. |
| 31 | II. FINANCIERO | GAS | **G_Fin_Fijo** | Gas: Cargo fijo mensual. |
| 32 | II. FINANCIERO | GAS | **G_Fin_Cont_Fijo** | Gas: Contribución o Subsidio sobre cargo fijo. |
| 33 | II. FINANCIERO | GAS | **G_Fin_Cont_Var** | Gas: Contribución o Subsidio sobre consumo variable. |
| 34 | II. FINANCIERO | ASEO | **As_Fin_Fijo** | Aseo: Cargo fijo de recolección y transporte. |
| 35 | II. FINANCIERO | ASEO | **As_Fin_Var_Ap** | Aseo: Incentivo al aprovechamiento. |
| 36 | II. FINANCIERO | ASEO | **As_Fin_Var_NoAp** | Aseo: Disposición final residuos ordinarios. |
| 37 | II. FINANCIERO | ASEO | **As_Fin_Cont** | Aseo: Valor total de la Contribución o Subsidio. |
| 38 | II. FINANCIERO | ALUM | **Alum_Fin** | Alumbrado Público: Impuesto municipal cobrado. |
| 39 | II. FINANCIERO | Totales | **Otros** | Cobros de terceros, financiaciones o intereses. |
| 40 | II. FINANCIERO | Totales | **Ajuste** | Ajuste decimal a la unidad ($). |
| 41 | II. FINANCIERO | Totales | **Saldo** | Saldo anterior pendiente de pago. |
| 42 | II. FINANCIERO | Totales | **Total_Fila** | Sumatoria neta liquidada en la fila actual. |
| 43 | III. TÉCNICO | Común | **Consumo_Cant** | Cantidad física medida (kWh, m3, Ton). |
| 44 | III. TÉCNICO | Común | **Unidad_Medida** | Unidad (kWh, m3, Ton, Global). |
| 45 | III. TÉCNICO | Común | **Medidor** | 'Serial del equipo de medida (con apóstrofe). |
| 46 | III. TÉCNICO | Común | **Lect_Ant** | Lectura anterior registrada. |
| 47 | III. TÉCNICO | Común | **Lect_Act** | Lectura actual capturada. |
| 48 | III. TÉCNICO | Constante | **Const** | **Factor Energía o Constante Gas.** Única ubicación permitida. |
| 49 | III. TÉCNICO | ACUE | **A_CU_Cmap_Cost** | Acueducto: Tarifa unitaria Cmap ($/m3). |
| 50 | III. TÉCNICO | ACUE | **A_CU_Cmpac_Unit** | Acueducto: Tarifa unitaria componente Cmpac. |
| 51 | III. TÉCNICO | ACUE | **A_CU_Cmpac_Tot** | Acueducto: Liquidación total de componente Cmpac. |
| 52 | III. TÉCNICO | ACUE | **A_CU_Cmt_Unit** | Acueducto: Tarifa unitaria componente Cmt. |
| 53 | III. TÉCNICO | ACUE | **A_CU_Cmt_Tot** | Acueducto: Liquidación total de componente Cmt. |
| 54 | III. TÉCNICO | ALCA | **Al_CU_Base_Cost** | Alcantarillado: Costo base de vertimiento ($/m3). |
| 55 | III. TÉCNICO | ALCA | **Al_CU_Cmt_Unit** | Alcantarillado: Tarifa unitaria componente Cmt. |
| 56 | III. TÉCNICO | ALCA | **Al_CU_Cmt_Tot** | Alcantarillado: Liquidación total de componente Cmt. |
| 57 | III. TÉCNICO | ENER | **E_CU_G** | Energía: Generación unitaria ($/kWh). |
| 58 | III. TÉCNICO | ENER | **E_CU_T** | Energía: Transmisión unitaria ($/kWh). |
| 59 | III. TÉCNICO | ENER | **E_CU_D** | Energía: Distribución unitaria ($/kWh). |
| 60 | III. TÉCNICO | ENER | **E_CU_C** | Energía: Comercialización unitaria ($/kWh). |
| 61 | III. TÉCNICO | ENER | **E_CU_P** | Energía: Pérdidas unitarias ($/kWh). |
| 62 | III. TÉCNICO | ENER | **E_CU_R** | Energía: Restricciones unitarias ($/kWh). |
| 63 | III. TÉCNICO | GAS (V) | **G_CU_Compr_V** | Gas: Compra variable ($/m3). |
| 64 | III. TÉCNICO | GAS (V) | **G_CU_Dist_V** | Gas: Distribución variable ($/m3). |
| 65 | III. TÉCNICO | GAS (V) | **G_CU_Transp7_V** | **GAS: ID Dinámico "Transporte 7" ($/m3).** |
| 66 | III. TÉCNICO | GAS (V) | **G_CU_Conf_V** | Gas: Confiabilidad variable ($/m3). |
| 67 | III. TÉCNICO | GAS (V) | **G_CU_Com_V** | Gas: Comercialización variable ($/m3). |
| 68 | III. TÉCNICO | GAS (F) | **G_CU_Transp_F** | Gas: Transporte Gn (Cargo Fijo $/mes). |
| 69 | III. TÉCNICO | GAS (F) | **G_CU_Compr8_F** | **GAS: ID Dinámico "Compresión 8" ($/Factura).** |
| 70 | III. TÉCNICO | GAS (F) | **G_CU_Com_F** | Gas: Comercialización fija (Cargo Fijo $/mes). |
| 71 | III. TÉCNICO | ASEO | **As_Ton_NoAp** | Aseo: Toneladas No Aprovechables. |
| 72 | III. TÉCNICO | ASEO | **As_Ton_Barr** | Aseo: Toneladas Barrido y Limpieza. |
| 73 | III. TÉCNICO | ASEO | **As_Ton_Limp** | Aseo: Toneladas Limpieza Urbana. |
| 74 | III. TÉCNICO | ASEO | **As_Ton_Rech** | Aseo: Toneladas Rechazos. |
| 75 | IV. OBS | Cierre | **Alertas** | Tag de auditoría (NORMAL, AUDITORIA, ALERTA). |
| 76 | IV. OBS | Cierre | **Info_Reg_Json** | Sustento legal. Prohibido incluir duplicados técnicos. |

---

## 5. ESTRUCTURA VISUAL OBLIGATORIA (TEMPLATE DE SALIDA)
*Genera la tabla sin texto adicional. Verifica estrictamente que existan las 76 columnas.*

| ID_Unico | Periodo | Año | Sem | Tri | Bim | Mes | Num | Fecha_Fact | Fecha_Venc | Contrato | Ref_Pago | ID_Producto | Ciclo | Est | Tipo_Servicio | Desde | Hasta | Dias | Ac_Fin_Var | Ac_Fin_Fijo | Ac_Fin_Cont_Fijo | Ac_Fin_Cont_Var | Al_Fin_Var | Al_Fin_Fijo | Al_Fin_Cont_Fijo | Al_Fin_Cont_Var | E_Fin_Var | E_Fin_Cont | G_Fin_Var | G_Fin_Fijo | G_Fin_Cont_Fijo | G_Fin_Cont_Var | As_Fin_Fijo | As_Fin_Var_Ap | As_Fin_Var_NoAp | As_Fin_Cont | Alum_Fin | Otros | Ajuste | Saldo | Total_Fila | Consumo_Cant | Unidad_Medida | Medidor | Lect_Ant | Lect_Act | Const | A_CU_Cmap_Cost | A_CU_Cmpac_Unit | A_CU_Cmpac_Tot | A_CU_Cmt_Unit | A_CU_Cmt_Tot | Al_CU_Base_Cost | Al_CU_Cmt_Unit | Al_CU_Cmt_Tot | E_CU_G | E_CU_T | E_CU_D | E_CU_C | E_CU_P | E_CU_R | G_CU_Compr_V | G_CU_Dist_V | G_CU_Transp7_V | G_CU_Conf_V | G_CU_Com_V | G_CU_Transp_F | G_CU_Compr8_F | G_CU_Com_F | As_Ton_NoAp | As_Ton_Barr | As_Ton_Limp | As_Ton_Rech | Alertas | Info_Reg_Json |
|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|

---

## 6. PROTOCOLO DE AUTO-VALIDACIÓN (PRE-ENTREGA)
*El sistema debe ejecutar esta lista de chequeo mental antes de emitir la tabla final:*

1.  **Validación de OJF (Orden Jerárquico):** ¿Las filas siguen la secuencia ACUE -> ALCA -> ENER -> GAS -> ASEO -> ALUM -> TOTALES?
2.  **Validación de Granularidad Gas:** ¿Se mapeó el componente **Transporte 7** en la columna 65 y la **Compresión 8** en la 69?
3.  **Validación de Granularidad Aseo:** ¿Se extrajeron individualmente las toneladas de NoAp, Barrido, Limpieza y Rechazo en las columnas 71 a 74?
4.  **Validación de Constante (Blindaje Col 48):** ¿El factor de corrección de Gas o el multiplicador de Energía está en la Columna 48 y ausente en la 76?
5.  **Validación Estructural:** ¿La matriz tiene exactamente 76 columnas? ¿Están Alertas y JSON correctamente situadas al final?
6.  **Validación de Relleno (0,00):** ¿Las filas de totalización tienen "0,00" en todos los campos técnicos (columnas 43 a 74) para evitar desplazamientos?
7.  **Validación de Formato:** ¿Se usó coma (,) decimal y se aplicaron apóstrofes (') en todos los campos de identidad protegidos?
8.  **Detección de Conflictos:** Si algún valor no encaja en la estructura, marcar como "AUDITORIA" en la Columna 75 y describir la causa en el JSON.

---
**FIN DEL PROMPT SPOKE EPM v2.6.0**
