## Módulo 4 – Handling Authentication and Authorization

### Resumen
Puntos clave para autenticación y autorización en Google Cloud.

#### IAM (Identity and Access Management) – Autorización
- Define quién (principal) tiene qué acceso (rol) sobre qué recurso.
- Principales: Google Accounts, Service Accounts, Google Groups, dominios de Google Workspace/Cloud Identity.
- Roles: básicos (Owner/Editor/Viewer, poco recomendados), predefinidos (granulares, p.ej. `roles/run.invoker`), y personalizados (custom).
- Condiciones de IAM (IAM Conditions): permiten restringir por atributos (p.ej., horario, IP, recursos específicos) con CEL.
- Jerarquía de recursos: Organización → Carpetas → Proyectos → Recursos. Las políticas se heredan hacia abajo.
- Principio de mínimo privilegio: concede solo permisos necesarios y por el tiempo necesario.

#### Autenticación en Google Cloud
- Autenticación = demostrar identidad (contraseña, clave, token).
- Opciones comunes para apps:
  - API Keys: casos de baja seguridad; evitar para acceso sensible.
  - OAuth 2.0 (cuentas de usuario): acceso delegado con consentimiento y expiración.
  - Service Accounts (workloads): identidad de apps/servicios; recomendado en producción.
- Riesgos de service account keys (claves descargadas): fuga de credenciales, escalamiento de privilegios, ocultamiento de identidad.
- Mitigación: evitar claves persistentes y usar Application Default Credentials (ADC), metadata server, short‑lived tokens.

#### Métodos de autenticación según entorno
- Desarrollo local: `gcloud auth application-default login` para ADC locales.
- Compute Engine / Cloud Run / Cloud Functions: adjuntar un service account al workload; usar metadata server para obtener tokens.
- GKE: usar Workload Identity para mapear ServiceAccounts de Kubernetes a Service Accounts de IAM.
- Multi‑cloud / on‑prem: Workload Identity Federation para evitar descargar claves; emite credenciales de corta duración.
- Último recurso: service account keys con controles estrictos (rotación, restricciones, almacenamiento seguro).

#### Autenticación en nombre de un usuario (OAuth 2.0)
- Flujo: consentimiento del usuario → app obtiene tokens → accede en nombre del usuario.
- Tokens: access token (acceso a APIs), ID token (identidad OIDC), refresh token (renovar acceso).
- Domain‑wide delegation: las service accounts pueden actuar en nombre de usuarios de un dominio (escenarios enterprise controlados).

#### Identity‑Aware Proxy (IAP)
- Capa centralizada de autenticación/autorización a nivel de aplicación.
- Permite acceso seguro sin VPN ni reglas de firewall complejas.
- Encabezados útiles para apps detrás de IAP: `X-Goog-Authenticated-User-Email`, `X-Goog-Authenticated-User-Id`.
- Ideal para apps internas accesibles vía HTTPS.

#### Firebase Authentication e Identity Platform
- Firebase Auth: alta velocidad de integración; soporta password, phone, Google, Apple, GitHub.
- Identity Platform: orientado a enterprise; soporta OIDC/SAML, MFA, multi‑tenant y se integra con IAP.

#### Secret Manager
- Almacén seguro de secretos (API keys, passwords, certificados) con versionado y replicación configurable.
- Integrado con IAM y auditado en Cloud Audit Logs; cifrado automático (opcional Cloud KMS).
- Accesible por consola, CLI o SDKs.

#### Prácticas recomendadas adicionales
- Impersonación de Service Accounts: preferir `gcloud iam service-accounts keys disable` y usar impersonación para emitir credenciales efímeras.
- Metadata server (GCE/GKE/Cloud Run): obtener tokens de acceso/ID sin distribuir claves.
- Rotación y principio de Zero Trust: usar políticas de expiración corta y verificación continua.

Referencia: [Module 4 – Handling Authentication and Authorization](https://storage.googleapis.com/cloud-training/devapps-foundations/en/on-demand/v1.2.0/Module4-HandlingAuthenticationAndAuthorization.pdf)

### Quiz (oficial)
1) Your enterprise has an online expense reporting application. Employees must access it without logging into the corporate VPN. How can you enable this access?
   - A) Give employees read permissions to critical resources in the project
   - B) Use Identity-Aware Proxy to provide application-level access
   - C) Use OAuth 2.0 to access resources on behalf of a user
   - D) Use Firebase Authentication for federated identity
   - Respuesta: B) Use Identity-Aware Proxy to provide application-level access

2) Your photo-sharing application requires user login. You don't want to build a custom auth system storing usernames/passwords. Best way to authenticate users?
   - A) Use OAuth 2.0 to access resources on behalf of a user
   - B) Use Firebase Authentication for federated identity
   - C) Use Identity-Aware Proxy to provide application-level access
   - D) Give employees read permissions to critical resources
   - Respuesta: B) Use Firebase Authentication for federated identity

3) How should you authenticate to Google Cloud APIs from your production application deployed to Cloud Run?
   - A) Use workload identity federation
   - B) Use gcloud auth application-default login
   - C) Use a service account key
   - D) Attach a service account to your application
   - Respuesta: D) Attach a service account to your application

### Preguntas extra (práctica estilo certificación)
4) Which IAM role type should you use if predefined roles are too broad?
   - A) Basic roles
   - B) Predefined roles
   - C) Custom roles
   - D) Service accounts
   - Respuesta: C) Custom roles

5) What is the recommended way to authenticate workloads in GKE?
   - A) API keys
   - B) Service account keys
   - C) Workload Identity
   - D) Cloud Identity domain
   - Respuesta: C) Workload Identity

6) Which service provides auditing for secret access and integrates with Cloud KMS?
   - A) Identity Platform
   - B) Cloud SQL
   - C) Secret Manager
   - D) Firebase Auth
   - Respuesta: C) Secret Manager

7) On‑prem app must call Google Cloud APIs without using service account keys. What should you configure?
   - A) Custom roles
   - B) IAP
   - C) Workload Identity Federation
   - D) OAuth 2.0 user consent
   - Respuesta: C) Workload Identity Federation

8) Which header can your app read when protected by IAP to know the user identity?
   - A) X-Forwarded-For
   - B) Authorization: Basic
   - C) X-Goog-Authenticated-User-Email
   - D) X-Cloud-Trace-Context
   - Respuesta: C) X-Goog-Authenticated-User-Email

9) In Cloud Run, what’s the preferred way to obtain tokens without storing keys?
   - A) Hardcode API keys as env vars
   - B) Use the metadata server to fetch short‑lived tokens
   - C) Download a JSON key and read from disk
   - D) Use Basic Auth headers
   - Respuesta: B) Use the metadata server to fetch short‑lived tokens