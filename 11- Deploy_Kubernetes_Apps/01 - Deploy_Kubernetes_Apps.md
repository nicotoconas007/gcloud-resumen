## Deploy Kubernetes Applications on Google Cloud
Este módulo se centra en el flujo de trabajo completo para llevar una aplicación a Kubernetes: empaquetarla con Docker, almacenarla y finalmente desplegarla y gestionarla en un clúster de Google Kubernetes Engine (GKE).

### Docker: El Contenedor
¿Qué es Docker?: Es una plataforma para crear, enviar y ejecutar contenedores. Permite empaquetar una aplicación con todas sus dependencias (librerías, sistema operativo base, etc.) en una unidad portable llamada imagen.

Dockerfile: Es un archivo de texto con instrucciones para construir una imagen de Docker. Es como una receta.

Instrucciones clave del Dockerfile:
- FROM node:lts: Define la imagen base sobre la que se construye.
- WORKDIR /app: Establece el directorio de trabajo dentro del contenedor.
- COPY . .: Copia archivos desde tu máquina local al sistema de archivos del contenedor.
- RUN go install -v: Ejecuta un comando durante la construcción de la imagen (ej. instalar dependencias).
- EXPOSE 80: Documenta qué puerto expone la aplicación. No publica el puerto realmente.
- CMD ["node", "app.js"] / ENTRYPOINT ["app"]: Especifica el comando que se ejecutará cuando el contenedor se inicie.

Comandos Clave de Docker:
- docker build -t mi-app:0.1 .: Construye una imagen a partir de un Dockerfile en el directorio actual (.) y la etiqueta (-t) con un nombre y versión.
- docker run -p 4000:80 mi-app:0.1: Ejecuta un contenedor a partir de una imagen. El flag -p mapea un puerto del host (4000) a un puerto del contenedor (80). -d lo ejecuta en segundo plano.
- docker images: Lista las imágenes locales.
- docker ps: Lista los contenedores en ejecución. docker ps -a lista todos, incluso los detenidos.
- docker push ...: Sube una imagen a un registro remoto (como Artifact Registry).
- docker exec -it <id> bash: Obtiene una shell interactiva dentro de un contenedor en ejecución (muy útil para depurar).

Artifact Registry: Es el servicio recomendado en Google Cloud para almacenar imágenes de Docker y otros artefactos. Antes de subir una imagen, hay que autenticar Docker con gcloud auth configure-docker ....

### Google Kubernetes Engine (GKE): El Orquestador
¿Qué es GKE?: Es el servicio gestionado de Kubernetes en Google Cloud. GKE se encarga de la infraestructura (máquinas virtuales, red, etc.) para que tú te centres en desplegar tus aplicaciones.

Arquitectura Básica:
- Clúster: Es el conjunto de todo. Consiste en un plano de control y nodos.
- Nodos (Nodes): Son las máquinas virtuales (VMs de Compute Engine) que ejecutan tus contenedores.
- Pods: Es la unidad de despliegue más pequeña de Kubernetes. Un Pod contiene uno o más contenedores que se ejecutan juntos en el mismo nodo y comparten red y almacenamiento. Los Pods son efímeros (pueden ser destruidos y recreados en cualquier momento).
- kubectl: Es la herramienta de línea de comandos para interactuar con un clúster de Kubernetes. Es el "control remoto" del clúster.

### Objetos Clave de Kubernetes (Conceptos de Examen)
Deployment:
- ¿Qué es?: Un objeto que gestiona un conjunto de Pods idénticos (réplicas). Su trabajo es asegurar que el número deseado de réplicas siempre esté en ejecución.
- Función: Si un Pod falla, el Deployment automáticamente crea uno nuevo para reemplazarlo. También gestiona las actualizaciones progresivas (rolling updates).
- Comando: kubectl create deployment mi-app --image=...

Service:
- ¿Qué es?: Un objeto que define un punto de acceso estable y único para un conjunto de Pods.
- Problema que resuelve: Como los Pods pueden ser destruidos y recreados (cambiando su IP), el Service proporciona una IP y un nombre DNS fijos para que otras partes de tu aplicación o usuarios externos puedan conectarse a ellos de forma fiable.

Tipos de Service (importante para el examen):
- ClusterIP (por defecto): Expone el servicio solo a una IP interna del clúster. Solo accesible desde otros Pods.
- NodePort: Expone el servicio en un puerto estático en la IP de cada nodo. Accesible desde fuera del clúster, pero no es ideal para producción.
- LoadBalancer: El más común para exponer servicios a internet. Crea un balanceador de cargas de red externo en Google Cloud y le asigna una IP pública.

Comando: kubectl expose deployment mi-app --type=LoadBalancer --port 8080

### Quiz (práctica)
1) ¿Cuál es el propósito principal de un objeto Deployment en Kubernetes?
   - A) Exponer un conjunto de Pods a internet con una IP fija.
   - B) Asegurar que un número específico de réplicas de un Pod estén siempre en ejecución y gestionar sus actualizaciones.
   - C) Almacenar datos de forma persistente para un Pod.
   - D) Construir una imagen de contenedor a partir de un Dockerfile.
   - Respuesta: B ✅

2) Quieres exponer tu aplicación web, gestionada por un Deployment, al tráfico de internet público. ¿Qué tipo de Service es el más adecuado para esta tarea en un entorno de GKE?
   - A) ClusterIP
   - B) NodePort
   - C) LoadBalancer
   - D) ExternalName
   - Respuesta: C ✅

3) ¿Cuál es la unidad de despliegue más pequeña y básica en Kubernetes, que encapsula uno o más contenedores?
   - A) Un Service
   - B) Un Deployment
   - C) Un Nodo
   - D) Un Pod
   - Respuesta: D ✅

4) ¿Qué comando de Docker usarías para ejecutar un contenedor en segundo plano y mapear el puerto 8080 de tu máquina al puerto 3000 del contenedor?
   - A) docker run -p 3000:8080 mi-imagen
   - B) docker start -d -p 8080:3000 mi-imagen
   - C) docker run -d -p 8080:3000 mi-imagen
   - D) docker exec -p 8080:3000 mi-imagen
   - Respuesta: C ✅

5) En un Dockerfile, ¿cuál es la diferencia entre la instrucción RUN y CMD?
   - A) RUN se ejecuta cuando el contenedor inicia, CMD se ejecuta cuando la imagen se construye.
   - B) RUN ejecuta comandos para construir la imagen (ej. instalar paquetes), CMD especifica el comando por defecto para ejecutar el contenedor.
   - C) No hay diferencia, son intercambiables.
   - D) CMD es para configurar variables de entorno, RUN es para ejecutar la aplicación.
   - Respuesta: B ✅

6) ¿Qué servicio de Google Cloud es el recomendado para almacenar y gestionar de forma privada tus imágenes de contenedor antes de desplegarlas en GKE?
   - A) Cloud Storage
   - B) Artifact Registry
   - C) Container Registry (legacy)
   - D) Cloud Source Repositories
   - Respuesta: B ✅

7) ¿Cuál de los siguientes tipos de Service de Kubernetes NO permite acceso desde fuera del clúster?
   - A) ClusterIP
   - B) NodePort
   - C) LoadBalancer
   - D) ExternalName
   - Respuesta: A ✅

8) ¿Qué herramienta de línea de comandos se utiliza para interactuar con un clúster de Kubernetes?
   - A) gcloud
   - B) kubectl
   - C) docker
   - D) kubeadm
   - Respuesta: B ✅

9) ¿Cuál es la diferencia entre ClusterIP y NodePort en los Services de Kubernetes?
   - A) ClusterIP expone el servicio fuera del clúster, NodePort solo internamente
   - B) ClusterIP solo es accesible dentro del clúster, NodePort expone el servicio en un puerto estático en cada nodo
   - C) No hay diferencia, son sinónimos
   - D) ClusterIP es para aplicaciones web, NodePort para APIs
   - Respuesta: B ✅

10) ¿Qué comando de kubectl se utiliza para crear un Deployment?
    - A) kubectl create deployment mi-app --image=mi-imagen
    - B) kubectl deploy mi-app --image=mi-imagen
    - C) kubectl run deployment mi-app --image=mi-imagen
    - D) kubectl apply deployment mi-app --image=mi-imagen
    - Respuesta: A ✅