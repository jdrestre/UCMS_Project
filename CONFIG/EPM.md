# 📑 FICHA TÉCNICA DE EXTRACCIÓN: EPM MULTISERVICIOS
**Rol:** Analista de Automatización de Procesos (RPA) / Especialista en Extracción de Datos (Data Extraction Specialist) | **Objetivo:** Automatizar la extracción y normalización de datos de servicios públicos para el seguimiento histórico y la auditoría financiera.

---

De la factura adjunta quiero extraer información por cada bloque que vaya definiendo por servicio

## 0. Bloque General
Se puede identificar por el letrero del logo de la empresa en la parte superior y la información del bloque se cubre verticalmente. Arriba empieza con el valor total de la factura seguido de `Pagar hasta ...` y abajo finaliza con `Fecha de validación` de esta zona se sacará información General de la factura y datos para verificar Totales de la factura.
- Documento Electrónico Equivalente SPD N° (Apostrofe obligatorio al inicio ('))
- Valor total a pagar
- Pagar hasta el (utilizar este formato siempre dd/mm/yyyy)
- Contrato (Apostrofe obligatorio al inicio ('))
- Referente de pago: (Apostrofe obligatorio al inicio ('))
- Documento No --> Extrae el valor numérico completo que aparece inmediatamente después de la etiqueta 'Documento No:'. Debes incluir TODOS los dígitos y espacios que aparezcan en esa misma línea (por ejemplo: '144 1676405'). No omitas los primeros dígitos ni resumas el número y agrega Apostrofe obligatorio al inicio (')
- Cliente
- CC/NIT
- Dirección de cobro
- Ciudad - Departamento 
- Estrato
- Ciclo
- Acueducto: Consumo y Valor a pagar
- Alcantarillado: Consumo y Valor a pagar
- Energía: Consumo y Valor a pagar
- Gas: Consumo y Valor a pagar
- Otras entidades:  Valor a pagar
- Ajuste al peso:  Valor a pagar
- Fecha de generación: (utilizar este formato siempre dd/mm/yyyy)

---

## 1. Bloque Acueducto
Se puede identificar por el letrero vertical con la palabra "Acueducto" y la información del bloque se cubre a la derecha de ese letrero, puede excluir la zona gráfica para quitar ruido de la extracción. Arriba empieza con `Cálculo Consumo` y abajo finaliza con `Total Acueducto` de esta zona se sacará toda la información del Bloque Acueducto.
Una vez tengas identificada esta zona necesito realizar la extracción de toda la información de este Bloque Acueducto para realizar seguimiento histórico para cualquier factura.
- Fecha Inicio de Cálculo de Consumo (utilizar este formato siempre dd/mm/yyyy)
- Fecha Final de Cálculo de Consumo (utilizar este formato siempre dd/mm/yyyy)
- Días de Cálculo de Consumo
- Lectura Actual
- Lectura Anterior
- Consumo m3
- Costo ($)
- Consumo mmm-yy
- Cargo fijo mmm-yy
- Contrib Cargo Fijo
- Contrib Consumo
- Total Acueducto
- Producto (Apostrofe obligatorio al inicio ('))
- Categoría
- Medidor (Apostrofe obligatorio al inicio ('))
- Plan
- Cmapac - Cost 
- Cmpac Unitari
- Cmpac Total
- Cmt Unitario
- Cmt Total

---

## 2. Bloque Alcantarillado
Se puede identificar por el letrero vertical con la palabra "Alcantarillado" y la información del bloque se cubre a la derecha de ese letrero, puede excluir la zona gráfica para quitar ruido de la extracción. Arriba empieza con `Cálculo Consumo` y abajo finaliza con `Total Alcantarillado` de esta zona se sacará toda la información del Bloque Alcantarillado.
Una vez tengas identificada esta zona necesito realizar la extracción de toda la información de este Bloque Alcantarillado para realizar seguimiento histórico para cualquier factura.
- Fecha Inicio de Cálculo de Consumo (utilizar este formato siempre dd/mm/yyyy)
- Fecha Final de Cálculo de Consumo (utilizar este formato siempre dd/mm/yyyy)
- Días de Cálculo de Consumo
- Lectura Actual (igual dato que tiene Bloque Acueducto)
- Lectura Anterior (igual dato que tiene Bloque Acueducto)
- Consumo m3
- Costo ($)
- Consumo mmm-yy
- Cargo fijo mmm-yy
- Contrib Cargo Fijo
- Contrib Consumo
- Total Alcantarillado
- Producto (Apostrofe obligatorio al inicio ('))
- Categoría
- Plan
- Cmt Unitario
- Cmt Total

---

## 3. Bloque Energía
Se puede identificar por el letrero vertical con la palabra "Energía" y la información del bloque se cubre a la derecha de ese letrero, puede excluir la zona gráfica para quitar ruido de la extracción. Arriba empieza con `Cálculo Consumo` y abajo finaliza con `Total Energía` de esta zona se sacará toda la información del Bloque Energía.
Una vez tengas identificada esta zona necesito realizar la extracción de toda la información de este Bloque Energía para realizar seguimiento histórico para cualquier factura.
- Fecha Inicio de Cálculo de Consumo (utilizar este formato siempre dd/mm/yyyy)
- Fecha Final de Cálculo de Consumo (utilizar este formato siempre dd/mm/yyyy)
- Días de Cálculo de Consumo
- Lectura Actual
- Lectura Anterior
- Constante
- Consumo kWh
- Costo ($)
- Energía mmm-yy
- Contribución activa
- Total Energía
- Producto (Apostrofe obligatorio al inicio ('))
- Categoría
- Medidor (Apostrofe obligatorio al inicio ('))
- Plan
- Generación
- Transmisión
- Distribución
- Comercializac
- Perdidas
- Restricciones
- N. tensión

---

## 4. Bloque Gas
Se puede identificar por el letrero vertical con la palabra "Gas" y la información del bloque se cubre a la derecha de ese letrero, puede excluir la zona gráfica para quitar ruido de la extracción. Arriba empieza con `Cálculo Consumo` y abajo finaliza con `Total Gas` de esta zona se sacará toda la información del Bloque Gas.
Una vez tengas identificada esta zona necesito realizar la extracción de toda la información de este Bloque Gas para realizar seguimiento histórico para cualquier factura.
- Fecha Inicio de Cálculo de Consumo (utilizar este formato siempre dd/mm/yyyy)
- Fecha Final de Cálculo de Consumo (utilizar este formato siempre dd/mm/yyyy)
- Días de Cálculo de Consumo
- Lectura Actual
- Lectura Anterior
- Constante
- Consumo m3
- Consumo mmm-yy
- Cargo fijo mmm-yy
- Contrib consumo
- Contrib cargo fijo
- Total Gas
- Producto (Apostrofe obligatorio al inicio ('))
- Categoría
- Medidor (Apostrofe obligatorio al inicio ('))
- Plan
- Compra
- Distribución
- Transporte 7 --> extrae el valor numérico que aparece después de `Transporte 7` 
- Confiabilidad
- Comercializac
- Transporte Gn --> extrae el valor numérico que aparece después de `Transporte Gn`
- Compresión 8 --> extrae el valor numérico que aparece después de `Compresión 8`
- Comercializac

---

## 5. Bloque Otras Entidades
Se puede identificar por el letrero vertical con la palabra "Otras Entidades" y la información del bloque se cubre a la derecha de ese letrero. Arriba empieza con `Emvarias` y abajo finaliza con `Total Otras Entidades` de esta zona se sacará toda la información del Bloque Otras Entidades. Este Bloque tiene la particularidad que puede tener varios sub bloques internos, cada sub bloque empieza con el nombre de la entidad (Emvarias para Aseo y Alumbrado Público Medellín para Alumbrado Público) y termina con los totales de cada sub bloque (Total Aseo y Total Alumbrado Público) y al final del Bloque está el Total Otras Entidades que es la suma de los totales de cada sub bloque. Una vez tengas identificada esta zona necesito realizar la extracción de toda la información de este Bloque Otras Entidades para realizar seguimiento histórico para cualquier factura.
- Total Otras Entidades

A continuación te detallo los sub bloques que puede tener este Bloque Otras Entidades:

### 5.1 Aseo
Se puede identificar por el letrero con la palabra "Emvarias" y la información del sub bloque se cubre a la derecha de ese letrero. Arriba empieza con `Emvarias` y abajo finaliza con `Total Aseo` de esta zona se sacará toda la información del Sub Bloque Aseo. Una vez tengas identificada esta zona necesito realizar la extracción de toda la información del Sub Bloque Aseo para realizar seguimiento histórico para cualquier factura.
- Periodo de consumo ('mmm-yy) Incluir apostrofe al inicio (') 
- Cargo fijo
- Cargo Variable Aprovechable
- Contribución
- Cargo Variable
- No Aprov - Ordinarios
- Barrido y limpieza
- Limpieza urbana
- Rechazados
- Total Aseo

### 5.1 Alumbrado Público
Se puede identificar por el letrero con la palabra "Alumbrado Público Medellín" y la información del sub bloque se cubre a la derecha de ese letrero. Arriba empieza con `Alumbrado Público Medellín` y abajo finaliza con `Total Alumbrado Público` de esta zona se sacará toda la información del Sub Bloque Alumbrado Público. Una vez tengas identificada esta zona necesito realizar la extracción de toda la información del Sub Bloque Alumbrado Público para realizar seguimiento histórico para cualquier factura.
- Alumbrado Público
- Total Alumbrado Público
- Total Otras Entidades (SUMATORIA DE LOS TOTALES DE CADA SUB BLOQUE ANOTADOS ARRIBA ASEO Y ALUMBRADO PÚBLICO)

---

## Instrucciones adicionales
- Fidelidad Estricta: Extrae datos exclusivamente del archivo adjunto. Está prohibido alucinar, inferir o usar datos de facturas de ejemplo.
- Toma solo los valores numéricos al sacar los valores de cada dato.
- Los datos numéricos solo utilizan la (,) como separador decimal y quita el separador de miles.
- Si encuentras un valor adicional a los anteriores me lo haces saber. Indicando con qué Bloque tiene relación y la historia del dato encontrado.
- Los valores numéricos que no encuentres los reemplazas con (0,00).
- Evalúa el contenido de cada Bloque y los datos extraídos y si encuentras algún dato adicional que le pueda aportar a la extracción en alguno de los bloques y me haces una recomendación.
- Verifica que los totales de Bloque 1, Bloque 2, Bloque 3, Bloque 4, Bloque 5 coincidan con los totales que se encuentran en el Bloque General, si no coinciden me lo haces saber indicando la diferencia encontrada.
- Si necesitas alguna aclaración adicional me lo haces saber antes de iniciar la extracción.
- Verifica que la sumatoria de los sub bloques del Bloque 5 coincidan con el total del Bloque 5 y a la vez comparar con el valor que se encuentra en el Bloque General, si no coinciden me lo haces saber indicando la diferencia encontrada.

Dame una tabla con estos datos identificados y Al final de la tabla, incluye una breve sección de "Auditoría de Extracción" confirmando si las coordenadas/letreros verticales descritos en el prompt coincidieron con la estructura del PDF adjunto.

# TABLAS DE DATOS EXTRAÍDOS

La tabla debe tener 8 filas que corresponden a los servicios: Acueducto, Alcantarillado, Energía, Gas, Otras Entidades y Total General.
La primera columna debe listar los nombres de los servicios con un ID definido como `ID_Servicio` y debe ser definido de la siguiente manera: 
- PERIODO = mmm-yyyy
- SERVICIO = Nombre del servicio (ACUE, ALCA, ENER, GAS, ASEO, ALUM, OTRAS, TOTAL)
- CONTRATO = Número de contrato extraído del Bloque General

FORMATO DEL `ID_Servicio`: 'PERIODO_SERVICIO_CONTRATO' (Ejemplo: 'ENE-2025_ACUE_12345678')

## COLUMNAS DE LA TABLA BASE
LA TABLA DE DATOS EXTRAÍDOS debe contener las siguientes columnas:
- ID_Servicio (como se definió anteriormente)
- PERÍODO ('mmm-yyyy) Debe tener un apostrofe al inicio (') Ejemplo: 'ENE-2025
- SERVICIO (Nombre del servicio: Acueducto, Alcantarillado, Energía, Gas, Otras Entidades, Total General)
- FECHA_GENERACIÓN (dd/mm/yyyy) Se extrae del Bloque General `Fecha de generación`
- FECHA_LIMITE_PAGO (dd/mm/yyyy) Se extrae del Bloque General `Pagar hasta el`
- CONSUMO (Valor numérico sin separador de miles y con coma como separador decimal) Se toma de cada Bloque correspondiente por servicio. Para Aseo, Alumbrado Público, Otras Entidades y Total General se coloca (0,00)
- CONSTANTE Para los Bloques que tienen este dato (Gas y Energía), para Gas y Energía se extrae utilizando la coma como separador decimal, para los demás servicios se coloca (0,00).
- COSTO ($) Se extrae de cada Bloque correspondiente por servicio (Valor numérico sin separador de miles y con coma como separador decimal). Para Aseo, Alumbrado Público, Otras Entidades y Total General se coloca (0,00).
- VALOR_A_PAGAR (Valor numérico sin separador de miles y con coma como separador decimal) Se toma de cada Bloque correspondiente por servicio con el texto `Total [Servicio]`  y del Bloque General para la fila de Otras Entidades y Total General
- PORCENTAJE_DEL_TOTAL (Valor numérico con dos decimales y coma como separador decimal) Se calcula dividiendo el VALOR_A_PAGAR de cada servicio entre el VALOR_A_PAGAR del Total General. Para el Total General se coloca (1)
- OTROS_CARGOS (Valor numérico sin separador de miles y con coma como separador decimal) Se extrae del Bloque General en caso que se encuentre un valor adicional que no corresponda a los servicios definidos (Acueducto, Alcantarillado, Energía, Gas, Otras Entidades, Ajuste al peso). En caso de no encontrar ningún valor adicional se coloca (0,00). Si el valor tiene relación con algún servicio se coloca en la fila correspondiente al servicio.


### FORMATO DE SALIDA TABLA BASE
Debe ser markdown con las columnas definidas en la sección `Columnas de la tabla` separadas por tuberías `|` como se muestra a continuación:
| ID_Servicio | PERÍODO | SERVICIO | FECHA_GENERACIÓN | FECHA_LIMITE_PAGO | CONSUMO | CONSTANTE | COSTO ($) | VALOR_A_PAGAR | PORCENTAJE_DEL_TOTAL | OTROS_CARGOS |
|---|---|---|---|---|---|---|---|---|---|---|
| 'MMM-YYYY_ACUE_XXXXXXXX' | 'mmm-yyyy | Acueducto | dd/mm/yyyy | dd/mm/yyyy | valor | valor | valor | valor | valor | valor |
| ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... |

---

## COLUMNAS TABLA ACUEDUCTO Y ALCANTARILLADO DETALLE
Necesito una tabla detallada solo para los bloques de: 
Bloque Acueducto y Bloque de Alcantarillado con las siguientes columnas:
- ID_Servicio (como se definió anteriormente) DEBE SER EL MISMO QUE EN LA TABLA BASE Y UNA FILA POR CADA SERVICIO (ACUE Y ALCA)
- SERVICIO (Nombre del servicio: Acueducto, Alcantarillado)
- PERIÓDO ('mmm-yyyy) Debe tener un apostrofe al inicio (') Ejemplo: 'ENE-2025
- PERIODO_CONSUMO_INICIO (dd/mm/yyyy) Se extrae del Bloque correspondiente al servicio `Cálculo Consumo` y es el mismo valor para Acueducto y Alcantarillado
- PERIODO_CONSUMO_FINAL (dd/mm/yyyy) Se extrae del Bloque correspondiente al servicio `Cálculo Consumo` y es el mismo valor para Acueducto y Alcantarillado
- DÍAS_CÁLCULO_CONSUMO (Número entero) Se extrae del Bloque correspondiente al servicio `Cálculo Consumo` y es el mismo valor para Acueducto y Alcantarillado
- LECTURA_ACTUAL Se extrae del Bloque correspondiente al servicio `Lectura Actual` y es el mismo valor para Acueducto y Alcantarillado
- LECTURA_ANTERIOR Se extrae del Bloque correspondiente al servicio `Lectura Anterior`
- CONSUMO_M3 Se extrae del Bloque correspondiente al servicio `Consumo m3` y es el mismo valor para Acueducto y Alcantarillado
- COSTO ($) Se extrae del Bloque correspondiente al servicio `Costo ($)`
- CONSUMO_MMM-YY Se extrae del Bloque correspondiente al servicio `Consumo mmm-yy` y es el valor numérico sin separador de miles y con coma como separador decimal que resulta de multiplicar el Consumo m3 por el Costo ($) en esa línea.
- CARGO_FIJO_MMM-YY Se extrae del Bloque correspondiente al servicio `Cargo fijo mmm-yy`
- CONTRIB_CARGO_FIJO Se extrae del Bloque correspondiente al servicio `Contribución Cargo Fijo`
- CONTRIB_CONSUMO Se extrae del Bloque correspondiente al servicio `Contribución Consumo`
- TOTAL_SERVICIO Se extrae del Bloque correspondiente al servicio `Total Servicio` (Acueducto o Alcantarillado)
- PRODUCTO (Apostrofe obligatorio al inicio (')) 
- CATEGORÍA
- MEDIDOR (Apostrofe obligatorio al inicio ('))
- PLAN
- CMAPAC_COST Nombre exacto del dato a extraer `Cmapac - Cost `
- CMAPAC_UNITARI Nombre exacto del dato a extraer `Cmpac Unitari`
- CMAPAC_TOTAL Nombre exacto del dato a extraer `Cmpac Total`
- CMT_UNITARIO Nombre exacto del dato a extraer `Cmt Unitario`
- CMT_TOTAL Nombre exacto del dato a extraer `Cmt Total`

Para los valores de Alcantarillado que no encuentres en la factura los reemplazas con (0,00) o 0 según corresponda.

---

### FORMATO DE SALIDA TABLA DETALLE ACUEDUCTO Y ALCANTARILLADO
Debe ser markdown con las columnas definidas en la sección `Columnas tabla Acueducto y Alcantarillado detalle` separadas por tuberías `|` como se muestra a continuación:
| ID_Servicio | SERVICIO | PERIÓDO | PERIODO_CONSUMO_INICIO | PERIODO_CONSUMO_FINAL | DÍAS_CÁLCULO_CONSUMO | LECTURA_ACTUAL | LECTURA_ANTERIOR | CONSUMO_M3 | COSTO ($) | CONSUMO_MMM-YY | CARGO_FIJO_MMM-YY | CONTRIB_CARGO_FIJO | CONTRIB_CONSUMO | TOTAL_SERVICIO | PRODUCTO | CATEGORÍA | MEDIDOR | PLAN | CMAPAC_COST | CMAPAC_UNITARI | CMAPAC_TOTAL | CMT_UNITARIO | CMT_TOTAL |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---||---|---|---|---|---|
| 'MMM-YYYY_ACUE_XXXXXXXX' | Acueducto | 'mmm-yyyy | dd/mm/yyyy | dd/mm/yyyy | valor | valor | valor | valor | valor | valor | valor | valor | valor | valor | 'producto' | valor | 'medidor' | valor | valor | valor | valor | valor |
| 'MMM-YYYY_ALCA_XXXXXXXX' | Alcantarillado | 'mmm-yyyy | dd/mm/yyyy | dd/mm/yyyy | valor | valor | valor | valor | valor | valor | valor | valor | valor | valor | 'producto' | valor | 'medidor' | | valor | valor | valor | valor | valor |

---

## COLUMNAS TABLA ENERGÍA DETALLE
Necesito una tabla detallada solo para el Bloque de Energía con las siguientes columnas:
- ID_Servicio (como se definió anteriormente) DEBE SER EL MISMO QUE EN LA TABLA BASE Y UNA FILA POR EL SERVICIO ENERGÍA (ENER)
- SERVICIO (Nombre del servicio: Energía)
- PERIÓDO ('mmm-yyyy) Debe tener un apostrofe al inicio (') Ejemplo: 'ENE-2025
- PERIODO_CONSUMO_INICIO (dd/mm/yyyy) Se extrae del Bloque correspondiente al servicio `Cálculo Consumo`
- PERIODO_CONSUMO_FINAL (dd/mm/yyyy) Se extrae del Bloque correspondiente al servicio `Cálculo Consumo`
- DÍAS_CÁLCULO_CONSUMO (Número entero) Se extrae del Bloque correspondiente al servicio `Cálculo Consumo`
- LECTURA_ACTUAL Se extrae del Bloque correspondiente al servicio `Lectura Actual`
- LECTURA_ANTERIOR Se extrae del Bloque correspondiente al servicio `Lectura Anterior`
- CONSTANTE Se extrae del Bloque correspondiente al servicio `Constante`
- CONSUMO_KWH Se extrae del Bloque correspondiente al servicio `Consumo kWh`
- COSTO ($) Se extrae del Bloque correspondiente al servicio `Costo ($)`
- ENERGÍA_MMM-YY Se extrae del Bloque correspondiente al servicio `Energía mmm-yy` y es el valor numérico sin separador de miles y con coma como separador decimal que resulta de multiplicar el Consumo kWh por el Costo ($) en esa línea.
- CONTRIBUCIÓN_ACTIVA Se extrae del Bloque correspondiente al servicio `Contribución activa`
- TOTAL_ENERGÍA Se extrae del Bloque correspondiente al servicio `Total Energía`
- PRODUCTO (Apostrofe obligatorio al inicio (')) 
- CATEGORÍA
- MEDIDOR (Apostrofe obligatorio al inicio ('))
- PLAN
- GENERACIÓN Extrae el valor numérico que aparece después de `Generación` utilizando la coma como separador decimal
- TRANSMISIÓN Extrae el valor numérico que aparece después de `Transmisión` utilizando la coma como separador decimal
- DISTRIBUCIÓN Extrae el valor numérico que aparece después de `Distribución` utilizando la coma como separador decimal
- COMERCIALIZACIÓN Extrae el valor numérico que aparece después de `Comercializac` utilizando la coma como separador decimal
- PERDIDAS Extrae el valor numérico que aparece después de `Perdidas` utilizando la coma como separador decimal
- RESTRICCIONES Extrae el valor numérico que aparece después de `Restricciones` utilizando la coma como separador decimal
- N_TENSIÓN_Voltios Extrae el valor numérico que aparece después de `N. tensión` como número entero

---

### FORMATO DE SALIDA TABLA DETALLE ENERGÍA
Debe ser markdown con las columnas definidas en la sección `Columnas tabla Energía detalle` separadas por tuberías `|` como se muestra a continuación:
| ID_Servicio | SERVICIO | PERIÓDO | PERIODO_CONSUMO_INICIO | PERIODO_CONSUMO_FINAL | DÍAS_CÁLCULO_CONSUMO | LECTURA_ACTUAL | LECTURA_ANTERIOR | CONSTANTE | CONSUMO_KWH | COSTO ($) | ENERGÍA_MMM-YY | CONTRIBUCIÓN_ACTIVA | TOTAL_ENERGÍA | PRODUCTO | CATEGORÍA | MEDIDOR | PLAN | GENERACIÓN | TRANSMISIÓN | DISTRIBUCIÓN | COMERCIALIZACIÓN | PERDIDAS | RESTRICCIONES | N_TENSIÓN_Voltios |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 'MMM-YYYY_ENER_XXXXXXXX' | Energía | 'mmm-yyyy | dd/mm/yyyy | dd/mm/yyyy | valor | valor | valor | valor | valor | valor | valor | valor | valor | 'producto' | valor | 'medidor' | | valor | valor | valor | valor | valor | valor | valor | valor |

---

## COLUMNAS TABLA GAS DETALLE
Necesito una tabla detallada solo para el Bloque de Gas con las siguientes columnas:
- ID_Servicio (como se definió anteriormente) DEBE SER EL MISMO QUE EN LA TABLA BASE Y UNA FILA POR EL SERVICIO GAS (GAS)
- SERVICIO (Nombre del servicio: Gas)
- PERIÓDO ('mmm-yyyy) Debe tener un apostrofe al inicio (') Ejemplo: 'ENE-2025
- PERIODO_CONSUMO_INICIO (dd/mm/yyyy) Se extrae del Bloque correspondiente al servicio `Cálculo Consumo`
- PERIODO_CONSUMO_FINAL (dd/mm/yyyy) Se extrae del Bloque correspondiente al servicio `Cálculo Consumo`
- DÍAS_CÁLCULO_CONSUMO (Número entero) Se extrae del Bloque correspondiente al servicio `Cálculo Consumo`
- LECTURA_ACTUAL Se extrae del Bloque correspondiente al servicio `Lectura Actual`
- LECTURA_ANTERIOR Se extrae del Bloque correspondiente al servicio `Lectura Anterior`
- CONSTANTE Se extrae del Bloque correspondiente al servicio `Constante`
- CONSUMO_M3 Se extrae del Bloque correspondiente al servicio `Consumo m3`
- COSTO ($) Se extrae del Bloque correspondiente al servicio `Costo ($)`
- CONSUMO_MMM-YY Se extrae del Bloque correspondiente al servicio `Consumo mmm-yy` y es el valor numérico sin separador de miles y con coma como separador decimal que resulta de multiplicar el Consumo m3 por el Costo ($) en esa línea.
- CARGO_FIJO_MMM-YY Se extrae del Bloque correspondiente al servicio `Cargo fijo mmm-yy`
- CONTRIB_CONSUMO Se extrae del Bloque correspondiente al servicio `Contrib Consumo`
- CONTRIB_CARGO_FIJO Se extrae del Bloque correspondiente al servicio `Contrib Cargo Fijo`
- TOTAL_GAS Se extrae del Bloque correspondiente al servicio `Total Gas`
- PRODUCTO (Apostrofe obligatorio al inicio (')) 
- CATEGORÍA
- MEDIDOR (Apostrofe obligatorio al inicio ('))
- PLAN
- COMPRA Extrae el valor numérico que aparece después de `Compra` utilizando la coma como separador decimal
- DISTRIBUCIÓN Extrae el valor numérico que aparece después de `Distribución` utilizando la coma como separador decimal
- TRANSPORTE Extrae el valor numérico que aparece después de `Transporte` o `Transporte 7`, el que aparezca, utilizando la coma como separador decimal
- CONFIABILIDAD Extrae el valor numérico que aparece después de `Confiabilidad` utilizando la coma como separador decimal
- COMERCIALIZACIÓN Extrae el valor numérico que aparece después de `Comercializac` utilizando la coma como separador decimal
- TRANSPORTE_GN Extrae el valor numérico que aparece después de `Transporte Gn` utilizando la coma como separador decimal
- COMPRESIÓN_FIJA Extrae el valor numérico que aparece después de `Compresión` o `Compresión 8`, el que aparezca, utilizando la coma como separador decimal
- COMERCIALIZACIÓN_FIJA Extrae el valor numérico que aparece después de la segunda aparición de `Comercializac` utilizando la coma como separador decimal, debe coincidir con el valor que aparece en la columna CARGO_FIJO_MMM-YY (En algunas facturas no aparece este valor, en ese caso colocar (0,00))

---

### FORMATO DE SALIDA TABLA DETALLE GAS
Debe ser markdown con las columnas definidas en la sección `Columnas tabla Gas detalle` separadas por tuberías `|` como se muestra a continuación:
| ID_Servicio | SERVICIO | PERIÓDO | PERIODO_CONSUMO_INICIO | PERIODO_CONSUMO_FINAL | DÍAS_CÁLCULO_CONSUMO | LECTURA_ACTUAL | LECTURA_ANTERIOR | CONSTANTE | CONSUMO_M3 | COSTO ($) | CONSUMO_MMM-YY | CARGO_FIJO_MMM-YY | CONTRIB_CONSUMO | CONTRIB_CARGO_FIJO | TOTAL_GAS | PRODUCTO | CATEGORÍA | MEDIDOR | PLAN | COMPRA | DISTRIBUCIÓN | TRANSPORTE | CONFIABILIDAD | COMERCIALIZACIÓN | TRANSPORTE_GN | COMPRESIÓN_FIJA | COMERCIALIZACIÓN_FIJA |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 'MMM-YYYY_GAS_XXXXXXXX' | Gas | 'mmm-yyyy | dd/mm/yyyy | dd/mm/yyyy | valor | valor | | valor | valor | valor | valor | valor | valor | valor | valor | valor | 'producto' | valor | 'medidor' | | valor | valor | valor | valor | valor | valor | valor |

---

## COLUMNAS TABLA OTRAS ENTIDADES DETALLE
Necesito una tabla detallada solo para el Bloque de Otras Entidades con las siguientes columnas:
- ID_Servicio (como se definió anteriormente) DEBE SER EL MISMO QUE EN LA TABLA BASE Y UNA FILA POR CADA SUB BLOQUE (ASEO Y ALUM) Y UNA FILA ADICIONAL PARA EL TOTAL GENERAL (OTRAS ENTIDADES)
- SERVICIO (Nombre del servicio: Aseo, Alumbrado Público)
- PERIÓDO ('mmm-yyyy) Debe tener un apostrofe al inicio (') Ejemplo: 'ENE-2025
- CARGO_FIJO Se extrae del Sub Bloque correspondiente al servicio `Cargo fijo` (Solo para Aseo)
- CARGO_VARIABLE_APROVECHABLE Se extrae del Sub Bloque correspondiente al servicio `Cargo Variable Aprovecha` (Solo para Aseo)
- CONTRIBUCIÓN Se extra e del Sub Bloque correspondiente al servicio `Contribución` (Solo para Aseo)
- CARGO_VARIABLE Se extrae del Sub Bloque correspondiente al servicio `Cargo Variable` (Solo para Aseo)
- NO_APROV_ORDINARIOS Se extrae del Sub Bloque correspondiente al servicio `No Aprov - Ordinarios` (Solo para Aseo)
- BARRIDO_Y_LIMPIEZA Se extrae del Sub Bloque correspondiente al servicio `Barrido y limpieza` (Solo para Aseo)
- LIMPIEZA_URBANA Se extrae del Sub Bloque correspondiente al servicio `Limpieza urbana` (Solo para Aseo)
- RECHAZADOS Se extrae del Sub Bloque correspondiente al servicio `Rechazados` (Solo para Aseo)
- ALUMBRADO_PÚBLICO Se extrae del Sub Bloque correspondiente al servicio `Alumbrado Público` (Solo para Alumbrado Público)
- TOTAL_SERVICIO Se extrae del Sub Bloque correspondiente al servicio `Total [Servicio]` (Aseo, Alumbrado Público Y Otras Entidades(SUMATORIA DE LOS TOTALES DE LOS SUB BLOQUES ASEO Y ALUMBRADO PÚBLICO))

* Para los valores que no encuentres en la factura los reemplazas con (0,00).

---
