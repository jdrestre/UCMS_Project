# GLOSARIO DE TÉRMINOS Y MAPA DE NAVEGACIÓN (UCMS)
**Versión:** v1.0.0
**Última Actualización:** 28-Dic-2025
**Propósito:** Definir el lenguaje común y la estructura física del Sistema de Gestión de Costos de Servicios Públicos (UCMS).

---

### 1. ROLES Y DEFINICIONES DEL SISTEMA
Para evitar ambigüedades, estas son las definiciones oficiales de los componentes:

* **UCMS (Utility Cost Management System):** Nombre global del proyecto.
* **GEM Admin (Hub):** El agente central. Actúa como Orquestador, Arquitecto y Analista Financiero. No extrae datos crudos; consume datos procesados.
* **GEM Spoke (Radio/Agente):** Agente especialista y limitado. Su única función es convertir un PDF/XML específico (ej: Tigo) en una tabla estructurada. No toma decisiones estratégicas.
* **Bloque A (Core):** Conjunto de datos financieros estandarizados (22 columnas) que permiten comparar peras con manzanas (ej: Gasto de Agua vs Gasto de Internet).
* **Bloque B (Vertical):** Conjunto de datos técnicos específicos de un servicio que permiten auditoría profunda (ej: Velocidad de bajada, Estrato, Subsidio exacto).
* **ID_Unico:** La llave maestra del sistema. Cadena de texto que vincula el Bloque A con el Bloque B. Formato: `[PERIODO]_[PROVEEDOR]_[CONTRATO]_[SERVICIO]`.

---

### 2. TERMINOLOGÍA TÉCNICA Y REGLAS
* **SemVer (Semantic Versioning):** Estrategia de control de cambios (vX.Y.Z).
    * **Major (X.0.0):** Cambio estructural (ej: agregar una columna al Core). Rompe compatibilidad.
    * **Minor (0.X.0):** Mejora funcional (ej: detectar avisos de alza). No rompe compatibilidad.
    * **Patch (0.0.X):** Corrección de errores (ej: arreglar un error de lectura de fecha).
* **Atomicidad:** Principio que exige que cada servicio facturado tenga su propia fila independiente. (Vital para EPM: Energía y Gas son átomos distintos).
* **Fila Total Condicional:** Regla lógica que dicta que solo las facturas multi-servicio (EPM) llevan una fila resumen `_TOTAL`. Las facturas mono-servicio (Tigo) no la llevan para evitar redundancia de datos.
* **Cero Alucinaciones:** Protocolo de seguridad que prohíbe a la IA inventar, estimar o completar datos que no estén explícitamente escritos en el documento fuente.

---

### 3. MAPA DE ESTRUCTURA DEL PROYECTO (FILE SYSTEM)
El Sistema UCMS reside en una estructura de carpetas jerárquica. La GEM Admin utiliza este mapa para entender la organización del conocimiento.

**RAÍZ:** `UCMS_Project/`

├── **00_CONTEXTO/**
│   ├── `GLOSARIO_TERMINOS.md`       # (ESTE ARCHIVO) Diccionario y Mapa.
│   └── `HISTORIA_PROYECTO.md`       # Memoria del sistema: Contexto evolutivo y decisiones de diseño ("Por qué es así").
│
├── **01_ESTANDARES/**
│   └── `OUTPUT_UNIVERSAL.md`        # [LEY SUPREMA] Reglas de las 22 columnas y lógica de Bloques A/B.
│
├── **02_SPOKES_PROMPTS/** # El "Cerebro" de cada Agente Spoke (Instrucciones).
│   ├── `PROMPT_ACUACAR.md`          # Instrucciones Agua/Alcantarillado (Cartagena).
│   ├── `PROMPT_EPM.md`              # Instrucciones Multi-Servicio (Medellín).
│   ├── `PROMPT_SURTIGAS.md`         # Instrucciones Gas/Brilla (Cartagena).
│   ├── `PROMPT_TIGO.md`             # Instrucciones Telecom (Hogar/Móvil).
│   └── `PROMPT_AFINIA.md`           # Instrucciones Energía (Caribe).
│
├── **03_OPERACIONES/**
│   ├── `CHANGELOG_ERRORES.md`       # Bitácora de versiones, errores detectados y arreglos aplicados.
│   └── `METRICAS_KPI.md`            # (Futuro) Fórmulas Python para análisis financiero automatizado.
│
└── **04_DATA/** # Datos brutos y procesados.
    ├── `DB_MAESTRA_UCMS.csv`        # La Base de Datos consolidada (Salida de las Spokes).
    ├── **HISTORICO_LEGACY/** # Instrucciones antiguas (Pre-v2.0) preservadas por seguridad.
    │   ├── `LEGACY_INSTR_EPM.txt`
    │   ├── `LEGACY_INSTR_TIGO.txt`
    │   └── ...
    └── **SAMPLE/** # PDFs de ejemplo para pruebas de regresión (Testeo de Spokes).
