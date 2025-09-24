## Desarrollar Apps Serverless Firebase
Firebase es una plataforma de Backend-como-un-Servicio (BaaS) que proporciona componentes de backend ya construidos para desarrollo rápido de aplicaciones web y móviles.

### ¿Qué es Firebase y por qué es diferente?
Piensa en Cloud Run/GKE como comprar ladrillos y cemento para construir una casa (te da total control y flexibilidad). Firebase es como comprar una casa prefabricada (es mucho más rápido para empezar y ya tiene todo integrado, pero sigues sus reglas).

Definición Clave: Firebase es una plataforma de Backend-como-un-Servicio (BaaS). Proporciona componentes de backend ya construidos (bases de datos, autenticación, etc.) que puedes llamar directamente desde tu aplicación cliente (una web en JavaScript, una app de Android/iOS).

Enfoque: Está diseñado para un desarrollo muy rápido, especialmente para apps web y móviles.

### Firestore (El corazón de los datos)
Este es uno de los temas más importantes.

¿Qué es?: Es la base de datos NoSQL principal de Firebase. Sus características clave son:

Características clave:
- Basada en documentos: Los datos se guardan en documentos (similares a un JSON), que se agrupan en colecciones. La estructura es: Colección -> Documento -> Colección -> Documento...
- En tiempo real: Esta es su "magia". Los clientes (tu app web o móvil) pueden "suscribirse" a una consulta. Cuando los datos cambian en la base de datos, se actualizan automáticamente en la app del usuario sin que tenga que recargar la página.
- Escalado automático: Al ser serverless, no te preocupas por la infraestructura.

Diferencia con Datastore: Firestore es la evolución de Datastore. Para el examen, considera a Firestore como la opción moderna y preferida. Ofrece mejores capacidades de consulta y un modelo de consistencia más fuerte.

### Firebase Security Rules (¡La seguridad es crítica!)
Este es probablemente el concepto más nuevo y específico de Firebase que debes aprender.

¿Qué son?: Son la principal forma de proteger tu base de datos Firestore y tu Cloud Storage en Firebase. NO son reglas de IAM. Viven y se configuran en la consola de Firebase.

¿Cómo funcionan?: Definen en un formato similar a JavaScript quién puede leer, escribir, actualizar o borrar datos en ciertas rutas de tu base de datos.

Ejemplo conceptual:
```javascript
// Permite que un usuario lea su propio perfil, pero no el de los demás.
match /users/{userId} {
  allow read: if request.auth.uid == userId;
}
```

Integración con Autenticación: Las reglas de seguridad casi siempre dependen de Firebase Authentication para saber quién es el usuario (request.auth.uid).

### Otros Servicios Clave de Firebase
Aunque no se mencionen explícitamente, los labs seguramente los usan y son fundamentales.

Firebase Authentication: Servicio para gestionar el login de usuarios (con Google, email/contraseña, Facebook, etc.). Es el que provee la identidad para que las Security Rules funcionen.

Cloud Functions for Firebase: Es el código de backend sin servidor de Firebase. Son funciones que se ejecutan en respuesta a eventos.

Tipos de Triggers (disparadores):
- Un nuevo usuario se registra en Authentication.
- Se crea o actualiza un documento en Firestore.
- Se sube un archivo a Cloud Storage.
- Una petición HTTPS directa (creando una mini-API).

Firebase Hosting: Servicio para desplegar y alojar aplicaciones web estáticas (HTML, CSS, JS) y dinámicas (frontends de frameworks como React, Angular, Vue). Incluye CDN global de forma automática.

### En Resumen para el Examen
Aunque los módulos anteriores te dieron una base sólida en "serverless", Firebase es un enfoque diferente y más "empaquetado".

Comparaciones clave:
- Firebase vs. Cloud Run: Firebase es un BaaS (ideal para frontends y móvil, desarrollo rápido), Cloud Run es un CaaS (Containers-as-a-Service) más flexible (para cualquier backend en un contenedor).
- Seguridad: En Firebase, la primera línea de defensa para los datos son las Firebase Security Rules, no IAM.
- Base de Datos: La opción principal es Firestore, que es NoSQL y en tiempo real.
- Backend Lógico: Se implementa con Cloud Functions for Firebase, que se activan por eventos.

### Quiz (práctica)
1) ¿Qué tipo de plataforma es Firebase?
   - A) Una plataforma de Container-as-a-Service (CaaS)
   - B) Una plataforma de Backend-as-a-Service (BaaS)
   - C) Una plataforma de Infrastructure-as-a-Service (IaaS)
   - D) Una plataforma de Software-as-a-Service (SaaS)
   - Respuesta: B ✅

2) ¿Cuál es la principal diferencia entre Firestore y Datastore?
   - A) Firestore es más antiguo que Datastore
   - B) Firestore es la evolución de Datastore con mejores capacidades de consulta
   - C) Ambos son exactamente iguales
   - D) Datastore es más moderno que Firestore
   - Respuesta: B ✅

3) ¿Qué característica hace que Firestore sea especialmente útil para aplicaciones en tiempo real?
   - A) Su capacidad de almacenar datos en formato JSON
   - B) Su capacidad de escalado automático
   - C) La capacidad de los clientes de "suscribirse" a consultas y recibir actualizaciones automáticas
   - D) Su integración con Firebase Authentication
   - Respuesta: C ✅

4) ¿Cuál es la principal forma de proteger datos en Firebase?
   - A) Reglas de IAM de Google Cloud
   - B) Firebase Security Rules
   - C) Certificados SSL/TLS
   - D) Encriptación de datos en reposo
   - Respuesta: B ✅

5) ¿Qué servicio de Firebase se utiliza para gestionar el login de usuarios?
   - A) Firebase Security Rules
   - B) Firebase Authentication
   - C) Firebase Hosting
   - D) Cloud Functions for Firebase
   - Respuesta: B ✅

6) ¿Cuál de los siguientes NO es un trigger típico para Cloud Functions for Firebase?
   - A) Un nuevo usuario se registra en Authentication
   - B) Se crea un documento en Firestore
   - C) Se sube un archivo a Cloud Storage
   - D) Se crea una nueva VM en Compute Engine
   - Respuesta: D ✅

7) ¿Qué servicio de Firebase se utiliza para desplegar aplicaciones web estáticas y dinámicas?
   - A) Firebase Authentication
   - B) Firebase Hosting
   - C) Cloud Functions for Firebase
   - D) Firebase Security Rules
   - Respuesta: B ✅

8) En Firebase Security Rules, ¿qué variable se utiliza para identificar al usuario autenticado?
   - A) request.user.id
   - B) request.auth.uid
   - C) user.uid
   - D) auth.user.id
   - Respuesta: B ✅