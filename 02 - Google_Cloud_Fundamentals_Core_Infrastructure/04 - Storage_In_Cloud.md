## Storage in the Cloud
Este módulo cubre las cinco opciones principales de almacenamiento en Google Cloud, diseñadas para diferentes tipos de datos y casos de uso.

### Cloud Storage: Almacenamiento de Objetos
¿Qué es?: Es el servicio de almacenamiento de objetos de Google Cloud. No es un sistema de archivos tradicional, sino que gestiona datos como "objetos" inmutables.

Caso de uso principal: Almacenar datos no estructurados o "blobs" (Binary Large Objects) como imágenes, videos, copias de seguridad y archivos de gran tamaño.

Estructura: Los objetos se organizan en buckets. Cada bucket debe tener un nombre globalmente único y estar ubicado en una región, multiregión o doble región.

Inmutabilidad y Versionado: Los objetos son inmutables. Al modificar un objeto, se crea una nueva versión. Se puede habilitar el versionado (versioning) en un bucket para conservar un historial de cambios y poder restaurar versiones anteriores.

### Clases de Almacenamiento (¡muy importante!)
- Standard: Para datos de acceso frecuente ("calientes"). Mayor costo de almacenamiento, menor costo de acceso.
- Nearline: Para datos de acceso infrecuente (aprox. 1 vez al mes).
- Coldline: Para datos de acceso muy infrecuente (aprox. 1 vez cada 90 días).
- Archive: Para archivo y recuperación ante desastres (acceso menos de 1 vez al año). Menor costo de almacenamiento, mayor costo de acceso.

### Gestión de Costos en Cloud Storage
Políticas de Ciclo de Vida (Lifecycle Policies): Reglas automáticas para gestionar el costo, como "mover un objeto a Coldline después de 90 días sin acceso" o "eliminar objetos con más de 1 año de antigüedad".

Autoclass: Una función a nivel de bucket que mueve automáticamente los objetos entre clases de almacenamiento según sus patrones de acceso, simplificando la optimización de costos.

### Transferencia de Datos
- Online: A través de gcloud storage o la consola.
- Storage Transfer Service: Para transferir grandes volúmenes de datos desde otras nubes o fuentes online.
- Transfer Appliance: Un dispositivo físico que se envía para cargar petabytes de datos offline.

### Bases de Datos Relacionales (SQL)
Cloud SQL:
- ¿Qué es?: Es un servicio totalmente gestionado para bases de datos relacionales (MySQL, PostgreSQL, SQL Server).
- Caso de uso: Ideal para aplicaciones web tradicionales, sistemas OLTP (Procesamiento de Transacciones en Línea) y cualquier carga de trabajo que requiera una base de datos SQL estándar.
- Escalabilidad: Escala verticalmente (más CPU/RAM/almacenamiento en una sola instancia). Puede llegar hasta 64 TB.

Spanner:
- ¿Qué es?: Es una base de datos relacional, globalmente distribuida, con consistencia fuerte y que habla SQL. Es "lo mejor de SQL y NoSQL".
- Caso de uso: Para aplicaciones de escala global que necesitan consistencia transaccional y alta disponibilidad.
- Escalabilidad: Escala horizontalmente (añadiendo más nodos) y puede manejar petabytes de datos. Es la opción relacional de mayor escala.

### Bases de Datos No Relacionales (NoSQL)
Firestore:
- ¿Qué es?: Una base de datos de documentos NoSQL, flexible y escalable.
- Caso de uso: Diseñada para el desarrollo de aplicaciones web y móviles. Su característica principal son las actualizaciones en tiempo real y el soporte offline.
- Estructura: Colecciones -> Documentos -> Datos.

Bigtable:
- ¿Qué es?: Una base de datos NoSQL de columna ancha, de alto rendimiento y diseñada para cargas de trabajo masivas.
- Caso de uso: Para grandes volúmenes de datos analíticos u operacionales con altas tasas de lectura/escritura, como IoT, series temporales o datos de AdTech. No soporta consultas SQL ni transacciones multi-fila complejas.

### Tabla Comparativa Rápida
| Servicio | Tipo | Escala | Caso de Uso Principal |
|----------|------|--------|----------------------|
| Cloud Storage | Objeto | Petabytes | Archivos grandes, backups, contenido estático |
| Cloud SQL | Relacional (SQL) | Vertical (hasta 64 TB) | Aplicaciones web estándar, OLTP |
| Spanner | Relacional (SQL) | Horizontal (Petabytes) | OLTP a escala global, consistencia fuerte |
| Firestore | Documento (NoSQL) | Horizontal (Terabytes) | Apps web y móviles, datos en tiempo real |
| Bigtable | Columna Ancha (NoSQL) | Horizontal (Petabytes) | Big Data, IoT, series temporales, analítica |

### Quiz (práctica)
1) Tu aplicación necesita almacenar facturas en PDF, que se acceden con poca frecuencia pero deben estar disponibles rápidamente cuando se solicitan. Quieres optimizar los costos. ¿Qué clase de Cloud Storage es la más adecuada?
   - A) Standard
   - B) Nearline
   - C) Archive
   - D) Persistent Disk
   - Respuesta: B ✅

2) Necesitas una base de datos relacional con soporte completo para SQL y transacciones ACID para una aplicación de comercio electrónico global que debe escalar horizontalmente para manejar millones de usuarios. ¿Qué servicio deberías elegir?
   - A) Cloud SQL
   - B) Firestore
   - C) Bigtable
   - D) Spanner
   - Respuesta: D ✅

3) ¿Cuál de las siguientes es una característica clave de Firestore, especialmente útil para aplicaciones móviles?
   - A) Soporte completo para consultas SQL y JOINS.
   - B) Almacenamiento en formato de columna ancha.
   - C) Sincronización de datos en tiempo real y soporte para consultas sin conexión.
   - D) El costo de almacenamiento más bajo de todos los servicios de Google Cloud.
   - Respuesta: C ✅

4) ¿Qué servicio de Google Cloud está diseñado específicamente para manejar cargas de trabajo de Big Data con altas tasas de lectura y escritura, como datos de sensores de IoT o análisis en tiempo real?
   - A) Cloud SQL
   - B) BigQuery
   - C) Bigtable
   - D) Cloud Storage
   - Respuesta: C ✅

5) ¿Cuál es el propósito de una Política de Ciclo de Vida (Lifecycle Policy) en un bucket de Cloud Storage?
   - A) Controlar quién puede acceder a los objetos del bucket.
   - B) Mover o eliminar objetos automáticamente según reglas definidas (como su antigüedad) para gestionar costos.
   - C) Habilitar el versionado de objetos para prevenir la sobreescritura accidental.
   - D) Transferir datos desde otros proveedores de nube al bucket.
   - Respuesta: B ✅

6) ¿Cuál es la principal diferencia de escalabilidad entre Cloud SQL y Spanner?
   - A) Cloud SQL escala horizontalmente, mientras que Spanner escala verticalmente.
   - B) Cloud SQL es un servicio global, mientras que Spanner es regional.
   - C) Cloud SQL escala verticalmente, mientras que Spanner escala horizontalmente.
   - D) No hay diferencia, ambos escalan de la misma manera.
   - Respuesta: C ✅

7) ¿Qué característica de Cloud Storage permite conservar un historial de cambios y restaurar versiones anteriores de los objetos?
   - A) Lifecycle Policies
   - B) Versioning
   - C) Autoclass
   - D) Transfer Appliance
   - Respuesta: B ✅

8) ¿Cuál es la clase de almacenamiento de Cloud Storage con el menor costo de almacenamiento pero mayor costo de acceso?
   - A) Standard
   - B) Nearline
   - C) Coldline
   - D) Archive
   - Respuesta: D ✅

9) ¿Qué servicio de Google Cloud se utiliza para transferir petabytes de datos offline usando un dispositivo físico?
   - A) Storage Transfer Service
   - B) Transfer Appliance
   - C) Cloud VPN
   - D) Cloud Interconnect
   - Respuesta: B ✅

10) ¿Cuál es la estructura de datos en Firestore?
    - A) Tablas -> Filas -> Columnas
    - B) Buckets -> Objetos -> Metadatos
    - C) Colecciones -> Documentos -> Datos
    - D) Clusters -> Nodos -> Datos
    - Respuesta: C ✅

11) ¿Qué función de Cloud Storage mueve automáticamente los objetos entre clases de almacenamiento según sus patrones de acceso?
    - A) Lifecycle Policies
    - B) Versioning
    - C) Autoclass
    - D) Transfer Service
    - Respuesta: C ✅

12) ¿Cuál es el límite máximo de escalabilidad vertical de Cloud SQL?
    - A) 16 TB
    - B) 32 TB
    - C) 64 TB
    - D) 128 TB
    - Respuesta: C ✅

13) ¿Qué tipo de datos NO es adecuado para Bigtable?
    - A) Datos de IoT y sensores
    - B) Series temporales
    - C) Datos de AdTech
    - D) Transacciones complejas multi-fila con SQL
    - Respuesta: D ✅

14) ¿Cuál es la principal ventaja de Spanner sobre Cloud SQL para aplicaciones globales?
    - A) Menor costo
    - B) Mayor escalabilidad vertical
    - C) Escalabilidad horizontal y distribución global con consistencia fuerte
    - D) Soporte para más tipos de datos
    - Respuesta: C ✅