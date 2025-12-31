# ESTÁNDAR DE SALIDA UNIVERSAL UCMS (v2.5.0)
**Estado:** VIGENTE | **Referencia de Conocimiento** (No de ejecución directa).

## SECCIÓN A: REGLAS MAESTRAS (GLOBALES)
* **Formato Fecha:** DD/MM/YYYY (Excel Ready).
* **ID Protegido:** Uso de apóstrofe (`'`) en: Contrato, Ref_Pago, ID_Producto, Medidor, ID_Unico.
* **Separador:** Coma (`,`) para decimales.

---

## SECCIÓN B: MATRIZ DE REFERENCIA - SPOKE EPM (65 COLUMNAS)
Esta sección describe la estructura técnica que el Admin debe esperar de la Spoke EPM.

### B.1 Grupos y Rangos
| Grupo | Rango | Descripción General |
| :--- | :--- | :--- |
| **Identidad y Tiempos** | 1 - 19 | Quién, Cuándo y Dónde. Datos de contrato y periodos. |
| **Financiero Detallado** | 20 - 38 | Liquidación en pesos ($) desglosada por servicio vertical. |
| **Auditoría Técnica** | 39 - 63 | Datos físicos, componentes unitarios ($) y consumos. |
| **Observaciones** | 64 - 65 | Banderas de alerta y sustento legal (JSON). |

### B.2 Catálogo Detallado (Conocimiento Estructural)
*Aquí se define qué es cada columna para auditoría manual o visual.*
| # | Columna | Descripción Funcional |
|:---:|:---|:---|
| 1 | **ID_Unico** | Llave primaria: `'[PERIODO]_[CONTRATO]_[SERVICIO]`. |
| 2 | **Periodo** | Texto: `'MES-AAAA` (Ej: `'OCT-2024`). |
| 3 | **Año** | Numérico: YYYY. |
| 4 | **Sem** | Semestre del año (S1, S2). |
| 5 | **Tri** | Trimestre del año (T1..T4). |
| 6 | **Bim** | Bimestre del año (B1..B6). |
| 7 | **Mes** | Nombre corto del mes (ENE, FEB...). |
| 8 | **Num** | Número de mes (1..12). |
| 9 | **Fecha_Fact** | Fecha de emisión (DD/MM/YYYY). |
| 10 | **Fecha_Venc** | Fecha límite de pago (DD/MM/YYYY). |
| 11 | **Contrato** | ID de cuenta: `'[NÚMERO]`. |
| 12 | **Ref_Pago** | Referente para pago electrónico: `'[NÚMERO]`. |
| 13 | **ID_Producto** | ID específico del servicio dentro de EPM. |
| 14 | **Ciclo** | Ciclo de lectura de la zona. |
| 15 | **Est** | Estrato socioeconómico (1..6). |
| 16 | **Tipo_Servicio** | Vertical: ENERGIA, GAS, ACUE, ALCA, ASEO, ALUM, _TOTAL. |
| 17 | **Desde** | Inicio periodo lectura (DD/MM/YYYY). |
| 18 | **Hasta** | Fin periodo lectura (DD/MM/YYYY). |
| 19 | **Dias** | Días totales facturados. |
| 20 | **E_Fin_Var** | Energía: Valor consumo ($). |
| 21 | **E_Fin_Cont** | Energía: Valor contribución/subsidio ($). |
| 22 | **G_Fin_Var** | Gas: Valor consumo ($). |
| 23 | **G_Fin_Fijo** | Gas: Valor cargo fijo ($). |
| 24 | **G_Fin_Cont** | Gas: Valor contribución/subsidio ($). |
| 25 | **Ac_Fin_Var** | Acueducto: Valor consumo ($). |
| 26 | **Ac_Fin_Fijo** | Acueducto: Valor cargo fijo ($). |
| 27 | **Ac_Fin_Cont** | Acueducto: Valor contribución/subsidio ($). |
| 28 | **Al_Fin_Var** | Alcantarillado: Valor consumo ($). |
| 29 | **Al_Fin_Fijo** | Alcantarillado: Valor cargo fijo ($). |
| 30 | **Al_Fin_Cont** | Alcantarillado: Valor contribución/subsidio ($). |
| 31 | **As_Fin_Fijo** | Aseo: Cargo fijo mensual ($). |
| 32 | **As_Fin_Var** | Aseo: Cargo variable ($). |
| 33 | **As_Fin_Cont** | Aseo: Valor contribución ($). |
| 34 | **Alum_Fin** | Alumbrado: Valor total impuesto ($). |
| 35 | **Otros** | Financiaciones, seguros o cobros externos ($). |
| 36 | **Ajuste** | Ajuste al peso (Solo fila _TOTAL). |
| 37 | **Saldo** | Saldo anterior / Deuda pendiente. |
| 38 | **Total_Fila** | Suma financiera neta de la fila. |
| 39 | **Consumo_Cant** | Cantidad consumida (kWh, m3, Ton). |
| 40 | **Unidad_Medida** | Etiqueta de la unidad. |
| 41 | **Medidor** | Serial del equipo: `'[SERIAL]`. |
| 42 | **Lect_Ant** | Lectura anterior del equipo. |
| 43 | **Lect_Act** | Lectura actual del equipo. |
| 44 | **Const** | Factor o constante multiplicadora. |
| 45 | **E_CU_G** | Energía: $/kWh Generación. |
| 46 | **E_CU_T** | Energía: $/kWh Transmisión. |
| 47 | **E_CU_D** | Energía: $/kWh Distribución. |
| 48 | **E_CU_C** | Energía: $/kWh Comercialización. |
| 49 | **E_CU_P** | Energía: $/kWh Pérdidas. |
| 50 | **E_CU_R** | Energía: $/kWh Restricciones. |
| 51 | **G_CU_Compr** | Gas: $/m3 Compra. |
| 52 | **G_CU_Dist** | Gas: $/m3 Distribución. |
| 53 | **G_CU_Transp** | Gas: $/m3 Transporte. |
| 54 | **G_CU_Conf** | Gas: $/m3 Confiabilidad. |
| 55 | **G_CU_Com_F** | Gas: $ Comercialización Fija. |
| 56 | **A_CU_Cmap** | Agua: $ Costo Admin. |
| 57 | **A_CU_Cmpac** | Agua: $ Costo Operación. |
| 58 | **A_CU_Cmt** | Agua: $ Tasas ambientales. |
| 59 | **Ton_NoAp** | Aseo: Toneladas ordinarias. |
| 60 | **Ton_Barr** | Aseo: Toneladas barrido. |
| 61 | **Ton_Limp** | Aseo: Toneladas limpieza urbana. |
| 62 | **Ton_Rech** | Aseo: Toneladas rechazados. |
| 63 | **Ton_Disp** | Aseo: Toneladas disposición final. |
| 64 | **Alertas** | Etiquetas de inteligencia (NORMAL, CAMBIO_MEDIDOR...). |
| 65 | **Info_Reg_Json** | JSON con decretos y letra pequeña informativa. |
