## Módulo 5 – Adding Intelligence to Your Application

### Resumen
Puntos clave para añadir inteligencia con servicios de ML y Generative AI en Google Cloud.

#### 1) Machine Learning y APIs pre‑entrenadas
- Objetivo: agregar capacidades inteligentes sin ser experto en ML.
- Acceso: invocación por REST/gRPC → JSON request/response.
- APIs principales:
  - Vision API: detección de objetos, OCR, landmarks, logos, rostros, contenido explícito.
  - Speech‑to‑Text: audio → texto (110+ lenguajes y variantes).
  - Text‑to‑Speech: texto → audio natural (voces y estilos personalizables).
  - Translation API: traducción rápida y dinámica a múltiples idiomas.
  - Natural Language API: entidades, sentimiento, clasificación de contenido, sintaxis.
  - Video Intelligence API: anotación y etiquetado de video (shot/frame/video‑level), timestamps.

#### 2) Vertex AI y AutoML
- AutoML (Vertex AI): entrena modelos de alta calidad sin escribir código (imágenes, tabular, texto, video).
- Vertex AI: ciclo completo de ML con tus datos y frameworks (TensorFlow, PyTorch), entrenamiento, despliegue y MLOps.

#### 3) Generative AI
- Crea contenido a partir de lo aprendido (foundation models: LLMs, modelos de imagen/código/audio).
- LLMs: datasets masivos (hasta PB) y miles de millones/trillones de parámetros; pre‑entrenados y luego fine‑tuning para tareas específicas.
- Diferencias clave:
  - Programación tradicional: reglas explícitas → respuestas.
  - ML clásico: datos + etiquetas → aprende patrones para una tarea.
  - Generative AI: modelos fundacionales multimodales → creación, resumen, búsqueda y automatización.

#### 4) Casos de uso
- Contenido: generación/mejora de texto e imágenes.
- Resumen y Q&A: de video, audio y documentos.
- Búsqueda/descubrimiento de información y productos.
- Automatización de flujos: extracción/clasificación de contratos, creación de tickets.
- Desarrollo de software: generación/explicación/arreglo/completado/traducción de código.
- Asistentes: Vertex AI Codey APIs y Gemini para productividad del desarrollador.

Referencia: [Module 5 – Adding intelligence to your application](https://storage.googleapis.com/cloud-training/devapps-foundations/en/on-demand/v1.2.0/Module5-AddingIntelligenceToYourApplication.pdf)
Más info: [Code models overview (Vertex AI Codey)](https://cloud.google.com/vertex-ai/docs/generative-ai/code/code-models-overview), [Actualizaciones de Gemini (2024)](https://blog.google/technology/ai/google-gemini-update-sundar-pichai-2024/)

### Quiz (oficial)
1) How can you invoke pre‑trained ML APIs (Vision, Natural Language) from your application?
   - A) Google Cloud console
   - B) gcloud CLI
   - C) TensorFlow
   - D) REST API
   - Respuesta: D) REST API

2) You're developing an app that labels entities in video before storing the files. Which API should you use?
   - A) Vision API
   - B) Cloud Translation API
   - C) Video Intelligence API
   - D) Cloud Natural Language API
   - Respuesta: C) Video Intelligence API

### Preguntas extra (práctica estilo certificación)
3) Which API should you use to perform sentiment analysis on customer reviews?
   - A) Vision API
   - B) Natural Language API
   - C) Translation API
   - D) Speech‑to‑Text
   - Respuesta: B) Natural Language API

4) Which service allows you to train custom ML models without writing code?
   - A) TensorFlow
   - B) AutoML on Vertex AI
   - C) BigQuery ML
   - D) Cloud Functions
   - Respuesta: B) AutoML on Vertex AI

5) You need to transcribe a multilingual podcast into text. Which API do you use?
   - A) Vision API
   - B) Speech‑to‑Text API
   - C) Translation API
   - D) BigQuery
   - Respuesta: B) Speech‑to‑Text API

6) Which service provides pre‑trained ML models usable with simple API calls?
   - A) Cloud SQL
   - B) Google Cloud AI APIs (Vision, Speech, Translation, NLP, Video Intelligence)
   - C) Memorystore
   - D) Dataproc
   - Respuesta: B) Google Cloud AI APIs

7) Large Language Models (LLMs) are described as “large” because:
   - A) Run only on large compute clusters
   - B) Use massive datasets and billions/trillions of parameters
   - C) Require manual rule definition
   - D) Only work with structured data
   - Respuesta: B) Use massive datasets and billions/trillions of parameters

8) You want near‑real‑time dynamic translation of UI strings for international users. Which API?
   - A) Natural Language API
   - B) Translation API
   - C) Vision API
   - D) Text‑to‑Speech
   - Respuesta: B) Translation API

9) Your app must extract entities and categorize support tickets by topic. Which API?
   - A) Speech‑to‑Text
   - B) Natural Language API
   - C) Video Intelligence API
   - D) Translation API
   - Respuesta: B) Natural Language API

10) You need to generate unit tests and refactor code from Python to Go. What do you use?
   - A) Vision API
   - B) Vertex AI Codey APIs / Gemini
   - C) AutoML Tables
   - D) Cloud Functions
   - Respuesta: B) Vertex AI Codey APIs / Gemini