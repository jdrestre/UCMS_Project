# MÉTRICAS Y KPIs DE GESTIÓN (UCMS)
**Versión:** v2.3.0
**Última Actualización:** 30-Dic-2025
**Propósito:** Definir las fórmulas matemáticas para transformar los datos crudos (CSV) en inteligencia de negocio.

---

### 1. DEFINICIÓN DE VARIABLES (DICCIONARIO DE DATOS)
Las fórmulas utilizan los nombres de columna definidos en `OUTPUT_UNIVERSAL.md`.

* **$C_{total}$**: `Total_Pagar` (Valor final de la factura).
* **$Q$**: `Consumo_Cant` (Cantidad consumida: kWh, m3).
* **$V_{sub}$**: `Valor_Subsidio` (Valor monetario de subsidio o contribución).
    * *Nota v2.3:* Recordar que en Estrato 5/6, este valor es una Contribución (+).
* **$D_{fact}$**: `Dias_Fact` (Días facturados en el periodo).

---

### 2. KPIs FINANCIEROS (COSTOS)

#### A. Costo Unitario Real ($CU_{real}$)
Revela cuánto cuesta realmente cada unidad consumida incluyendo impuestos y contribuciones, descontando subsidios.
* **Fórmula:** `(Costo_Consumo + Variables_Extra + Valor_Subsidio - Deducciones) / Q`
* **Interpretación:** Si este valor sube mientras el consumo se mantiene, el proveedor subió tarifas o cambió la regulación.

#### B. Impacto del Estrato ($I_{socio}$)
Mide cuánto subsidia o contribuye el usuario al sistema.
* **Fórmula:** `(Valor_Subsidio / Costo_Consumo) * 100`
* **Meta:** Verificar que coincida con la ley (Ej: +20% Energía Estrato 6).

---

### 3. KPIs TÉCNICOS (EFICIENCIA)

#### A. Consumo Promedio Diario ($Q_{day}$)
Normaliza el consumo para comparar periodos de diferentes duraciones (ej: 28 días vs 32 días).
* **Fórmula:** `Q / D_{fact}`
* **Uso:** La métrica más precisa para detectar fugas o cambios de hábito.

#### B. Variación Mensual ($\Delta\%$)
Mide la aceleración del gasto/consumo.
* **Fórmula:** `((Valor_Actual - Valor_Anterior) / Valor_Anterior) * 100`
* **Alerta:** Si $\Delta\% > 15\%$ sin justificación estacional, revisar `Alertas_Novedades`.

---

### 4. AUDITORÍA DE FACTURACIÓN (BLINDAJE)

#### A. Validación de Total ($Check_{sum}$)
Verifica si la factura suma correctamente (detecta errores de OCR o del proveedor).
* **Fórmula:** `| Total_Pagar - (Costo_Consumo + Variables_Extra + Valor_Subsidio - Deducciones) |`
* **Regla:** El resultado debe ser menor a `10` (pesos) por tolerancias de redondeo. Si es mayor, marcar como `ERROR_CALCULO`.
