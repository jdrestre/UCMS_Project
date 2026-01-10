# ⚡ UCMS - Utility Cost Management System

> **Sistema de Auditoría Forense de Servicios Públicos basado en IA Modular Dinámica.**
> *Granularidad Absoluta y Arquitectura Bicapa*

---

## 🚀 El Sistema UCMS
El **Utility Cost Management System (UCMS)** es un ecosistema de ingeniería de datos diseñado para la extracción, normalización y auditoría técnica de facturas de servicios públicos complejos. A diferencia de un extractor convencional, el UCMS opera como un sistema modular que separa las reglas de negocio globales de la lógica específica de cada proveedor.

### 🏗️ Arquitectura del Sistema
EL UCMS define las instrucciones en cada módulo de proveedor que se encuentra en la carpeta `CONFIG`. Cada módulo contiene las reglas específicas para interpretar y procesar las facturas de un proveedor particular. La carpeta `DATA` almacena los datos normalizados extraídos de las facturas, facilitando su análisis y auditoría.

## 📂 Estructura Orgánica del Proyecto

```../UCMS_Project/
├── CONFIG
│   ├── ACUACAR.md
│   ├── AFINIA.md
│   ├── EPM.md
│   ├── SURTIGAS.md
│   └── TIGO.md
├── DATA
│   ├── ACUACAR.csv
│   ├── AFINIA.csv
│   ├── EPM.csv
│   ├── SURTIGAS.csv
│   └── TIGO.csv
├── README.md
└── SOURCES
    ├── 11) Noviembre 2025 Surtigas generar_factura.php.pdf
    ├── 12) Diciembre 2025 Acuacar Pagar.pdf
    ├── AGO2025 Regulado_6691509222_08082025.pdf
    ├── JUN2025 Regulado_6691509220_06062025.pdf
    ├── TIgo Hogar Octubre 2025 900092385_18764098297031_BOPU126974439_01.pdf
    ├── Tigo Nov2025 900092385_18764098297031_BOPU128229461_01.pdf
    └── nov2025 epm_110598289621.pdf
