# 📑 FICHA TÉCNICA DE EXTRACCIÓN: EPM (v2.6.2)
**Alineación Sistema:** NÚCLEO_MAESTRO v3.0.0 (Global UCMS)
**Estructura:** Matriz Plana de 76 Columnas | **Foco:** Granularidad Absoluta.

---

## 1. PROTOCOLO DE INVARIANZA ESTRUCTURAL (OJF)
Para asegurar la integridad de la serie histórica en `DATA/EPM.csv`, es MANDATORIO generar exactamente **8 filas** por factura en este orden físico estricto:

1. **ACUE** (Acueducto)
2. **ALCA** (Alcantarillado)
3. **ENER** (Energía)
4. **GAS** (Gas Natural)
5. **ASEO** (Servicio de Aseo - Emvarias)
6. **ALUM** (Alumbrado Público)
7. **OTRAS** (Fila Pivote: Ajustes genéricos o Terceros)
8. **TOTAL** (Cierre y Cuadre de Caja)

*Regla:* Si un servicio no existe o tiene valor cero, la fila se genera con relleno técnico `0,00` en todos sus campos de valor.

---

## 2. LÓGICA DE AISLAMIENTO PARENTAL (RETROACTIVOS)
Basado en el aprendizaje de la factura de Febrero 2025:
* **Vinculación:** Si el PDF indica un retroactivo o ajuste de un servicio específico, el valor financiero DEBE quedarse en la fila de ese servicio.
* **Mapeo:** El monto se coloca en la **Columna 40 (Ajuste)**.
* **Protección de KPI:** No sumar el retroactivo a la columna de Consumo Variable (`Ac_Fin_Var`, etc.).
* **Documentación:** Detallar en la **Columna 76 (JSON)**: `{"Tipo": "Retroactivo", "Nota": "Periodo aplicado"}`.

---

## 3. GRANULARIDAD ESPECÍFICA POR BLOQUE

### 3.1 Gas Natural (IDs Dinámicos)
Capturar etiquetas específicas para evitar "Ceguera de Granularidad":
* **Col 48 (Const):** Valor de la "Constante" (ej. 0.858).
* **Col 65 (G_CU_Transp7_V):** Valor unitario de "Transporte 7".
* **Col 69 (G_CU_Compr8_F):** Valor fijo de "Compresión 8".

### 3.2 Aseo (Desglose Forense de Toneladas)
Extraer las 4 clases técnicas del recuadro de residuos:
* **Col 71:** No Aprovechables.
* **Col 72:** Barrido y Limpieza.
* **Col 73:** Limpieza Urbana.
* **Col 74:** Rechazos.

### 3.3 Energía (Costo Unitario)
* **Cols 57 a 62:** Desglosar los 6 componentes del CU (G, T, D, C, P, R).
* **Col 48 (Const):** Factor Multiplicador (si aplica).

---

## 4. MATRIZ DE MAPEO (76 COLUMNAS)

| Bloque | Rango de Cols | Instrucción de Mapeo |
| :--- | :--- | :--- |
| **Identidad** | 1 a 19 | 'ID_Unico, 'Contrato, 'Ref_Pago, 'ID_Producto (Siempre con apóstrofe). |
| **Financiero** | 20 a 42 | Desglose de Variable, Fijo, Contribución y **Ajuste (Col 40)**. |
| **Técnico** | 43 a 47 | Cantidad, Unidad, 'Medidor, Lectura Ant y Act. |
| **Constantes** | 48 | Única ubicación para Factor Energía o Constante Gas. |
| **Unitarios** | 49 a 74 | Desglose de $/m3, $/kWh y Toneladas de Aseo. |
| **Cierre** | 75 a 76 | Alertas (NORMAL/AUDITORIA) e Info_Reg_Json. |

---

## 5. PROTOCOLO DE RELLENO TÉCNICO (0,00)
Para las filas de **OTRAS** y **TOTAL**, es obligatorio insertar `"0,00"` en las columnas **43 a 74**. Esto blindará la matriz contra desplazamientos laterales y permitirá que el campo de Alertas (75) y JSON (76) se mantengan alineados.

---

## 6. CHECKLIST DE AUTO-VALIDACIÓN (PRE-ENTREGA)
1. ¿Están las 8 filas en el orden ACUE -> TOTAL?
2. ¿Los retroactivos están en la columna 40 del servicio padre?
3. ¿Todos los IDs tienen apóstrofe inicial?
4. ¿Se capturaron las 4 clases de toneladas de aseo?
5. ¿La matriz tiene exactamente 76 columnas?

**FIN DE FICHA TÉCNICA v2.6.2**
