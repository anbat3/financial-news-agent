# Agente AI para Análisis de Noticias Financieras

**Autor:** Anabel Arasanz  
**Fecha:** 28 de abril de 2025

## Descripción del Proyecto

- Este Agente AI automatiza el análisis de noticias financieras, extrayendo insights clave para inversores.
- Su arquitectura modular permite integrar nuevos modelos y métricas, ofreciendo un equilibrio entre precisión (OpenAI) y autonomía
(Zephyr).
- El proyecto se planteó para que cumpliera una serie de requisitos

## Nota sobre el proyecto
Este proyecto fue desarrollado contemplando ciertos requisitos específicos definidos en su contexto original.  
En futuras iteraciones, el flujo y el código podrían optimizarse para reducir redundancias y mejorar la eficiencia general.

---
## Metodología

### 1. Pipeline de Procesamiento
- **Extracción de entidades**
  - Identifica empresas y países mencionados en el texto.
  - Normaliza nombres de países a su forma oficial (ej: "USA" → "United States").
  - Excluye ciudades, estados, personas y organizaciones no financieras.

- **Generación de resúmenes**
  - Crea resúmenes concisos para cada entidad, enfocándose en su relevancia en el contexto financiero.

- **Clasificación de sentimiento**
  - Clasifica el tono como "positivo", "neutral" o "negativo" usando modelos de lenguaje.

- **Detección de sesgos**
  - Se aplica únicamente a resúmenes clasificados como "neutrales" para identificar polaridad oculta (umbral heurístico: ±0.15).

### 2. Modelos Utilizados
- **CrewAI (OpenAI, GPT-4.1-nano)**
  - Optimizado para tareas estructuradas de extracción, resumen y sentimiento.
  - Alta precisión en la interpretación de contexto.

- **Zephyr (Open Source, HuggingFace)**
  - Modelo de código abierto para comparación de resultados.
  - Costo reducido y flexibilidad en entornos sin API de OpenAI.

### 3. Herramientas Complementarias
- **Visualización interactiva**
  - Gráficos de barras e histogramas con Plotly.
  - Selector desplegable para explorar detalles por entidad.

- **Métricas de eficiencia**
  - Registro de tokens utilizados (OpenAI) y tiempo de procesamiento.

---

## Instalación

### 1. Clonar el repositorio
```bash
git clone <enlace del repositorio>
cd <repositorio>
```

### 2. Crear entorno virtual (opcional)
```bash
python -m venv venv
source venv/bin/activate  # Linux/Mac
venv\Scripts\activate     # Windows
```

### 3. Instalar dependencias
```bash
pip install pandas plotly textblob torch tiktoken ipywidgets             requests langchain-openai crewai transformers             google-colab
```

---

## Uso

1. Abrir el notebook:
```bash
jupyter notebook arasanz_project_aiagents.ipynb
```
2. Cargar el dataset de noticias financieras.
3. Ejecutar la extracción de entidades.
4. Generar resúmenes y clasificar sentimiento.
5. Visualizar resultados y métricas.

---

## Formato de Resultados

**Resultados CrewAI (GPT-4.1-nano):**
| date       | entity         | type     | summary | sentiment |
|------------|---------------|----------|---------|-----------|
| 2025-04-28 | United States  | country  | ...     | neutral   |

**Resultados CrewAI + Bias:**
| date       | entity         | type     | summary | sentiment | bias_flag |
|------------|---------------|----------|---------|-----------|-----------|
| 2025-04-28 | United States  | country  | ...     | neutral   |           |
