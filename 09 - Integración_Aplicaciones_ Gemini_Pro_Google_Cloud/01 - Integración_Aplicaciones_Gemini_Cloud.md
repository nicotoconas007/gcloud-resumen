## Integración con Gemini 1.0 Pro en Google Cloud
Este módulo introduce Vertex AI como la plataforma para usar los modelos de IA generativa de Google, con un enfoque en la familia de modelos Gemini.

### Vertex AI y Modelos Base
Vertex AI: Es una plataforma de aprendizaje automático (AA) unificada. Sirve para entrenar, personalizar y desplegar modelos de AA y aplicaciones de IA. Permite usar los LLMs de Google a través de su SDK de Python.

IA Generativa en Vertex AI: Proporciona acceso a los modelos de base de Google a través de APIs.

Ajuste de Modelo (Fine-Tuning): Es el proceso de personalizar un modelo de base para que se especialice en tareas específicas. Beneficios: reduce costos y latencia al no necesitar instrucciones tan largas y complejas.

Modelos de Base Clave:
- Gemini: El más avanzado para razonamiento, chat multi-turno y multimodalidad (texto, imagen, video, código).
- PaLM: Para tareas de lenguaje natural, chat y embeddings de texto.
- Codey: Especializado en generación, finalización y chat de código.
- Imagen: Para generación, edición y subtítulos de imágenes.
- MedLM: Especializado en resúmenes y preguntas del dominio médico.

### API de Gemini y sus Modelos
API de Gemini de Vertex AI: Contiene los extremos de publicador (publisher endpoints) para acceder a los modelos Gemini. No es necesario desplegar los modelos base, solo se consumen sus APIs.

Modelos de Gemini:
- Gemini 1.0 Pro: Diseñado para tareas de lenguaje natural y código (basado en texto). Ideal para chatbots, resúmenes, generación de código, etc.
- Gemini 1.0 Pro Vision: Es multimodal. Acepta instrucciones que combinan texto, imágenes y/o video en una misma solicitud. Ideal para describir imágenes, responder preguntas sobre videos, etc.

Beneficios de la API de Gemini:
- Potencia: Acceso a modelos de última generación.
- Flexibilidad: Capacidad de procesar múltiples modalidades.
- Escalabilidad: Diseñada para uso empresarial (seguridad, residencia de datos).
- Facilidad de uso: SDKs para Python, Node.js, Java y Go.

### Quiz (práctica)
1) ¿Cuál de las siguientes opciones describe los modelos de Gemini 1.0 Pro y Gemini 1.0 Pro Vision?
   - A) Un modelo se usa para traducción y, el otro, se usa para responder preguntas.
   - B) Ambos modelos son adecuados para casos de uso médicos.
   - C) Un modelo maneja instrucciones basadas en texto y, el otro, instrucciones multimodales con texto, imágenes o video.
   - D) Un modelo se especializa solo en la generación de texto, mientras que el otro se especializa solo en la generación de imágenes.
   - Respuesta: C

2) Debes crear un chatbot diseñado para responder de manera informativa y amistosa las preguntas de los clientes sobre los productos de tu empresa. ¿Cuál modelo de Gemini 1.0 Pro es la mejor opción para esta tarea?
   - A) Ninguno de los modelos de Gemini 1.0 Pro es adecuado para chatbots.
   - B) Gemini 1.0 Pro Vision
   - C) Gemini 1.0 Pro
   - D) Ambos modelos, Gemini 1.0 Pro y Gemini 1.0 Pro Vision, son igualmente aptos.
   - Respuesta: C (Nota: Un chatbot de texto no necesita capacidades multimodales, por lo que Gemini 1.0 Pro es la opción correcta y más eficiente).

3) ¿Cuál es la función principal de Vertex AI en el ecosistema de Google Cloud?
   - A) Es un servicio de base de datos NoSQL.
   - B) Es una plataforma unificada para el ciclo de vida completo del aprendizaje automático.
   - C) Es una herramienta para la gestión de redes virtuales (VPC).
   - D) Es un servicio de almacenamiento de objetos similar a Cloud Storage.
   - Respuesta: B ✅

4) Tu equipo necesita generar código Python a partir de descripciones en lenguaje natural. ¿Cuál es el modelo de base más especializado para esta tarea?
   - A) API de PaLM
   - B) API de Imagen
   - C) APIs de Codey
   - D) MedLM
   - Respuesta: C ✅

5) ¿Qué término se utiliza para describir el proceso de personalizar un modelo de base de Google en Vertex AI para mejorar su rendimiento en una tarea específica?
   - A) Despliegue (Deployment)
   - B) Inferencia (Inference)
   - C) Ajuste de modelo (Fine-tuning)
   - D) Publicación (Publishing)
   - Respuesta: C ✅

6) ¿Cómo se accede a los modelos de base como Gemini en Vertex AI para su uso en aplicaciones?
   - A) Descargando el modelo e instalándolo en una VM de Compute Engine.
   - B) A través de un extremo de publicador (publisher endpoint) específico del modelo.
   - C) Creando una conexión directa de Cloud Interconnect.
   - D) Únicamente a través de la consola de Google Cloud.
   - Respuesta: B ✅