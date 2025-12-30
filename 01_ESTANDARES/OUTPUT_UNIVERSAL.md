# ESTÁNDAR DE SALIDA UNIVERSAL (UCMS)
**Versión:** 2.2.0 (Triángulo de Seguridad + Desglose de Costos)
**Estado:** VIGENTE
**Fecha:** 29-Dic-2025

Todas las GEMs Spokes deben generar su extracción en DOS BLOQUES vinculados por el `ID_Unico`.

---

### REGLAS DE FORMATO TRANSVERSALES (v2.1.3)
1. **Números (Localización COL):**
   - **Separador Decimal:** Siempre COMA (`,`).
   - **Separador de Miles:** PROHIBIDO (No usar ni punto ni espacio).
   - *Ejemplo:* `1250600,50`
2. **Periodo (Protección de Celda):**
   - **Formato:** `'` + 3 Letras Mes (MAY) + `-` + Año (AAAA).
   - *Ejemplo:* `'ENE-2025`
3. **IDs Únicos:** Deben iniciar con apóstrofe si se pegan en hojas de cálculo para mantener la integridad de la cadena.

---

### BLOQUE A: TABLA MAESTRA (CORE)
**Destino:** Hoja `MASTER_CONSOLIDADA`
**Columnas:** 22 columnas obligatorias e inmutables.

| # | ID Columna | Descripción |
|:---|:---|:---|
| 1 | **ID_Unico** | `'` + `PERIODO` + `_` + `PROVEEDOR` + `_` + `CONTRATO` [+ `_SERVICIO`] |
| 2 | **Periodo** | `'MMM-AAAA` (Ej: `'OCT-2025`) |
| 3 | **Año** | AAAA (Ej: `2025`) |
| 4 | **Mes** | Nombre completo (Ej: `Octubre`) |
| 5 | **Ciudad** | (Ej: `Cartagena`, `Medellín`) |
| 6 | **Servicio** | `Energía`, `Gas`, `Agua`, `Alcantarillado`, `Aseo`, `TOTAL_FACTURA` |
| 7 | **Proveedor** | (Ej: `EPM`, `Tigo`, `Afinia`) |
| 8 | **Contrato** | Número de suscriptor |
| 9 | **Fecha_Inicio** | `d-mmm` (Ej: `1-oct`) |
| 10 | **Fecha_Fin** | `d-mmm` (Ej: `31-oct`) |
| 11 | **Dias_Fact** | Número entero |
| 12 | **Consumo_Cant** | Cantidad consumida o "1" (fijo) |
| 13 | **Unidad_Medida**| `kWh`, `m3`, `Plan`, `GLOBAL` |
| 14 | **Valor_Unitario**| (Float con coma) Precio unidad o Valor Plan Base |
| 15 | **Costo_Consumo** | (Float con coma) `Consumo` * `Unitario` |
| 16 | **Variables_Extra**| (Float con coma) Otros cobros (Alumbrado, Netflix) |
| 17 | **Deducciones** | (Float con coma) Valor POSITIVO de subsidios o negativo para ajustes |
| 18 | **Total_Pagar** | (Float con coma) Valor final |
| 19 | **Estado_Pago** | `Al día`, `En Mora`, `Pendiente` |
| 20 | **Fecha_Limite** | `d-mmm-aaaa` (Vencimiento) |
| 21 | **Lectura_Plan** | Lectura medidor o Velocidad Plan |
| 22 | **Alertas_Novedades**| Inteligencia Predictiva o "Normal" |

---

### BLOQUE B: EXTENSIÓN TÉCNICA (VERTICAL)
**Destino:** Hojas de detalle específicas (ej: `EXT_EPM`).
**Regla:** El `ID_Unico` debe coincidir exactamente con el del Bloque A. Los formatos numéricos siguen la regla de la coma decimal.
**Estrategia:** "Triángulo de Seguridad".

**1. HARD FIELDS (Auditoría Física):**
Datos inmutables que validan la legalidad del cobro.
* `Medidor_Serial`, `Lectura_Anterior`, `Lectura_Actual`, `Factor_Tecnico`.

**2. STRUCTURED FIELDS (Estructura Tarifaria):**
Desglose del Costo Unitario en columnas explícitas para análisis de variación.
* Energía/Gas: `Comp_Generacion`, `Comp_Transmision`, `Comp_Distribucion`, `Comp_Comercializacion`, `Comp_Perdidas`, `Comp_Restricciones`.
* Agua: `Comp_Admin`, `Comp_Operacion`, `Comp_Tasas`.
* Aseo: `Comp_Barrido`, `Comp_Recoleccion`, `Comp_Disposicion`.

**3. FLEXIBLE FIELDS (Future-Proofing):**
Datos en formato JSON para almacenamiento de textos regulatorios y calidad.
* `Info_Calidad_Json`: DIU, FIU, Presión, Calidad Agua.
* `Info_Regulatoria_Json`: Justificaciones de desviación, Normativas CREG/CRA citadas.
