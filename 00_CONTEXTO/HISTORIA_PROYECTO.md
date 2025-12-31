# Estrategia de Versionamiento (SemVer)
## Formato: vMAJOR.MINOR.PATCH (Ej: v1.2.0)

### MAJOR (X.0.0): Cambio que rompe la compatibilidad.

Ejemplo: Cambiar la Tabla Maestra de 22 a 25 columnas. Todas las Spokes deben actualizarse.

### MINOR (0.X.0): Nueva funcionalidad o mejora lógica que no rompe la tabla.

Ejemplo: Agregar "Inteligencia Predictiva" a Tigo o mejorar la detección de fechas en EPM.

### PATCH (0.0.X): Corrección de errores pequeños o ajustes de formato.

Ejemplo: Tigo movió la fecha 2 cm a la derecha; corrección de OCR.

### Hito v2.1.0: Modularidad Vertical y Eficiencia (Dic 2025)
**Problema:** Intentar meter todos los datos técnicos (estrato, subsidios exactos, velocidad de internet) en la tabla maestra de 22 columnas la estaba haciendo inmanejable. Además, sumar totales en facturas complejas era difícil.
**Solución:**
1. Se adoptó arquitectura **Core + Vertical**: Una tabla resumen estandarizada y tablas satélite específicas por servicio.
2. Se definió la **"Fila Total Condicional"**: Solo las facturas complejas (EPM) generan una fila de resumen total para facilitar gráficos globales sin duplicar datos en facturas simples (Tigo).

### Hito v2.3.0: Blindaje Técnico y Realidad Socioeconómica (Dic 2025)
**Problema:**
Al auditar facturas de EPM de Estrato 6 (Ene-Mar 2025), el sistema colapsó en dos frentes:
1.  **Ceguera Financiera:** Asumía que `Subsidio` siempre era un descuento (negativo). Al encontrarse con "Contribuciones" (cobros positivos del +20% o +60%), la extracción fallaba o generaba datos matemáticamente incorrectos.
2.  **Rigidez Estructural:** Intentar extraer componentes tarifarios (Generación, Transmisión) columna por columna fallaba cuando el formato visual de la factura cambiaba levemente, generando filas vacías (`N/A`) y perdiendo datos valiosos de auditoría.

**Solución Arquitectónica:**
1.  **Estrategia "Triángulo de Seguridad":** Se redefinió el Bloque B en tres niveles de rigidez para garantizar que siempre se extraiga *algo*, incluso si la factura es difícil de leer:
    * *Hard Fields:* Datos físicos inmutables (Medidores).
    * *Structured Fields:* Tarifas desglosadas (si son legibles).
    * *Flexible Fields (JSON):* Un "balde" para capturar justificaciones legales y novedades visuales sin romper la tabla.
2.  **Agnosticismo Socioeconómico:** Se reescribió la regla de negocio para aceptar que un subsidio puede ser positivo (Contribución) o negativo (Descuento), dependiendo del estrato.
3.  **Autonomía del Spoke:** Se eliminó la dependencia de "instrucciones implícitas" o saludos protocolarios. El Prompt v2.3.0 contiene *todas* las reglas de mapeo (ej: Gas Compra = Generación) para no depender del entrenamiento base del modelo.
### Hito v2.5.0: Unificación y Modelo de Bloque Único (31-Dic-2025)
**Problema:**
La dualidad Bloque A/B (v2.3.0) generaba fricción operativa en el copiado/pegado y riesgo de desincronización de IDs. Además, la "Ceguera Técnica" impedía un seguimiento histórico fluido de componentes como Generación (G) o Pérdidas (P).

**Solución Arquitectónica:**
1. **Modelo de Bloque Único Dinámico:** Fusión de datos financieros y técnicos en una sola matriz plana. Cada servicio (Spoke) define su número de columnas bajo un núcleo común.
2. **Matriz de 65 Columnas (Piloto EPM):** Diseño de alta precisión que desglosa componentes tarifarios, lecturas y periodos de facturación en columnas numéricas independientes.
3. **Optimización de Formatos:** Adopción de `DD/MM/YYYY` para fechas (sin apóstrofe) y blindaje estricto con apóstrofe (`'`) para Contratos, Referentes e IDs de Producto.
