# GLOSARIO DE TÉRMINOS Y MAPA DE NAVEGACIÓN (UCMS)
**Versión:** v2.3.0
**Última Actualización:** 30-Dic-2025
**Propósito:** Definir el lenguaje común, la estructura física y los conceptos de negocio del Sistema UCMS.

---

### 1. ROLES Y DEFINICIONES DEL SISTEMA
* **UCMS (Utility Cost Management System):** Nombre global del proyecto.
* **GEM Admin (Hub):** Agente central. Orquestador y Arquitecto. No extrae, solo valida y consolida.
* **GEM Spoke (Radio/Agente):** Agente especialista (ej: EPM, Tigo). Su función es convertir documentos no estructurados (PDF) en tablas estructuradas (CSV).
* **Bloque A (Core):** Tabla maestra financiera de 22 columnas. Estandarizada para comparación global.
* **Bloque B (Vertical):** Tabla de extensión técnica. Específica por servicio. Sigue la estrategia del "Triángulo de Seguridad".
* **ID_Unico:** Llave primaria textual que vincula Bloque A y B. Formato: `'[PERIODO]_[PROVEEDOR]_[CONTRATO]_[SERVICIO]`.

---

### 2. ESTRUCTURA DE ARCHIVOS (MAPA)
**RAÍZ:** `UCMS_Project/`

├── **00_CONTEXTO/**
│   ├── `GLOSARIO_TERMINOS.md`       # Diccionario y definiciones (v2.3.0).
│   └── `HISTORIA_PROYECTO.md`       # Memoria evolutiva y decisiones de diseño ("Por qué").
│
├── **01_ESTANDARES/**
│   └── `OUTPUT_UNIVERSAL.md`        # [LEY SUPREMA] Definición de columnas y reglas de formato.
│
├── **02_SPOKES_PROMPTS/** # "Cerebros" autónomos de los Agentes.
│   ├── `PROMPT_EPM.md`              # Spoke Multiservicio (Estable v2.3.0).
│   ├── `PROMPT_TIGO.md`             # Spoke Telecom (Pendiente actualización).
│   ├── `PROMPT_AFINIA.md`           # Spoke Energía (Pendiente actualización).
│   ├── `PROMPT_SURTIGAS.md`
│   └── `PROMPT_ACUACAR.md`         # Spoke Gas (Pendiente actualización).
│
├── **03_OPERACIONES/**
│   ├── `CHANGELOG_ERRORES.md`       # Bitácora de cambios y fixes.
│   ├── `MANUAL_OPERACIONES_UCMS.md` # Protocolos de mantenimiento y reacción.
│   └── `METRICAS_KPI.md`            # Fórmulas para análisis financiero.
│
└── **04_DATA/** # Repositorio de CSVs y PDFs.

---

### 3. CONCEPTOS DE NEGOCIO Y ESTRATEGIA (NUEVO v2.3)

#### A. Triángulo de Seguridad (Blindaje de Datos)
Estrategia de almacenamiento para el **Bloque B** que garantiza la captura de datos útiles incluso si la estructura de la factura cambia.
1.  **Hard Fields (Datos Físicos):** Datos inmutables verificables físicamente. (Ej: Serial del Medidor, Lecturas). Son la prioridad #1 de extracción.
2.  **Structured Fields (Datos Financieros):** Desglose de componentes tarifarios en columnas explícitas (Generación, Transmisión, etc.).
3.  **Flexible Fields (Datos Contextuales):** Uso de formato JSON para capturar textos variables, justificaciones legales o novedades visuales (Ej: `{ "Alerta": "Desviación Justificada" }`).

#### B. Subsidios vs. Contribuciones
Manejo agnóstico del estrato socioeconómico en la columna `Valor_Subsidio`.
* **Subsidio:** Valor negativo (resta). Aplica a Estratos 1, 2, 3.
* **Contribución:** Valor positivo (suma). Aplica a Estratos 5, 6 y Comerciales. También llamado "Sobrecosto" o "Solidaridad".

#### C. Fila Total Condicional
* **Multiservicio (EPM):** Obligatorio generar una fila `_TOTAL` que consolide la factura.
* **Monoservicio (Tigo):** Prohibido generar fila total (el servicio es el total en sí mismo).

#### D. Autonomía del Prompt
Principio de diseño donde cada archivo `PROMPT_[SPOKE].md` contiene *todas* las reglas necesarias para la extracción (mapeos, fórmulas), sin depender del conocimiento base del modelo de IA ni de instrucciones externas.

#### E. Reglas de Formato Regional
* **Coma Decimal:** Uso exclusivo de `,` para decimales.
* **Blindaje de Tipos:** Uso de `'` al inicio de cadenas críticas (IDs, Fechas) para evitar auto-formato en hojas de cálculo.
