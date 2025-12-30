# ESTÁNDAR DE SALIDA UNIVERSAL (UCMS)
**Versión:** 2.3.0 (Soporte Estrato Alto + Triángulo de Seguridad)
**Estado:** VIGENTE
**Fecha:** 30-Dic-2025

Todas las GEMs Spokes deben generar su extracción en DOS BLOQUES vinculados por el `ID_Unico`.

---

### REGLAS DE FORMATO TRANSVERSALES
1. **Números (Localización COL):**
   - **Separador Decimal:** OBLIGATORIO usar COMA (`,`).
   - **Separador de Miles:** PROHIBIDO (Ni puntos ni espacios).
   - *Ejemplo:* `15400,50`
2. **Periodo (Protección de Celda):**
   - **Formato:** `'` + 3 Letras Mes (MAY) + `-` + Año (AAAA).
   - *Ejemplo:* `'ENE-2025`. (Excepción Septiembre: `'SEPT-2025`).
3. **IDs Únicos:**
   - Deben iniciar con apóstrofe (`'`) para asegurar integridad de texto en CSV.

---

### BLOQUE A: TABLA MAESTRA (CORE)
**Destino:** Hoja `MASTER_CONSOLIDADA`
**Objetivo:** Comparabilidad Financiera Global.
**Columnas:** 22 columnas obligatorias e inmutables.

| # | ID Columna | Descripción y Regla de Llenado |
|:---|:---|:---|
| 1 | **ID_Unico** | Fórmula: `'[PERIODO]_[PROVEEDOR]_[CONTRATO]_[SERVICIO]` |
| 2 | **Periodo** | Formato `'MMM-AAAA` (Ej: `'OCT-2025`) |
| 3 | **Año** | AAAA (Ej: `2025`) |
| 4 | **Mes** | Nombre completo (Ej: `Octubre`) |
| 5 | **Ciudad** | Ciudad de prestación (Ej: `Medellín`) |
| 6 | **Servicio** | Valores permitidos: `Energía`, `Gas`, `Agua`, `Alcantarillado`, `Aseo`, `Alumbrado`, `TOTAL_FACTURA` |
| 7 | **Proveedor** | Empresa prestadora (Ej: `EPM`, `Tigo`, `Afinia`) |
| 8 | **Contrato** | Número de contrato o suscriptor principal |
| 9 | **Fecha_Inicio** | Fecha inicio periodo facturado (Texto con Año) |
| 10 | **Fecha_Fin** | Fecha fin periodo facturado (Texto con Año) |
| 11 | **Dias_Fact** | Entero |
| 12 | **Consumo_Cant** | Cantidad numérica consumida. Si es cargo fijo único, poner `1` |
| 13 | **Unidad_Medida**| `kWh`, `m3`, `Plan`, `GLOBAL` |
| 14 | **Valor_Unitario**| (Float con coma) Precio por unidad o Valor Plan Base |
| 15 | **Costo_Consumo** | (Float con coma) Resultado de `Consumo` * `Unitario` |
| 16 | **Variables_Extra**| (Float con coma) Suma de otros cobros menores (Tasas, Impuestos menores, Cargo Fijo) |
| 17 | **Deducciones** | (Float con coma) Ajustes al peso o descuentos |
| 18 | **Total_Pagar** | (Float con coma) Valor final neto a pagar por el servicio |
| 19 | **Estado_Pago** | `Al día`, `En Mora`, `Pendiente` |
| 20 | **Fecha_Limite** | Fecha de vencimiento o pago oportuno |
| 21 | **Lectura_Plan** | Lectura actual del medidor o Velocidad del Plan (Texto) |
| 22 | **Alertas_Novedades**| Detección Visual (Ej: `ALERTA: DESVIACION`, `ALERTA: CAMBIO_MEDIDOR`, `Normal`) |

---

### BLOQUE B: EXTENSIÓN TÉCNICA (VERTICAL)
**Destino:** Hojas de detalle específicas (ej: `EXT_EPM`).
**Estrategia:** "Triángulo de Seguridad" para evitar re-procesamientos.

**1. HARD FIELDS (Auditoría Física):**
Datos inmutables que validan la legalidad del cobro.
* `Ref_Producto`: ID específico del servicio (distinto al contrato).
* `Medidor_Serial`: Serial del equipo físico.
* `Lectura_Ant`: Lectura anterior del medidor.
* `Lectura_Act`: Lectura actual del medidor.
* `Factor_Tecnico`: Multiplicador o factor de corrección.

**2. STRUCTURED FIELDS (Estructura Tarifaria):**
Desglose del Costo Unitario para análisis de variación.
* **Regla de Subsidios/Contribuciones (v2.3.0):**
    * `Porc_Subsidio`: Porcentaje aplicado.
    * `Valor_Subsidio`: Valor monetario absoluto.
    * *Nota:* Si es Estrato 5/6, el valor es **POSITIVO** (Contribución). Si es Estrato 1-3, es **NEGATIVO** (Subsidio).
* **Componentes:** `Comp_Generacion`, `Comp_Transmision`, `Comp_Distribucion`, `Comp_Comercializ`, `Comp_Perdidas`, `Comp_Restricciones`, `Comp_Admin`, `Comp_Operacion`, `Comp_Tasas`, `Comp_Aseo_BL`, `Comp_Aseo_RT`, `Comp_Aseo_DF`.

**3. FLEXIBLE FIELDS (Future-Proofing JSON):**
* `Info_Calidad_Json`: Indicadores técnicos (DIU, FIU, Presión).
* `Info_Regulatoria_Json`: Novedades visuales, justificaciones de desviación, textos legales.
