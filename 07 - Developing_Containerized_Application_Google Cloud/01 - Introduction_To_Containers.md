## Módulo 1 – Introduction to Containers

### Resumen
- Un contenedor empaqueta la app y sus dependencias para ejecución consistente en cualquier entorno. Comparte el kernel del host (a diferencia de las VMs que ejecutan un SO invitado completo).
- Beneficios: portabilidad, eficiencia y velocidad en despliegue/escala.

### Conceptos clave
- Imagen: plantilla inmutable con app, dependencias y config.
- Contenedor: instancia en ejecución de una imagen.
- Dockerfile: instrucciones para construir la imagen.
- Buenas prácticas de imagen:
  - Escanear vulnerabilidades; eliminar archivos y herramientas innecesarias.
  - No ejecutar como root; usar imágenes base slim/alpine.
  - Definir proceso principal con CMD/ENTRYPOINT.
  - Usar multi‑stage builds para imágenes más pequeñas y seguras.

### Cloud Build
- Servicio para construir, probar y desplegar contenedores; integra con GitHub, GitLab, Bitbucket y CSR.
- Soporta Dockerfiles y Buildpacks; útil en pipelines CI/CD (no solo manual).

### Buildpacks
- Generan imágenes desde código sin Dockerfile, ejecutados por “builders” (OCI).
- Fases: detect → build.
- Ventajas: simplicidad; compatible con Cloud Run y Cloud Build.

### Dockerfile vs Buildpacks
- Dockerfile: control total y personalización avanzada.
- Buildpacks: sencillez para stacks estándar (Node.js, Python, Java…).

### Seguridad y optimización
- Usar imágenes ligeras; eliminar restos de build; escanear antes de desplegar; gestionar env vars y secretos de forma segura.

### Quiz (oficial)
1) What are best practices for containers/images? (Select three)
   - A) Scan images for vulnerabilities
   - B) Launch main process with CMD/ENTRYPOINT
   - C) Run as root by default
   - D) Remove unnecessary files/tools from image
   - Respuestas: A, B, D

2) Which statements about Cloud Build are correct? (Select two)
   - A) Only manual builds are possible
   - B) Continuously build, test and deploy on Google Cloud
   - C) Cannot use Dockerfile
   - D) Integrates with GitHub/Bitbucket/GitLab in addition to CSR
   - Respuestas: B, D

3) Which statements about using Docker are correct? (Select three)
   - A) Dockerfiles provide a flexible mechanism to create images
   - B) Build fails if base image not local (no download)
   - C) You must pre‑build your app before Docker
   - D) Multi‑stage builds create optimized/secure images
   - E) Dockerfile is a set of instructions to build an image
   - Respuestas: A, D, E

4) Which statements about Buildpacks are correct? (Select three)
   - A) Builders support a single language only
   - B) Builder runs detect and build phases
   - C) Google Cloud’s buildpacks are built into Cloud Run
   - D) Buildpacks create images without writing a Dockerfile
   - E) You must create your own builder first
   - Respuestas: B, C, D

5) A container image is:
   - A) A deployment script
   - B) A VM manifest
   - C) A base runtime to bootstrap apps
   - D) A package with your app and everything it needs to run
   - Respuesta: D

### Preguntas extra (práctica)
6) Main difference between containers and VMs?
   - A) Containers run an entire OS; VMs share host kernel
   - B) Containers share host kernel; VMs run full guest OS
   - C) VMs start faster than containers
   - D) Containers use more memory than VMs
   - Respuesta: B

7) Advantage of multi‑stage builds in Docker?
   - A) Always produce larger images
   - B) Remove need for Dockerfiles
   - C) Create smaller, optimized images by removing build‑time deps
   - D) Allow containers to run multiple kernels
   - Respuesta: C

8) Benefit of Buildpacks vs Dockerfiles?
   - A) Simplifies image creation without Docker expertise
   - B) Full control over system libraries/config
   - C) Guarantees smaller images
   - D) Bypass Cloud Build
   - Respuesta: A

9) Command to create a Docker image from Dockerfile?
   - A) docker start
   - B) docker build
   - C) docker run
   - D) docker image init
   - Respuesta: B

10) Which Google Cloud service runs containers serverlessly?
   - A) Cloud Build
   - B) GKE
   - C) Cloud Run
   - D) App Engine Standard
   - Respuesta: C