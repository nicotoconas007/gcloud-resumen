## Módulo 2 – Getting Started with Google Cloud Development

### Resumen
Este módulo introduce herramientas y servicios clave para empezar en Google Cloud:
- Cloud APIs: interfaces programáticas (HTTP/JSON o gRPC) para Compute, Storage, ML, Networking; requieren credenciales válidas (IAM, service accounts).
- Google Cloud SDK: conjunto de herramientas CLI (`gcloud`, `bq` y utilidades de Storage). Administrar recursos, autenticación y componentes (incluye `kubectl` como componente). Se recomienda `gcloud storage` en lugar de `gsutil` para comandos nuevos.
- Cloud Client Libraries: bibliotecas por lenguaje (Python, Node.js, Java, Go, PHP, Ruby, C++, C#, .NET); manejan autenticación y reintentos, optimizadas con gRPC y respetan convenciones del lenguaje.
- Cloud Shell: VM temporal con SDK preinstalado, editor en navegador y 5 GB persistentes.
- Cloud Code: plugins para IDEs (Cloud Shell Editor, VS Code, JetBrains) con flujos para Kubernetes y Cloud Run, integración con Secret Manager, asistencia en YAML de Kubernetes y despliegues.
- Cloud Workstations: entornos de desarrollo administrados, reproducibles y seguros en la nube (sobre Compute Engine).

### Quiz (oficial)
1) Which command-line tools does the Google Cloud SDK include? Select two.
   - A) gRPC
   - B) bq
   - C) node
   - D) ruby
   - E) gcloud
   - Respuestas: B) bq, E) gcloud

2) Which of the following statements about Cloud Code are true? Select two.
   - A) Cloud Code's YAML authoring assistance provides autocomplete and inline documentation for Docker/Kubernetes manifests
   - B) Cloud Code is only available in the Cloud Shell editor
   - C) Cloud Code integrates with Secret Manager to securely store sensitive data
   - D) Cloud Code works with both Cloud Run and Kubernetes applications
   - E) Cloud Code is an integrated development environment
   - Respuestas: C) integra con Secret Manager, D) funciona con Cloud Run y Kubernetes

3) Which of the following statements about Google Cloud Client Libraries are true? Select two.
   - A) Cloud Client Libraries support a language's natural conventions and styles
   - B) Should only be used when you cannot call Cloud APIs directly
   - C) Provided in all languages that can be used on Google Cloud
   - D) Include the Cloud SDK
   - E) Handle retry logic and authentication
   - Respuestas: A) convenciones del lenguaje, E) manejan reintentos y autenticación

### Preguntas de práctica adicionales
4) ¿Qué ventaja principal ofrece gRPC frente a HTTP/JSON para Cloud APIs?
   - A) Estructura binaria eficiente y menor latencia
   - B) Mayor facilidad de lectura humana
   - C) No requiere credenciales
   - D) Es específico de Python
   - Respuesta: A) Estructura binaria eficiente y menor latencia

5) ¿Cuál es el comando para listar las instancias de VM en tu proyecto?
   - A) gcloud compute instances list
   - B) bq instances list
   - C) gsutil vm list
   - D) gcloud vm describe
   - Respuesta: A) gcloud compute instances list

6) ¿Qué servicio permite un entorno temporal con SDK preinstalado accesible vía navegador?
   - A) Cloud Shell
   - B) Cloud Code
   - C) Cloud Workstations
   - D) App Engine
   - Respuesta: A) Cloud Shell

7) ¿Cuál es el reemplazo recomendado para `gsutil` en la administración de Cloud Storage?
   - A) gcloud storage
   - B) gcloud bucket
   - C) cloudcli storage
   - D) kubectl storage
   - Respuesta: A) gcloud storage