## Resources and Access in the Cloud
Este módulo explica cómo se organizan los recursos en Google Cloud y cómo se gestionan los permisos de acceso a ellos a través de IAM.

### Jerarquía de Recursos de Google Cloud
Concepto Clave: Los recursos en Google Cloud están organizados de forma jerárquica. Las políticas (permisos) aplicadas en un nivel superior son heredadas por todos los niveles inferiores.

Niveles (de arriba hacia abajo):
- Nodo de Organización (Organization Node): Es el nodo raíz, representa a toda la empresa. Requiere tener un dominio de Google Workspace o Cloud Identity. Permite la gestión centralizada de políticas.
- Carpetas (Folders): Son un mecanismo de agrupación opcional para proyectos. Sirven para organizar recursos por departamento o equipo y aplicar políticas comunes a varios proyectos.
- Proyecto (Project): Es la unidad fundamental de organización. Todos los recursos (VMs, buckets, etc.) pertenecen a un proyecto. Es el nivel en el que se habilitan las APIs, se gestiona la facturación y se asignan permisos.
- Recursos (Resources): Son los servicios individuales que creas (una instancia de Compute Engine, un bucket de Cloud Storage, etc.).

Identificadores de Proyecto:
- Nombre del Proyecto (Project Name): Elegido por el usuario, no es único y se puede cambiar.
- ID del Proyecto (Project ID): Globalmente único e inmutable (no se puede cambiar una vez creado).
- Número del Proyecto (Project Number): Asignado por Google, globalmente único e inmutable.

### Identity and Access Management (IAM)
¿Qué es IAM?: Es el servicio que define quién (who) puede hacer qué (what) en qué recurso (which resource).

Componentes de una Política de IAM:

Principal (el "quién"): La identidad que solicita acceso. Puede ser:
- Una Cuenta de Google (un usuario humano, ej. usuario@gmail.com).
- Una Cuenta de Servicio (una identidad para una máquina o aplicación, ej. una VM o un servicio de Cloud Run).
- Un Grupo de Google.
- Un Dominio (ej. todos los usuarios de miempresa.com).

Rol (el "qué puede hacer"): Una colección de permisos. No se asignan permisos individuales, sino roles.

Tipos de Roles (de más amplio a más específico):

Roles Básicos (Basic Roles): Muy amplios, aplican a todo el proyecto.
- Propietario (Owner): Control total, puede gestionar usuarios, permisos y facturación.
- Editor (Editor): Puede crear, modificar y eliminar todos los recursos.
- Visualizador (Viewer): Permisos de solo lectura para todos los recursos.

Roles Predefinidos (Predefined Roles): Son roles granulares para un servicio específico. Son la práctica recomendada para seguir el principio de mínimo privilegio. (Ej: roles/compute.instanceAdmin, roles/storage.objectAdmin, roles/run.invoker).

Roles Personalizados (Custom Roles): Permiten crear un rol a medida con una lista específica de permisos, si ningún rol predefinido se ajusta a tus necesidades.

### Cuentas de Servicio (Service Accounts)
- Son una identidad para procesos no humanos (aplicaciones, VMs).
- Se autentican mediante claves criptográficas, no contraseñas.
- Siguen el principio de mínimo privilegio: se les debe otorgar solo los roles necesarios para su tarea.

### Cloud Identity
Es una plataforma para gestionar usuarios y grupos de forma centralizada para una organización, especialmente si no usan Google Workspace. Permite integrar con directorios existentes como Active Directory/LDAP.

### Formas de Interacción con Google Cloud
- Consola de Google Cloud: Interfaz gráfica basada en web (GUI).
- Google Cloud CLI (gcloud) y Cloud Shell: Herramienta de línea de comandos para gestionar recursos. Cloud Shell es una VM con gcloud y otras herramientas preinstaladas, accesible desde el navegador.
- APIs y Librerías Cliente: Para interactuar con los servicios de Google Cloud de forma programática desde tu propio código.
- Google Cloud App: Aplicación móvil para gestión básica de recursos.

### Quiz (práctica)
1) Ordena los siguientes tipos de roles de IAM desde el más amplio (más permisos) hasta el más específico (menos permisos):
   - A) Predefinido, Básico, Personalizado
   - B) Básico, Personalizado, Predefinido
   - C) Básico, Predefinido, Personalizado
   - D) Personalizado, Predefinido, Básico
   - Respuesta: C ✅

2) ¿A qué nivel de la jerarquía de recursos de Google Cloud se habilitan las APIs y se asocia la facturación?
   - A) A nivel de Recurso
   - B) A nivel de Carpeta
   - C) A nivel de Proyecto
   - D) A nivel de Organización
   - Respuesta: C ✅

3) Un administrador otorga el rol de Editor a un usuario a nivel de Carpeta. ¿Qué permisos tendrá ese usuario?
   - A) Permisos de edición solo sobre la configuración de la Carpeta.
   - B) Permisos de edición sobre la Carpeta y todos los Proyectos y Recursos dentro de esa carpeta.
   - C) Solo permisos de lectura sobre los Proyectos dentro de la Carpeta.
   - D) La asignación fallará porque los roles básicos solo se pueden asignar a nivel de Proyecto.
   - Respuesta: B ✅ (Nota: Las políticas se heredan hacia abajo en la jerarquía).

4) ¿Qué identificador de un proyecto de Google Cloud es globalmente único y no se puede cambiar después de su creación?
   - A) El Nombre del Proyecto
   - B) El Número del Proyecto
   - C) El ID del Proyecto
   - D) El ID de la Cuenta de Facturación
   - Respuesta: C ✅ (El ID del Proyecto es el más relevante para comandos y APIs)

5) Necesitas darle permisos a una máquina virtual de Compute Engine para que pueda escribir objetos en un bucket de Cloud Storage. ¿Cuál es la forma más segura y recomendada de hacerlo?
   - A) Crear una clave de API y guardarla en un archivo dentro de la VM.
   - B) Otorgar el rol de Editor a la cuenta de servicio por defecto de la VM.
   - C) Crear una nueva Cuenta de Servicio, otorgarle el rol roles/storage.objectAdmin y asociar esa cuenta de servicio a la VM.
   - D) Hacer el bucket de Cloud Storage público para que cualquiera pueda escribir en él.
   - Respuesta: C ✅

6) ¿Qué herramienta de Google Cloud es una máquina virtual basada en Debian con 5 GB de almacenamiento persistente y el SDK de Cloud preinstalado, accesible directamente desde el navegador?
   - A) La Consola de Google Cloud
   - B) La App Móvil de Google Cloud
   - C) Compute Engine
   - D) Cloud Shell
   - Respuesta: D ✅

7) ¿Cuál es la jerarquía correcta de recursos de Google Cloud, de arriba hacia abajo?
   - A) Organización → Proyecto → Carpeta → Recurso
   - B) Organización → Carpeta → Proyecto → Recurso
   - C) Proyecto → Organización → Carpeta → Recurso
   - D) Carpeta → Organización → Proyecto → Recurso
   - Respuesta: B ✅

8) ¿Qué tipo de rol de IAM es la práctica recomendada para seguir el principio de mínimo privilegio?
   - A) Roles Básicos (Basic Roles)
   - B) Roles Predefinidos (Predefined Roles)
   - C) Roles Personalizados (Custom Roles)
   - D) Todos los tipos de roles son igualmente recomendados
   - Respuesta: B ✅

9) ¿Cuál de los siguientes NO es un tipo de principal (identity) válido en IAM?
   - A) Una Cuenta de Google
   - B) Una Cuenta de Servicio
   - C) Un Grupo de Google
   - D) Una Clave de API
   - Respuesta: D ✅

10) ¿Qué servicio de Google Cloud permite gestionar usuarios y grupos de forma centralizada para una organización?
    - A) Cloud IAM
    - B) Cloud Identity
    - C) Google Workspace
    - D) Cloud Directory
    - Respuesta: B ✅

11) ¿Cuál es la diferencia principal entre el Nombre del Proyecto y el ID del Proyecto?
    - A) No hay diferencia, son sinónimos
    - B) El Nombre es único globalmente, el ID no
    - C) El ID es único globalmente e inmutable, el Nombre no es único y se puede cambiar
    - D) El ID se usa solo para facturación
    - Respuesta: C ✅

12) ¿Qué característica define a las Cuentas de Servicio en Google Cloud?
    - A) Son identidades para usuarios humanos
    - B) Se autentican con contraseñas
    - C) Son identidades para procesos no humanos (aplicaciones, VMs)
    - D) Solo pueden tener roles básicos
    - Respuesta: C ✅