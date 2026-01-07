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
- Documento No (Busca después de `Documento No:` y Extrae la secuencia numérica completa agrega Apostrofe obligatorio al inicio ('))
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
- Transporte 7
- Confiabilidad
- Comercializac
- Transporte Gn
- Compresión 8
- Comercializac

---

## Instrucciones adicionales
- Toma solo los valores numéricos al sacar los valores de cada dato.
- Los datos numéricos solo utilizan la (,) como separador decimal y quita el separador de miles.
- Si encuentras un valor adicional a los anteriores me lo haces saber. Indicando con qué Bloque tiene relación y la historia del dato encontrado.
- Los valores numéricos que no encuentres los reemplazas con (0,00).
- Evalúa el contenido de cada Bloque y los datos extraídos y si encuentras algún dato adicional que le pueda aportar a la extracción en alguno de los bloques y me haces una recomendación.
- Verifica que los totales de Bloque 1, Bloque 2, Bloque 3 coincidan con los totales que se encuentran en el Bloque General, si no coinciden me lo haces saber indicando la diferencia encontrada.
- Si necesitas alguna aclaración adicional me lo haces saber antes de iniciar la extracción.

Dame una tabla con estos datos identificados y dame un análisis de las Instrucciones para ubicar el Bloque y Dato fueron las correctas.
