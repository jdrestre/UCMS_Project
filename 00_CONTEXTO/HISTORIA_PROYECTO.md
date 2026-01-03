# HISTORIA Y EVOLUCIÓN DEL PROYECTO UCMS

Este documento registra la trayectoria estratégica, los desafíos arquitectónicos y las soluciones de ingeniería que han permitido la evolución del Utility Cost Management System (UCMS).

---

## 🏷️ ESTRATEGIA DE VERSIONAMIENTO (SemVer)
**Formato:** vMAJOR.MINOR.PATCH (Ej: v1.2.0)

* **MAJOR (X.0.0):** Cambio estructural que rompe la compatibilidad (Ej: Cambiar la matriz de 65 a 76 columnas). Obliga a actualizar todas las Spokes.
* **MINOR (0.X.0):** Nueva funcionalidad o mejora lógica que no altera la estructura de la tabla (Ej: Nueva regla de detección de fechas).
* **PATCH (0.0.X):** Corrección de errores menores, ajustes de OCR o formato visual.

---

## 📜 HITOS Y EVOLUCIÓN TÉCNICA

### Hito v2.1.0: Modularidad Vertical y Eficiencia (Dic 2025)
* **Problema:** La tabla maestra de 22 columnas era inmanejable para datos técnicos (estrato, subsidios exactos). Sumar totales en facturas complejas generaba duplicidad.
* **Solución:**
    1.  Adopción de arquitectura **Core + Vertical**: Tabla resumen estandarizada + tablas satélite específicas.
    2.  Definición de **"Fila Total Condicional"**: Solo facturas complejas (EPM) generan fila de resumen para evitar redundancia en facturas simples (Tigo).

### Hito v2.3.0: Blindaje Técnico y Realidad Socioeconómica (Dic 2025)
* **Problema:** El sistema fallaba ante "Contribuciones" positivas (Estratos 5 y 6) y era rígido ante cambios visuales en componentes tarifarios, generando filas vacías.
* **Solución:**
    1.  **Estrategia "Triángulo de Seguridad":** Redefinición del Bloque B en tres niveles: *Hard Fields* (Medidores), *Structured Fields* (Tarifas) y *Flexible Fields* (JSON para future-proofing).
    2.  **Agnosticismo Socioeconómico:** Reglas para aceptar subsidios positivos (Contribución) o negativos (Descuento).
    3.  **Autonomía del Spoke:** Prompts con reglas de mapeo completas (Ej: Gas Compra = Generación) sin dependencia de entrenamiento base.

### Hito v2.5.0: Unificación y Modelo de Bloque Único (31-Dic-2025)
* **Problema:** La dualidad Bloque A/B generaba fricción operativa y riesgo de desincronización de IDs. La "Ceguera Técnica" impedía el seguimiento histórico de componentes como G o P.
* **Solución:**
    1.  **Modelo de Bloque Único Dinámico:** Fusión financiera y técnica en una sola matriz plana de alta densidad.
    2.  **Matriz de 65 Columnas (Piloto EPM):** Desglose independiente de componentes tarifarios y periodos.
    3.  **Optimización:** Formato `DD/MM/YYYY` y blindaje estricto con apóstrofe (`'`) para IDs protegidos.

### Hito v2.6.0: Era de la Granularidad Absoluta (02-Ene-2026)
* **Problema:** Persistencia de "Ceguera de Granularidad" en componentes dinámicos de Gas (Transporte/Compresión) y falta de detalle en residuos de Aseo. Desplazamientos de matriz en filas de totalización.
* **Solución:**
    1.  **Salto a 76 Columnas:** Expansión de la matriz para capturar IDs dinámicos (Transporte 7 en Col 65, Compresión 8 en Col 69).
    2.  **Desglose Forense de Aseo:** Captura de 4 tipos de toneladas (Cols 71-74) en lugar de datos genéricos.
    3.  **Protocolo OJF (Orden Jerárquico por Factura):** Obligatoriedad de extracción siguiendo el flujo físico del documento.
    4.  **Blindaje de Constante (Col 48):** Reubicación estratégica de variables técnicas para garantizar Cero Redundancia en el JSON.
    5.  **Relleno Técnico Forense:** Uso de `"0,00"` en campos técnicos de filas de total para proteger la estructura de la matriz.

---

## 🏛️ FILOSOFÍA DEL SISTEMA
1.  **Agnosticismo de Datos:** Capacidad de procesar cualquier GEM mediante Spokes personalizadas.
2.  **Cero Redundancia:** El dato reside en su columna técnica; el JSON es solo para sustento legal.
3.  **Integridad Forense:** Formatos estrictos para que la información sea 100% analizable en herramientas externas.
