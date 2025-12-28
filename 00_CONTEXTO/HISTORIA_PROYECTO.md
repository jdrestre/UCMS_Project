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
