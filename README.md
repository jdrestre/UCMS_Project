# ⚡ UCMS - Utility Cost Management System

> **Sistema de Auditoría de Servicios Públicos basado en IA Modular.**
> *Versión Actual: v2.1.1 (Arquitectura Relacional Core + Vertical)*

![Diagrama del Sistema UCMS](https://via.placeholder.com/800x400?text=Sistema+UCMS:+Hub+%26+Spoke+Architecture)
*(Aquí puedes subir la imagen de tus GEMs al repositorio y reemplazar este link)*

---

## 📖 ¿Qué es este proyecto?

El **UCMS** es un ecosistema de Agentes de IA (GEMs) diseñado para automatizar la extracción, auditoría y análisis financiero de facturas de servicios públicos en Colombia (Medellín y Cartagena).

A diferencia de los lectores de PDF tradicionales, este sistema utiliza una arquitectura **Hub & Spoke** (Cerebro Central + Especialistas) que permite:
1.  **Normalizar datos:** Convierte facturas dispares (Tigo, EPM, Afinia) en una base de datos estándar.
2.  **Auditoría Profunda:** Detecta anomalías técnicas (lecturas de medidores, estratos, factores de corrección).
3.  **Inteligencia Predictiva:** Lee la "letra pequeña" para alertar sobre futuras alzas de tarifas.

---

## 🏗️ Arquitectura del Sistema

El sistema opera bajo dos principios de datos inmutables:

1.  **Bloque A (Core):** Una tabla maestra de **22 Columnas** estandarizada para todos los servicios. Permite consolidación financiera.
2.  **Bloque B (Vertical):** Tablas de extensión técnica específicas para cada proveedor (ej: *Velocidad de Internet* para Tigo, *Subsidios* para EPM).

### 🤖 Los Agentes (GEMs)

| Rol | Agente (GEM) | Función Principal | Tipo de Salida |
| :--- | :--- | :--- | :--- |
| **HUB** | 🧠 **Admin UCMS** | Orquestador, Arquitecto y Analista Financiero. Valida estándares. | Auditoría y SQL |
| **SPOKE** | ⚡ **EPM** | Energía, Gas, Agua (Medellín). Maneja **Filas Múltiples**. | Core + Vertical + Total |
| **SPOKE** | 📡 **Tigo** | Telecomunicaciones. Detecta planes y apps. | Core + Vertical |
| **SPOKE** | 🔌 **Afinia** | Energía (Costa). Desglosa Aseo/Alumbrado. | Core + Vertical |
| **SPOKE** | 🔥 **Surtigas** | Gas y Crédito Brilla. Audita cupos. | Core + Vertical |
| **SPOKE** | 💧 **Acuacar** | Agua y Alcantarillado (Cartagena). | Core + Vertical |

---

## 📂 Estructura del Repositorio

* **`00_CONTEXTO/`**: Mapas del sistema y glosario.
* **`01_ESTANDARES/`**: Reglas de la Tabla Maestra (Core). **¡No tocar sin autorización!**
* **`02_SPOKES_PROMPTS/`**: Los "Cerebros" de cada IA. Aquí se edita la lógica de extracción.
* **`03_OPERACIONES/`**: Manuales de reacción ante errores y Changelog.
* **`04_DATA/`**: Datos históricos y CSVs maestros (Ignorado por git por seguridad).

---

## 🛠️ Guía de Mantenimiento y Mejora

### ¿Cómo actualizar el sistema?

1.  **Si una factura cambia de diseño:**
    * Edita el archivo correspondiente en `02_SPOKES_PROMPTS/` (ej: `PROMPT_TIGO.md`).
    * Registra el cambio en `03_OPERACIONES/CHANGELOG_ERRORES.md`.
    * *Nota:* No olvides avisarle a la GEM Admin sobre el cambio.

2.  **Si quieres agregar un nuevo dato al estándar:**
    * Esto es un cambio **MAJOR**. Debes editar `01_ESTANDARES/OUTPUT_UNIVERSAL.md`.
    * Debes actualizar **TODOS** los prompts de las Spokes para que cumplan la nueva regla.

3.  **Flujo de Trabajo Diario:**
    * Procesa la factura en su **Spoke**.
    * Copia el **Bloque A** a la Hoja Maestra.
    * Copia el **Bloque B** a la Hoja de Detalle del servicio.
    * Consulta al **Admin** para análisis de tendencias.

---

> **Nota:** Este sistema se rige por la regla de **"Cero Alucinaciones"**. Si un dato no está en el PDF, las IAs deben reportar `N/A`.
