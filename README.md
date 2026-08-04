# Asistente Inteligente para la Asignación de Personal de Empresas Industriales mediante Prompt Engineering

**Curso:** Inteligencia Artificial: Generación de Prompts  
**Comisión:** #95970  
**Autor:** Mauro García  
**Entrega:** Preentrega 2 - Proof of Concept (POC) & Repositorio del Proyecto Final  

---

## 📋 Tabla de Contenidos
1. [Introducción & Presentación del Problema](#1-introducción--presentación-del-problema)
2. [Desarrollo de la Propuesta de Solución](#2-desarrollo-de-la-propuesta-de-solución)
3. [Justificación de la Viabilidad del Proyecto](#3-justificación-de-la-viabilidad-del-proyecto)
4. [Objetivos del Proyecto](#4-objetivos-del-proyecto)
5. [Metodología & Flujo de Trabajo](#5-metodología--flujo-de-trabajo)
6. [Herramientas y Tecnologías (Técnicas de Prompting)](#6-herramientas-y-tecnologías-técnicas-de-prompting)
7. [Implementación y Guía de Ejecución](#7-implementación-y-guía-de-ejecución)
8. [Estructura del Repositorio](#8-estructura-del-repositorio)

---

## 1. Introducción & Presentación del Problema

### Nombre del Proyecto
**Asistente Inteligente para la Asignación de Personal de Empresas Industriales mediante Prompt Engineering**

### Presentación de la Problemática
En el sector industrial (plantas de manufactura, logística, petróleo y gas, siderurgia), la planificación diaria de turnos y la asignación de operarios a puestos de trabajo es una tarea compleja que habitualmente se realiza de forma manual o mediante planillas estáticas.

Los supervisores de planta y los departamentos de Recursos Humanos enfrentan diariamente una multiplicidad de variables dinámicas:
- **Ausentismo imprevisto:** Licencias médicas de último momento, vacaciones y permisos.
- **Matriz de Competencias y Certificaciones:** Puestos críticos (ej. Operador de Autoelevador, Soldador Alta Presión) exigen certificaciones obligatorias y vigentes.
- **Restricciones Operativas y Normativas:** Límites de horas extras, descansos mínimos interturnos y prioridades de producción.

### Relevancia del Desarrollo de la Solución
Realizar este proceso manualmente consume horas operativas de alto valor y genera un elevado margen de error humano:
- Superposición de asignaciones (un mismo empleado asignado a dos sectores).
- Paradas de línea por falta de personal certificado en puestos clave.
- Asignación ineficiente de personal disponible.

Una solución basada en **Prompt Engineering** permite transformar un proceso artesanal y propenso a fallas en un **flujo asistido por IA**, rápido, escalable y con alto nivel de precisión en la toma de decisiones.

---

## 2. Desarrollo de la Propuesta de Solución

La solución consiste en una arquitectura asistida por Inteligencia Artificial Generativa que procesa la nómina de personal, la matriz de habilidades y los partes de ausentismo para proponer la distribución óptima de turnos.

### Vinculación con Modelos de IA
1. **Modelo Texto-a-Texto (LLM - Google Gemini API / OpenAI):**
   Actúa como motor de razonamiento lógico. Filtra nóminas activas, valida restricciones operativas y resuelve la combinación óptima de puestos respetando las competencias exigidas.
2. **Modelo Texto-a-Imagen (NightCafe / Pollinations.ai / DALL-E):**
   Utiliza los prompts descriptivos generados por el LLM para sintetizar diagramas de flujo y esquemas visuales de distribución para la alta gerencia y supervisores de planta.

---

## 3. Justificación de la Viabilidad del Proyecto

El proyecto presenta una **alta viabilidad técnica, operativa y económica**, ya que se sustenta en modelos maduros de acceso público sin requerir entrenamiento de modelos desde cero.

### Matriz de Viabilidad y Recursos
| Dimensión | Detalle / Recurso Requerido | Nivel de Viabilidad |
| :--- | :--- | :--- |
| **Técnica** | Uso de LLMs mediante APIs de nivel gratuito (Google Gemini API / Groq). | **Alta**: No requiere infraestructura especializada ni entrenamiento de modelos. |
| **Datos / Contexto** | Casos reales/sintéticos estructurados de plantas industriales. | **Alta**: Reglas de negocio claras y representativas. |
| **Económica / Costos** | Acceso a tiers gratuitos ($0 USD) con cuota holgada para POC. | **Alta**: Inversión inicial de **$0 USD**. |
| **Tiempo** | Desarrollo modular e iteración de prompts en 2-3 semanas. | **Alta**: Compatible con los plazos académicos. |

### Optimización de Costos y Consultas API
Para garantizar la rentabilidad y sostenibilidad del proyecto:
- **Consolidación de Prompts:** En lugar de realizar 5 a 10 peticiones individuales por cada consulta, se combinan las etapas de razonamiento (Auditoría + Asignación + Explicabilidad) en un flujo optimizado de **máximo 2 consultas por ciclo**.
- **Formato JSON Estructurado:** Reduce el desperdicio de tokens en texto introductorio o redundante.

---

## 4. Objetivos del Proyecto

### Objetivo General
Desarrollar una Prueba de Concepto (POC) mediante una Jupyter Notebook que demuestre la viabilidad de optimizar la asignación diaria de personal en plantas industriales utilizando técnicas avanzadas de **Fast Prompting**.

### Objetivos Específicos
1. Diseñar e implementar prompts estructurados utilizando **Role Prompting**, **Few-Shot Prompting** y **Chain-of-Thought (CoT)**.
2. Automatizar el filtrado de ausentismo y la concordancia de habilidades requeridas por puesto.
3. Minimizar la cantidad de llamadas a la API para maximizar la eficiencia técnica y económica.
4. Generar salidas en formato estructurado (JSON) y reportes ejecutivos explicativos.

---

## 5. Metodología & Flujo de Trabajo

El proyecto se desarrolla bajo una metodología de fraccionamiento de problemas complejos en etapas simples:

```
[Datos de Entrada: Nómina + Ausentismo + Requerimientos]
                          │
                          ▼
           ┌─────────────────────────────┐
           │   Etapa 1: Fast Prompting   │
           │  (Filtro & Nómina Activa)   │
           └──────────────┬──────────────┘
                          │
                          ▼
           ┌─────────────────────────────┐
           │   Etapa 2: Chain-of-Thought │
           │ (Matriz & Matcheo Puestos)  │
           └──────────────┬──────────────┘
                          │
                          ▼
           ┌─────────────────────────────┐
           │  Etapa 3: Reporte Ejecutivo │
           │ & Prompt Visual Diagrama    │
           └─────────────────────────────┘
```

1. **Ingesta de Datos:** Carga de nómina total y partes de ausentismo diario en estructuras JSON/Pandas.
2. **Procesamiento Lógico:** Filtrado de personal apto y cruce automático con puestos críticos.
3. **Auditoría y Explicabilidad:** Verificación paso a paso para evitar superposición de turnos o paradas de planta.
4. **Síntesis Visual:** Generación de prompts de entrada para herramientas Texto-a-Imagen.

---

## 6. Herramientas y Tecnologías (Técnicas de Prompting)

### Técnicas de Fast Prompting Aplicadas:
- **Role Prompting:** Definición explicita del perfil: `"Actúa como un Experto en Logística de RRHH y Operaciones Industriales..."`
- **Few-Shot Prompting:** Inclusión de ejemplos concretos de entradas (empleados, ausencias) y la salida esperada en formato JSON para calibrar al modelo.
- **Chain-of-Thought (CoT):** Instrucciones explícitas para razonar la verificación de ausencias y certificaciones antes de proponer la asignación final.
- **Structured Output (JSON Enforcement):** Garantiza que las respuestas sean parseables computacionalmente sin texto extra.

### Stack Tecnológico:
- **Lenguaje:** Python 3.10+
- **Librerías principales:** `google-generativeai`, `pandas`, `python-dotenv`
- **Entorno:** Jupyter Notebook (`.ipynb`) / Google Colab
- **Modelo LLM:** Google Gemini 1.5 Flash (Tier Gratuito API)

---

## 7. Implementación y Guía de Ejecución

### Requisitos Previos
1. Tener instalado Python 3.10 o superior.
2. Obtener una API Key gratuita de Google Gemini en [Google AI Studio](https://aistudio.google.com/).

### Instalación Local
```bash
# Clonar el repositorio
git clone https://github.com/tu-usuario/asistente-asignacion-personal-ia.git
cd asistente-asignacion-personal-ia

# Crear entorno virtual (opcional pero recomendado)
python -m venv venv
# En Windows:
venv\Scripts\activate

# Instalar dependencias
pip install -r requirements.txt
```

### Configuración de Variables de Entorno
Copia el archivo `.env.example` a `.env` e ingresa tu API Key:
```env
GEMINI_API_KEY=tu_api_key_aqui
```

### Ejecución de la Notebook
Abre la notebook en tu entorno local o impórtala directamente en Google Colab:
```bash
jupyter notebook poc_fast_prompting.ipynb
```

---

## 8. Estructura del Repositorio

```text
asistente-asignacion-personal-ia/
├── README.md                 # Documentación principal del proyecto
├── poc_fast_prompting.ipynb  # Notebook interactiva con la POC del proyecto
├── requirements.txt          # Dependencias de Python requeridas
└── .env.example              # Plantilla para la configuración de API Key
```

---
*Mauro García - Preentrega 2 - Comisión #95970*
