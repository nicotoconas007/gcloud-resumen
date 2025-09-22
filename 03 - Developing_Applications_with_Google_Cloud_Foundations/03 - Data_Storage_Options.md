## Módulo 3 – Data Storage Options

### Resumen
Visión general de las opciones de almacenamiento en Google Cloud y cuándo usarlas.

#### Cloud Storage
- Tipo: object storage para datos no estructurados.
- Usos: sitios estáticos, imágenes, videos, backups, archivos grandes.
- Características: alta durabilidad, escalable, hasta 5 TB por objeto, acceso HTTP/HTTPS, clases de almacenamiento.
- No ideal para: datos relacionales ni consultas complejas.

#### Firestore
- Tipo: base de datos NoSQL de documentos (colecciones/documentos).
- Usos: apps web/móviles con datos flexibles, usuarios externos, sync offline y tiempo real.
- Características: escalado automático, listeners en tiempo real, transacciones, seguridad con reglas.
- No ideal para: OLAP y consultas masivas/scan completos.

#### Bigtable
- Tipo: NoSQL key-value/wide-column para grandes volúmenes.
- Usos: analítica/operacional a gran escala, IoT, time series, billones de filas.
- Características: baja latencia (<10 ms), escalado horizontal, compatibilidad HBase API.
- No ideal para: relacional y joins.

#### Cloud SQL
- Tipo: RDBMS gestionado (MySQL, PostgreSQL, SQL Server).
- Usos: OLTP, apps con relaciones y transacciones, migraciones lift-and-shift.
- Características: réplicas, backups, failover, Auth Proxy.
- No ideal para: escalado horizontal masivo global.

#### AlloyDB
- Tipo: PostgreSQL gestionado y optimizado.
- Usos: workloads híbridos (OLTP+analítico), modernización desde PostgreSQL/Oracle.
- Características: hasta 4× en transacciones vs PostgreSQL estándar; hasta 100× en analítico con columnar engine; separación compute/storage.
- No ideal para: apps que no requieran PostgreSQL o con requerimientos mínimos.

#### Cloud Spanner
- Tipo: base de datos relacional con escalado horizontal global.
- Usos: aplicaciones críticas globales que requieren consistencia fuerte y alta disponibilidad.
- Características: consistencia fuerte multi-región, 99.999% SLA, transacciones distribuidas.
- No ideal para: apps pequeñas/medianas con necesidades locales.

#### BigQuery
- Tipo: data warehouse serverless (OLAP).
- Usos: BI, analytics, ML, big data.
- Características: escanea TB en segundos, PB en minutos, sin gestión de infraestructura, SQL estándar.
- No ideal para: OLTP ni lecturas transaccionales en tiempo real.

#### Memorystore (Redis/Memcached)
- Tipo: caché en memoria gestionada.
- Usos: caching, gaming, sesiones, stream processing con baja latencia.
- Características: compatible con Redis/Memcached, IAM/VPC, failover y replicación.
- No ideal para: almacenamiento persistente de largo plazo.

### Comparación rápida
| Servicio      | Tipo                         | Ideal para                              | No ideal para                       |
| ---           | ---                          | ---                                      | ---                                  |
| Cloud Storage | Object                       | Archivos grandes, sitios estáticos       | Datos relacionales, queries          |
| Firestore     | NoSQL documentos             | Apps móviles/web, datos flexibles        | OLAP, big data analytics             |
| Bigtable      | NoSQL key-value/wide-column  | Billones de filas, analíticas, IoT       | Relacional, joins                    |
| Cloud SQL     | Relacional                   | OLTP, migraciones rápidas                | Escalado masivo global               |
| AlloyDB       | Relacional (Postgres opt.)   | OLTP + OLAP híbrido                      | Apps que no requieran Postgres       |
| Spanner       | Relacional global            | OLTP crítico con consistencia fuerte     | Apps pequeñas/medianas               |
| BigQuery      | Data warehouse               | OLAP, BI, ML                             | OLTP, lecturas transaccionales       |
| Memorystore   | In-memory cache              | Cache, baja latencia                     | Almacenamiento persistente           |

### Quiz (oficial)
1) You have a very large database used for complex BI queries. You want a fully managed solution. Which is ideal?
   - A) Cloud SQL
   - B) BigQuery
   - C) Firestore
   - D) Cloud Bigtable
   - Respuesta: B) BigQuery

2) A restaurant needs a static website (menu, hours, map). Best solution?
   - A) Cloud Bigtable
   - B) Compute Engine web server
   - C) Cloud Storage bucket
   - D) Firestore
   - Respuesta: C) Cloud Storage bucket

3) Banking app with global users; deposits must reflect immediately. Ideal storage?
   - A) Firestore
   - B) Cloud SQL
   - C) Bigtable
   - D) Cloud Spanner
   - Respuesta: D) Cloud Spanner

### Preguntas extra (práctica estilo certificación)
4) Which database for mobile apps requiring offline sync and real-time updates?
   - A) Cloud SQL
   - B) BigQuery
   - C) Firestore
   - D) Spanner
   - Respuesta: C) Firestore

5) Which service offers a columnar storage engine for analytics on PostgreSQL workloads?
   - A) Cloud SQL
   - B) AlloyDB
   - C) Firestore
   - D) BigQuery
   - Respuesta: B) AlloyDB

6) Which service for IoT sensor data at scale (billions of rows, low-latency lookups)?
   - A) Firestore
   - B) Bigtable
   - C) Cloud SQL
   - D) Spanner
   - Respuesta: B) Bigtable

7) Cache session data for a gaming app with millisecond latency. Choose:
   - A) BigQuery
   - B) Memorystore
   - C) Cloud SQL
   - D) Cloud Storage
   - Respuesta: B) Memorystore