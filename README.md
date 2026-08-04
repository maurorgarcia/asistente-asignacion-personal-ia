# Asistente Inteligente para la Asignación de Personal en Empresas Industriales

**Curso:** Inteligencia Artificial: Generación de Prompts | **Comisión:** #95970 | **Alumno:** Mauro García

---

## Introducción

### Nombre del proyecto
**Asistente Inteligente para la Asignación de Personal en Empresas Industriales mediante Prompt Engineering**

### Presentación del problema

En plantas industriales (manufactura, logística, siderurgia, petróleo y gas), la planificación diaria de turnos es una tarea crítica que se realiza de forma manual o mediante planillas estáticas. Los supervisores y el área de RRHH deben resolver diariamente una combinatoria compleja de variables:

- **Ausentismo imprevisto:** bajas médicas de último momento, vacaciones y permisos.
- **Matriz de competencias:** puestos críticos como Soldador Alta Presión u Operador de Autoelevador exigen certificaciones obligatorias y vigentes.
- **Restricciones normativas:** horas extras máximas, descansos interturnos mínimos, prioridades de producción.

Este proceso manual consume horas de supervisores de alto valor y genera errores frecuentes:
- Superposición de asignaciones (mismo empleado en dos sectores).
- Paradas de línea por falta de personal certificado en puestos clave.
- Asignación ineficiente del personal disponible.

**¿Por qué es relevante desarrollar una solución?**
El costo de una parada de línea no planificada en industrias como automotriz o siderurgia puede superar los miles de dólares por hora. Una solución basada en IA puede transformar este proceso artesanal en un flujo asistido, rápido, auditable y escalable, reduciendo errores y tiempos de respuesta de horas a segundos.

---

## Desarrollo de la propuesta de solución

La solución consiste en un **asistente de IA basado en Prompt Engineering** que procesa la nómina del personal, la matriz de habilidades y el parte de ausentismo diario para proponer en segundos la asignación óptima de turnos.

### Vinculación con modelos de IA

Se utilizan dos tipos de modelos:

1. **Modelo Texto-a-Texto (LLM):** Actúa como motor de razonamiento. Aplica reglas de negocio, filtra ausentismo, valida certificaciones y propone la distribución de puestos con explicación de cada decisión.
2. **Modelo Texto-a-Imagen (gratuito vía NightCafe / Pollinations.ai):** El LLM genera automáticamente un prompt descriptivo del estado de la planta para producir un diagrama visual comprensible por supervisores sin formación técnica.

### Descripción de los prompts por etapa

| Etapa | Técnica de Prompting | Qué resuelve |
|:------|:---------------------|:-------------|
| Contexto del sistema | Role Prompting | Define el perfil experto del modelo |
| Ejemplos de reglas | Few-Shot | Instruye al modelo con casos reales de ausencias y certificaciones |
| Razonamiento | Chain-of-Thought (CoT) | Audita paso a paso antes de proponer la asignación |
| Salida estructurada | Structured Output (JSON) | Garantiza que la respuesta sea parseable por código Python |
| Resumen visual | Prompt Texto-a-Imagen | Genera descripción para diagrama de planta |

---

## Justificación de la viabilidad del proyecto

| Dimensión | Análisis | Viabilidad |
|:----------|:---------|:-----------|
| **Técnica** | Uso de Google Gemini API (tier gratuito, sin tarjeta de crédito). Sin infraestructura ni entrenamiento de modelos. | ✅ Alta |
| **Datos** | Dataset sintético realista generado en Python. Extensible a datos reales de ERP/RRHH. | ✅ Alta |
| **Económica** | Costo: **$0 USD**. Tier gratuito de Gemini cubre miles de peticiones diarias. | ✅ Alta |
| **Tiempo** | Desarrollo modular completado en el plazo académico. | ✅ Alta |

**Optimización de consultas API:** El sistema consolida todas las etapas de razonamiento (filtrado de ausencias + validación de certificaciones + asignación + reporte + prompt visual) en una **única llamada a la API por jornada**. Esto lo hace técnicamente eficiente y económicamente rentable desde el primer día.

---

## Objetivos

**Objetivo general:** Demostrar mediante una POC en Jupyter Notebook que es posible optimizar la asignación diaria de personal en plantas industriales usando técnicas de Fast Prompting con costo cero.

**Objetivos específicos:**
1. Diseñar prompts que apliquen correctamente Role Prompting, Few-Shot y Chain-of-Thought.
2. Automatizar el filtrado de ausentismo y la validación de competencias requeridas por puesto.
3. Minimizar las llamadas a la API (máximo 1 por ciclo de asignación).
4. Generar salidas en formato JSON parseable y reporte ejecutivo legible.
5. Producir un prompt para herramienta Texto-a-Imagen que visualice el estado de la planta.

---

## Metodología

El proyecto se desarrolla fraccionando el problema complejo en etapas simples, cada una con un propósito claro:

```
Datos de entrada (Nómina + Ausentismo + Requerimientos)
        │
        ▼
Paso 1: Ingesta y estructuración de datos en Python (JSON/Pandas)
        │
        ▼
Paso 2: Construcción del Master Prompt (Role + Few-Shot + CoT + JSON Output)
        │
        ▼
Paso 3: 1 llamada a la API → Modelo procesa y devuelve JSON estructurado
        │
        ▼
Paso 4: Parseo del resultado → Tabla de asignaciones + Alertas operativas
        │
        ▼
Paso 5: Prompt visual → NightCafe / Pollinations.ai (sin costo adicional)
```

**¿Por qué este diseño?**
Cada paso tiene una responsabilidad única y es independiente. Esto facilita el debugging, permite reemplazar el modelo de IA sin cambiar la lógica, y asegura que si falla un paso no compromete el resto.

---

## Herramientas y tecnologías

### Técnicas de Fast Prompting aplicadas

| Técnica | Aplicación en este proyecto | Justificación |
|:--------|:----------------------------|:--------------|
| **Role Prompting** | `"Actúa como Experto en Logística de RRHH Industrial..."` | Define el dominio y tono de respuesta del modelo |
| **Few-Shot Prompting** | Reglas de negocio con ejemplos concretos (caso: certificación vencida, caso: empleado ausente) | Calibra el modelo con casos reales sin entrenarlo |
| **Chain-of-Thought (CoT)** | Instrucción explícita de razonar paso a paso antes de proponer la asignación | Reduce errores lógicos y hace las decisiones auditables |
| **Structured Output (JSON)** | Formato de salida obligatorio especificado en el prompt | Permite parsear la respuesta con Python sin procesamiento extra |

### Stack tecnológico

- **Lenguaje:** Python 3.10+
- **Librerías:** `google-generativeai`, `pandas`, `python-dotenv`
- **Modelo LLM:** Google Gemini 1.5 Flash (API gratuita — [obtener key aquí](https://aistudio.google.com/))
- **Imagen:** NightCafe o Pollinations.ai (gratuitos, sin registro requerido)
- **Entorno:** Jupyter Notebook / Google Colab

---

## Implementación

La implementación completa se encuentra en la Jupyter Notebook:

📓 **[poc_fast_prompting.ipynb](./poc_fast_prompting.ipynb)**

### Cómo ejecutarla

**Opción A — Google Colab (recomendado, sin instalar nada):**
1. Abrir el archivo en GitHub y hacer clic en el badge de Colab, o descargar el `.ipynb` e importarlo en [colab.research.google.com](https://colab.research.google.com).
2. Obtener una API Key gratuita en [aistudio.google.com](https://aistudio.google.com/) (requiere cuenta Gmail, sin tarjeta).
3. Reemplazar `"SU_API_KEY_AQUI"` en la primera celda de código.
4. Ejecutar todas las celdas (`Runtime > Run all`).

**Opción B — Local:**
```bash
git clone https://github.com/maurorgarcia/asistente-asignacion-personal-ia.git
cd asistente-asignacion-personal-ia
pip install -r requirements.txt
# Copiar .env.example a .env y agregar la API Key
jupyter notebook poc_fast_prompting.ipynb
```

---

*Mauro García — Preentrega 2 — Comisión #95970*
