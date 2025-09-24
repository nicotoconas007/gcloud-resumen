## Prompt Engineering
Este módulo cubre los conceptos fundamentales detrás de los modelos de lenguaje y las mejores prácticas para interactuar con ellos de manera efectiva.

### Conceptos Fundamentales de IA Generativa
IA Generativa (Gen AI): Es un subconjunto de la inteligencia artificial que crea contenido nuevo (texto, imágenes, audio, etc.) en respuesta a una instrucción o prompt. Aprende patrones de datos de entrenamiento para generar contenido similar.

Modelo de Lenguaje Grande (LLM): Es un tipo específico de IA Generativa enfocado en tareas de lenguaje.

"Grande" se refiere al tamaño del set de datos de entrenamiento y al número de parámetros (el conocimiento aprendido por el modelo).

Son pre-entrenados con datos masivos y pueden ser ajustados (fine-tuned) para tareas específicas.

### Alucinaciones (Hallucinations)
Es cuando un LLM genera una respuesta que es incorrecta, inventada o sin sentido.

Causas comunes:
- Datos de entrenamiento insuficientes o de mala calidad
- Falta de contexto en el prompt
- Falta de restricciones claras

### Ingeniería de Prompts (Prompt Engineering)
¿Qué es un Prompt?: El texto (instrucción, pregunta) que se le da al modelo.

¿Qué es Prompt Engineering?: El arte y la ciencia de diseñar prompts efectivos para obtener la respuesta deseada de un LLM. Un buen prompt mejora la calidad de la salida.

### Tipos de Prompts (¡clave para el examen!)
- Zero-shot: Solo la pregunta, sin ejemplos. Ej: ¿Cuál es la capital de Francia?
- One-shot: Se proporciona un ejemplo para dar contexto. Ej: Italia: Roma. Francia: ?
- Few-shot: Se proporcionan dos o más ejemplos. Ej: Italia: Roma. Japón: Tokio. Francia: ?
- Prompt de Rol (Role Prompting): Se le pide al modelo que adopte una personalidad o rol específico. Ej: Actúa como un arquitecto de la nube experto...

### Elementos de un Prompt
- Preámbulo: El contexto, las instrucciones y los ejemplos (si los hay). Prepara al modelo.
- Input: La pregunta o tarea concreta sobre la que debe actuar el modelo.

### Mejores Prácticas (¡Importante!)
Ser Detallado y Explícito: Las instrucciones vagas producen resultados vagos. Sé claro en lo que quieres.
- Mal: Resume la reunión.
- Bien: Resume la reunión en un párrafo. Luego, haz una lista de los puntos clave de cada orador.

Definir Límites: Es mejor decirle al modelo qué hacer en lugar de qué no hacer. Dale una ruta de escape si no sabe la respuesta.
- Bien: Si no tienes una película para recomendar, responde "Lo siento, hoy no encontré ninguna recomendación".

Adoptar una Persona/Rol: Darle un rol al modelo (Actúa como...) proporciona un contexto muy valioso y mejora la precisión de las respuestas.

Ser Conciso y Simple: Divide las peticiones largas y complejas en frases y tareas más simples.

### Quiz (práctica)
1) Le pides a un LLM: "Actúa como un chef profesional y dame una receta de pasta carbonara auténtica". ¿Qué tipo de prompt estás utilizando principalmente?
   - A) Zero-shot
   - B) One-shot
   - C) Few-shot
   - D) Prompt de Rol (Role Prompting)
   - Respuesta: D ✅

2) ¿Qué se entiende por "alucinación" en el contexto de un LLM?
   - A) Una respuesta que es creativamente excepcional.
   - B) Una respuesta que es factualmente incorrecta, inventada o sin sentido.
   - C) La capacidad del modelo para procesar imágenes.
   - D) Un error de sintaxis en el prompt del usuario.
   - Respuesta: B ✅

3) ¿Cuál de las siguientes es una de las mejores prácticas recomendadas para la ingeniería de prompts?
   - A) Usar frases largas y complejas para mostrar todo el contexto de una vez.
   - B) Ser lo más vago posible para permitir que el modelo sea creativo.
   - C) Darle al modelo una persona específica para que adopte.
   - D) Evitar dar ejemplos para no sesgar al modelo.
   - Respuesta: C ✅

4) Si le das a un modelo el siguiente prompt: "Clasifica el sentimiento. 'Amo este producto': Positivo. 'Odio este producto': Negativo. 'Este producto está bien': ?", ¿qué tipo de prompt es?
   - A) Zero-shot
   - B) One-shot
   - C) Few-shot
   - D) Role Prompting
   - Respuesta: C ✅

5) ¿Cuál es la relación correcta entre IA Generativa y los LLMs?
   - A) Son exactamente lo mismo.
   - B) La IA Generativa es un tipo de LLM.
   - C) Los LLMs son un tipo de IA Generativa enfocada en tareas de lenguaje.
   - D) No tienen ninguna relación.
   - Respuesta: C ✅

6) ¿Qué significa "Grande" en el contexto de Modelo de Lenguaje Grande (LLM)?
   - A) El tamaño físico del servidor donde se ejecuta
   - B) El tamaño del set de datos de entrenamiento y número de parámetros
   - C) La cantidad de usuarios que pueden acceder simultáneamente
   - D) El tamaño del archivo de configuración
   - Respuesta: B ✅

7) ¿Cuál de los siguientes elementos NO es parte de un prompt bien estructurado?
   - A) Preámbulo (contexto e instrucciones)
   - B) Input (pregunta o tarea concreta)
   - C) Configuración del servidor
   - D) Ejemplos (en algunos casos)
   - Respuesta: C ✅

8) ¿Cuál es el tipo de prompt más simple que se puede usar?
   - A) Few-shot
   - B) One-shot
   - C) Zero-shot
   - D) Role Prompting
   - Respuesta: C ✅

9) ¿Qué causa común de alucinaciones se puede mitigar mejorando el prompt?
   - A) Datos de entrenamiento insuficientes
   - B) Falta de contexto en el prompt
   - C) Calidad de los datos de entrenamiento
   - D) Limitaciones del hardware
   - Respuesta: B ✅

10) ¿Cuál es una mejor práctica para evitar resultados vagos en un LLM?
    - A) Usar instrucciones vagas para mayor creatividad
    - B) Ser detallado y explícito en las instrucciones
    - C) Evitar dar contexto adicional
    - D) Usar solo prompts de una palabra
    - Respuesta: B ✅

11) ¿Qué tipo de prompt proporciona el mayor contexto al modelo?
    - A) Zero-shot
    - B) One-shot
    - C) Few-shot
    - D) Todos proporcionan el mismo contexto
    - Respuesta: C ✅

12) ¿Cuál es la principal ventaja de usar Role Prompting?
    - A) Reduce el costo de procesamiento
    - B) Proporciona contexto valioso y mejora la precisión de las respuestas
    - C) Acelera el tiempo de respuesta
    - D) Reduce el uso de memoria
    - Respuesta: B ✅

13) ¿Qué significa "fine-tuned" en el contexto de LLMs?
    - A) Ajustado para tareas específicas después del entrenamiento inicial
    - B) Optimizado para mayor velocidad
    - C) Reducido en tamaño para ahorrar espacio
    - D) Configurado para múltiples idiomas
    - Respuesta: A ✅

14) ¿Cuál es la mejor estrategia para manejar peticiones complejas a un LLM?
    - A) Enviar todo en una sola instrucción larga
    - B) Dividir en tareas más simples y concisas
    - C) Usar solo comandos de una palabra
    - D) Evitar dar instrucciones específicas
    - Respuesta: B ✅