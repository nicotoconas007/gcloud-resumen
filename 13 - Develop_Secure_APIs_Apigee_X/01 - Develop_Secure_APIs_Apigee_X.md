## Develop and Secure APIs with Apigee X
Este módulo cubre los fundamentos de las APIs, cómo usar Apigee X como una plataforma de gestión de APIs para proteger, transformar y publicar tus servicios de backend.

### Fundamentos de APIs y REST
API (Interfaz de Programación de Aplicaciones): Un conjunto de reglas y métodos que permiten que diferentes programas de software se comuniquen entre sí.

Modelo Cliente-Servidor: El cliente solicita recursos y el servidor los proporciona.

Protocolo HTTP: El estándar de comunicación web usado por las APIs.

Métodos (Verbos): GET (leer), POST (crear), PUT (actualizar/reemplazar), DELETE (borrar).

Endpoint: Una URL que representa un recurso específico (ej: /clientes/123). Es el "sustantivo" de la API.

API RESTful: Un estilo de arquitectura que usa los componentes anteriores (HTTP, verbos, endpoints) para construir APIs sin estado y orientadas a recursos.

JSON (JavaScript Object Notation): El formato de datos ligero y preferido para las APIs REST, basado en pares clave-valor.

### Autenticación
- API Keys: Tokens simples para identificar al proyecto o aplicación que llama.
- OAuth 2.0: Un estándar para delegar autorización. Permite que una aplicación actúe en nombre de un usuario sin conocer su contraseña. Ideal para acceder a datos de usuario.
- Cuentas de Servicio: Identidades para aplicaciones/máquinas, no para humanos.

### Conceptos Clave de Apigee X
¿Qué es Apigee?: Es una plataforma de gestión de APIs. Actúa como una fachada o API Gateway que se sitúa delante de tus servicios de backend (ej. un servicio de Cloud Run, una API de Google, etc.).

API Proxy: Es el corazón de Apigee. Es la representación de tu API que los desarrolladores consumen. Su función principal es desacoplar el backend de la API pública. Puedes cambiar el backend sin afectar a tus consumidores.

Políticas (Policies): Son bloques de lógica reutilizables que se aplican en el flujo de una petición. Son la forma de implementar casi toda la funcionalidad en Apigee.

Flujos (Flows): Son la secuencia de pasos (políticas) que se ejecutan cuando llega una petición. Hay flujos para la petición (Request) y la respuesta (Response), y pueden ser condicionales (ej. if request.verb == 'GET').

API Product: Es un paquete de uno o más API Proxies que se ofrece a los desarrolladores. Aquí es donde se configuran las cuotas de uso y los niveles de acceso. Es la forma de "productizar" tus APIs.

Developer y App: Un Developer se registra en tu portal y crea una App. La App se suscribe a un API Product y a cambio recibe una API Key (o credenciales OAuth) para poder llamar a la API.

Developer Portal: Un sitio web de autoservicio para que los desarrolladores descubran tus APIs, lean la documentación y obtengan sus claves.

### Políticas Esenciales de Apigee (¡Crucial para el Examen!)

#### Seguridad
- VerifyAPIKey: Verifica que la petición incluya una API key válida y que esté asociada a un producto que permita el acceso al recurso solicitado.
- OAuthV2: Verifica tokens de acceso OAuth 2.0 (operación VerifyAccessToken) o genera nuevos tokens (operación GenerateAccessToken).

#### Gestión de Tráfico
- Quota: Limita el número de peticiones que una app puede hacer en un período de tiempo (ej. 100 peticiones por minuto). Se configura en el API Product.
- SpikeArrest: Protege contra picos de tráfico repentinos, limitando el número de peticiones por segundo/minuto a un valor fijo para evitar sobrecargar el backend.

#### Mediación (Transformación)
- AssignMessage: Crea o modifica mensajes (peticiones o respuestas). Se usa para cambiar cabeceras, el cuerpo (payload) o crear variables.
- ExtractVariables: Extrae datos de un mensaje (ej. de un payload JSON usando JSONPath) y los guarda en una variable de flujo para usarla en otras políticas.
- JavaScript: Permite ejecutar código JavaScript personalizado para lógica de transformación compleja que otras políticas no pueden manejar.
- RaiseFault: Detiene el flujo y devuelve un error personalizado. Muy útil para manejar errores del backend y no exponer información sensible.

#### Extensión (Llamadas a otros servicios)
- ServiceCallout: Hace una llamada a un servicio externo desde dentro del flujo del proxy (ej. llamar a una API de geocodificación o a la API de Cloud Natural Language).
- MessageLogging: Envía mensajes de log a un sistema externo como Cloud Logging.

### Quiz (práctica)
1) Quieres limitar el número total de llamadas que una aplicación de desarrollador puede hacer a tu API a 500 por día. ¿Qué combinación de componentes de Apigee usarías?
   - A) Una política SpikeArrest en el API Proxy.
   - B) Una política Quota definida dentro de un API Product al que la aplicación está suscrita.
   - C) Una política JavaScript para contar las peticiones manualmente.
   - D) Una regla de RaiseFault.
   - Respuesta: B ✅

2) Tu API Proxy necesita enriquecer una respuesta. Primero, debe llamar a un servicio externo para obtener datos adicionales y luego usar lógica compleja para fusionar esos datos con la respuesta original del backend. ¿Qué dos políticas usarías en secuencia?
   - A) AssignMessage y ExtractVariables.
   - B) ServiceCallout y JavaScript.
   - C) VerifyAPIKey y Quota.
   - D) RaiseFault y MessageLogging.
   - Respuesta: B ✅

3) ¿Cuál es el propósito principal de un API Proxy en Apigee?
   - A) Reemplazar completamente la necesidad de un servicio de backend.
   - B) Actuar como una fachada para desacoplar la API pública del servicio de backend, permitiendo añadir políticas de seguridad y gestión.
   - C) Únicamente para registrar desarrolladores y asignarles claves de API.
   - D) Alojar y ejecutar el código de la aplicación de backend.
   - Respuesta: B ✅

4) Una petición llega a tu API Proxy sin una API Key. Quieres que se rechace inmediatamente. ¿Qué política usarías y en qué parte del flujo la colocarías?
   - A) Quota en el TargetEndpoint Response Flow.
   - B) VerifyAPIKey en el ProxyEndpoint PreFlow (al inicio del flujo de la petición).
   - C) OAuthV2 en el ProxyEndpoint PostFlow.
   - D) SpikeArrest en el TargetEndpoint Request Flow.
   - Respuesta: B ✅

5) El servicio de backend devuelve un error con detalles técnicos sensibles. Quieres interceptar ese error y devolver un mensaje genérico al cliente. ¿Qué política es la ideal para esto?
   - A) AssignMessage
   - B) RaiseFault, dentro de una FaultRule.
   - C) ExtractVariables
   - D) ServiceCallout
   - Respuesta: B ✅

6) ¿Qué componente de Apigee es un sitio web de autoservicio donde los desarrolladores pueden explorar la documentación de tu API, registrar sus aplicaciones y obtener claves de API?
   - A) El API Proxy
   - B) El API Product
   - C) Un Shared Flow
   - D) El Developer Portal
   - Respuesta: D ✅

7) ¿Cuál es la diferencia principal entre las políticas Quota y SpikeArrest?
   - A) Quota protege contra picos de tráfico, SpikeArrest limita el uso total
   - B) Quota limita el uso total en un período, SpikeArrest protege contra picos repentinos
   - C) Ambas hacen exactamente lo mismo
   - D) Quota es para autenticación, SpikeArrest es para transformación
   - Respuesta: B ✅

8) ¿Qué política usarías para extraer el valor de un campo específico de un payload JSON y guardarlo en una variable?
   - A) AssignMessage
   - B) ExtractVariables
   - C) JavaScript
   - D) RaiseFault
   - Respuesta: B ✅

9) ¿Cuál es el formato de datos preferido para las APIs REST?
   - A) XML
   - B) JSON
   - C) CSV
   - D) HTML
   - Respuesta: B ✅

10) ¿Qué método HTTP se utiliza típicamente para crear nuevos recursos?
    - A) GET
    - B) POST
    - C) PUT
    - D) DELETE
    - Respuesta: B ✅

11) ¿Cuál es la principal ventaja de usar OAuth 2.0 sobre API Keys simples?
    - A) Es más rápido de implementar
    - B) Permite delegación de autorización y acceso a datos de usuario
    - C) No requiere configuración adicional
    - D) Es más barato de usar
    - Respuesta: B ✅

12) ¿Qué política usarías para modificar las cabeceras de una petición antes de enviarla al backend?
    - A) ExtractVariables
    - B) AssignMessage
    - C) ServiceCallout
    - D) MessageLogging
    - Respuesta: B ✅

13) ¿Cuál es el propósito de un API Product en Apigee?
    - A) Alojar el código de la aplicación backend
    - B) Empaquetar uno o más API Proxies con configuraciones de cuotas y acceso
    - C) Proporcionar documentación automática
    - D) Gestionar la autenticación de usuarios finales
    - Respuesta: B ✅

14) ¿Qué política usarías para enviar logs a Cloud Logging desde tu API Proxy?
    - A) AssignMessage
    - B) ExtractVariables
    - C) MessageLogging
    - D) JavaScript
    - Respuesta: C ✅

15) ¿Cuál es la característica principal de una API RESTful?
    - A) Usa solo el protocolo HTTP
    - B) Es sin estado y orientada a recursos
    - C) Requiere autenticación obligatoria
    - D) Solo funciona con JSON
    - Respuesta: B ✅

16) ¿Qué representa un endpoint en una API REST?
    - A) El servidor donde se aloja la API
    - B) Una URL que representa un recurso específico
    - C) El método de autenticación usado
    - D) El formato de los datos de respuesta
    - Respuesta: B ✅