# MÉTRICAS Y KPIs DE GESTIÓN POR SPOKE (UCMS)
**Versión:** v2.3.1
**Última Actualización:** 30-Dic-2025
**Propósito:** Definir fórmulas específicas de negocio según la naturaleza de cada Spoke.

---

### 1. KPIs TRANSVERSALES (GLOBALES)
*Aplican a todas las facturas independientemente del proveedor.*

| KPI | Fórmula | Interpretación |
|:---|:---|:---|
| **Variación Mensual ($\Delta\%$)** | `((Total_Actual - Total_Anterior) / Total_Anterior) * 100` | Alerta si $\Delta > 15\%$. Indica explosión de gasto. |
| **Auditoría de Suma** | `| Total_Pagar - (Sumatoria_Conceptos) |` | Debe ser $< 10$ pesos. Detecta errores de lectura/OCR. |

---

### 2. KPIs SPOKE EPM (MULTI-SERVICIOS)
*Basados en la extracción profunda de componentes (v2.3.0+).*

#### A. Energía y Gas (Eficiencia Tarifaria)
* **Costo Unitario Real ($CU_{real}$):**
    * *Fórmula:* `(Costo_Consumo + Valor_Subsidio) / Consumo_Cant`
    * *Propósito:* Muestra el costo real por kWh/m3 incluyendo la Contribución de Estrato 6.
* **Peso de la Contribución ($W_{tax}$):**
    * *Fórmula:* `(Valor_Subsidio / Total_Pagar) * 100`
    * *Meta:* Verificar cumplimiento legal (Ej: Energía ~20%, Agua Variable).
* **Análisis de Componentes (Solo si Bloque B existe):**
    * *Generación vs Total:* `(Comp_Generacion / Valor_Unitario) * 100`
    * *Propósito:* Entender si el alza se debe a la compra de energía (fenómeno El Niño) o a la distribución (redes locales).

#### B. Acueducto (Eficiencia de Consumo)
* **Consumo Diario ($Q_{day}$):**
    * *Fórmula:* `Consumo_Cant / Dias_Fact`
    * *Propósito:* Detectar fugas. Un salto brusco en el promedio diario es la primera señal de una fuga invisible.

---

### 3. KPIs SPOKE TIGO (TELECOMUNICACIONES)
*Centrados en la relación Costo-Beneficio del plan.*

#### A. Costo por Mega ($P_{mbps}$)
* **Fórmula:** `Total_Pagar / Lectura_Plan (Velocidad)`
* *Propósito:* Evaluar si vale la pena renegociar el contrato. (Ej: Pagar $100.000 por 300Mb es mejor que $90.000 por 100Mb).
* *Nota:* Requiere que la columna `Lectura_Plan` extraiga la velocidad numérica (ej: 300).

#### B. Estabilidad de Precio
* **Fórmula:** `(Valor_Unitario_Actual - Valor_Unitario_Base_Contrato)`
* *Propósito:* Detectar si se acabaron las promociones de entrada o si aplicaron cláusulas de permanencia/aumento anual IPC.

---

### 4. KPIs SPOKE AFINIA / SURTIGAS (ENERGÍA PURA)
* **Factor de Penalización (Reactiva):**
    * *Fórmula:* `Variables_Extra (si contiene "Reactiva") / Total_Pagar`
    * *Propósito:* Identificar ineficiencias en equipos eléctricos (motores, aires acondicionados viejos) que generan multas.

---

### 5. GUÍA DE IMPLEMENTACIÓN
Para el analista (Usuario):
1.  **No mezclar peras con manzanas:** No comparar el $CU_{real}$ de EPM (Agua) con el de Afinia (Energía).
2.  **Uso de JSON:** Para explicar variaciones anómalas en los KPIs, consultar siempre la columna `Info_Regulatoria_Json` extraída por la Spoke (ej: "Desviación justificada").
