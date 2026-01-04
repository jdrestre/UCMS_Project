# 🛠️ NÚCLEO MAESTRO UCMS (v3.0.0)
**Identidad:** Admin UCMS Único (CTO/CFO) | **Estado:** Operativo

---

## 1. GLOBAL UCMS: SISTEMA (LAS REGLAS DE ORO)
*Estas reglas rigen a todos los componentes. Los archivos en CONFIG/ las heredan automáticamente.*

* **Formato:** Decimales con **COMA (,)**, Fechas **DD/MM/YYYY**, IDs con **'** (apóstrofe inicial).
* **Integridad (8 Filas):** Toda factura multiservicio debe generar: ACUE, ALCA, ENER, GAS, ASEO, ALUM, OTRAS, TOTAL.
* **Aislamiento Parental (Ajustes):** Los retroactivos se quedan en la fila del servicio de origen, columna **AJUSTE (Col 41)**. El detalle se va al JSON (Col 76).

---

## 2. CONTROL DE VERSIONES CENTRALIZADO
*El Sistema tiene una versión Core. Cada CONFIG/ maneja su propia versión técnica.*

**VERSIÓN GLOBAL DEL SISTEMA:** **v3.0.0**

| Proveedor | Archivo CONFIG | Versión Spoke | Base de Datos (DATA) | Estado |
| :--- | :--- | :--- | :--- | :--- |
| **EPM** | `EPM.md` | v2.6.2 | `EPM.csv` | ALINEADO |
| **TIGO** | `TIGO.md` | v1.0.0 | `TIGO.csv` | ESTÁNDAR |
| **AFINIA** | `AFINIA.md` | v1.0.0 | `AFINIA.csv` | ESTÁNDAR |
| **SURTIGAS** | `SURTIGAS.md` | v1.0.0 | `SURTIGAS.csv` | ESTÁNDAR |
| **ACUACAR** | `ACUACAR.md` | v1.0.0 | `ACUACAR.csv` | ESTÁNDAR |

---

## 3. DIRECTORIO DE PROVEEDORES Y ALCANCE
1. **EPM (Multiservicios):** Gestión de 76 columnas. Alta complejidad.
2. **TIGO (Hogar/Móvil):** Facturación fija y consumos adicionales.
3. **AFINIA / SURTIGAS / ACUACAR:** Servicios específicos de energía, gas y agua con sus propias lógicas de contribución.

---

## 4. GESTIÓN DEL REPOSITORIO
* **`CONFIG/`**: Contiene la inteligencia técnica (Prompts) de cada proveedor.
* **`DATA/`**: Contiene la historia física (CSVs) por proveedor.
* **`SOURCES/`**: Contiene los documentos PDF/Imagen para extracción.

---

## 5. BITÁCORA DE HITOS (LOG)
| Fecha | Versión Core | Autor | Descripción del Cambio |
| :--- | :--- | :--- | :--- |
| 03/01/2026 | v3.0.0 | Admin | **SIMPLIFICACIÓN TOTAL.** Unificación de Núcleo y creación de registro de versiones centralizado. |
