# <span style="color:#3e86fe"> Política | Seguridad de la Información </span> 

Santiago de Cali, 1 de enero del 2026 

## Propósito 

Establecer el marco integral de gestión de seguridad de la información de Ingecon Group SAS para proteger los activos de información gestionados a través de la plataforma Ingecloud, garantizando: 
-	Confidencialidad 
-	Integridad 
-	Disponibilidad 
-	Autenticidad 
-	Trazabilidad 
 
## 1. Alcance 

Esta política aplica a: 
-	Todos los empleados y contratistas. 
-	La infraestructura tecnológica que soporta Ingecloud. 
-	Los datos personales y corporativos tratados por la plataforma. 
-	Proveedores tecnológicos vinculados a la operación. 

## 2. Marco Normativo 

Ingecon Group SAS opera conforme a: 
-	Ley 1581 de 2012 (Protección de Datos Personales – Colombia). 
-	Decreto 1377 de 2013. 
-	Principios internacionales de buenas prácticas en seguridad de la información (alineados conceptualmente con ISO 27001). 
 
## 3. Gobierno y Responsabilidades 

### 3.1 Gerencia General 
-	Aprobar la presente política. 
-	Proveer recursos necesarios para su cumplimiento. 
 
### 3.2 Responsable de Tecnología 
-	Implementar y mantener controles técnicos. 
-	Gestionar riesgos tecnológicos. 
-	Supervisar incidentes de seguridad. 

### 3.3 Colaboradores 
-	Cumplir los lineamientos establecidos. 
-	Reportar eventos sospechosos o incidentes. 
 
## 4. Gestión de Riesgos 

La organización identifica, evalúa y trata riesgos que puedan afectar la seguridad de la información mediante: 
-	Evaluación periódica de vulnerabilidades. 
-	Implementación de controles preventivos, de detección y correctivos. 
-	Revisión anual de la postura de seguridad. 

## 5. Seguridad de Infraestructura 

-	Infraestructura desplegada en servidores VPS con recursos dedicados. 
-	Segmentación mediante red privada (VPC). 
-	Bases de datos no expuestas públicamente. 
-	Acceso administrativo exclusivo mediante autenticación SSH basada en llave criptográfica. 
-	Firewall perimetral activo. 
-	Protección contra ataques DDoS. 
-	Cifrado obligatorio HTTPS (TLS). 

## 6. Protección de Datos Personales 

-	Se implementan medidas técnicas y organizativas para: 
-	Garantizar tratamiento conforme a finalidad contractual 
-	Evitar acceso no autorizado 
-	Aplicar control de acceso basado en roles 
-	Mantener política de retención de datos 
-	Prohibir cesión o transferencia no autorizada 

## 7. Gestión de Cambios 

Todo cambio significativo en infraestructura o aplicación debe: 
-	Evaluarse en términos de impacto de seguridad 
-	Documentarse 
-	Validar antes de su despliegue en producción 

## 8. Control de Accesos 

Establecer controles estrictos de autenticación y autorización para proteger los activos tecnológicos y datos personales gestionados por Ingecloud. 

**Principios:** Mínimo privilegio, Necesidad de saber, Segregación de funciones y Trazabilidad de accesos. 

**Autenticación de Usuarios:** Cada usuario posee credenciales individuales e intransferibles. Las contraseñas se almacenan utilizando hashing seguro (bcrypt con salt aleatorio). Se aplican políticas configurables de complejidad y caducidad. Los intentos excesivos de autenticación son limitados mediante controles perimetrales. 

**Autorización y Roles:** La plataforma implementa control granular por módulo: Lectura, Escritura y Sin acceso. Los permisos son asignados por administradores autorizados. 

**Accesos Administrativos:** El acceso root está restringido exclusivamente al responsable de TI. Autenticación SSH solo mediante llave criptográfica. Plataformas críticas protegidas con doble factor de autenticación. Puertos administrativos no expuestos públicamente. 

**Ciclo de Vida de Usuarios:** Creación de cuentas autorizada por el cliente. Modificación basada en cambios de rol. Eliminación inmediata ante desvinculación. 
 
**Registro y Monitoreo:** Se mantienen registros de eventos relevantes que permiten: Auditoría posterior, Investigación de incidentes, Análisis de comportamiento anómalo.
 
## 9. Gestión de vulnerabilidades 

Ingecon Group SAS mantiene una política interna de Gestión de Vulnerabilidades y Gestión de Parches que define los procedimientos para identificar, evaluar y mitigar vulnerabilidades que puedan afectar la plataforma SaaS Ingecloud. 

La política incluye controles como: 

Monitoreo de vulnerabilidades publicadas que afecten el sistema operativo, dependencias de software y componentes de infraestructura. 
-	Aplicación periódica de parches de seguridad del sistema operativo. 
-	Actualización regular de dependencias del software utilizadas por la aplicación. 
-	Evaluación y priorización de vulnerabilidades según su severidad. 
-	Implementación de mitigaciones o actualizaciones cuando se identifican riesgos de seguridad relevantes. 
 
## 10. Gestión de Incidentes de Seguridad 

Definir el proceso formal para detección, análisis, contención, erradicación y recuperación ante incidentes de seguridad. 

Se considera incidente cualquier evento que: Comprometa confidencialidad, integridad o disponibilidad; Genere acceso no autorizado e Interrumpa la operación normal del servicio. 

Estos incidentes se clasifican como: Bajo, Medio, Alto y Crítico. La clasificación determina tiempos de respuesta y escalamiento. 

El proceso de gestión está estructurado de la siguiente manera:  
**Detección:** Alertas automáticas; Monitoreo de infraestructura y Reporte de usuarios. 
**Contención:** Aislamiento de servicios afectados; Revocación de credenciales comprometidas y Bloqueo de tráfico malicioso. 
**Erradicación:** Eliminación de causa raíz y Aplicación de parches o cambios de configuración. 
**Recuperación:** Restauración desde backups verificados; Validación de integridad y Monitoreo reforzado posterior. 

En caso de afectación de datos personales se notificará al cliente correspondiente y se evaluará obligación de reporte a autoridades competentes. Todo incidente generará análisis de causa raíz, revisión de controles e implementación de mejoras preventivas. 

## 11. Backup y Continuidad

Garantizar la resiliencia operativa y continuidad del servicio ante fallos técnicos, incidentes de seguridad o desastres. 

**Estrategia de Respaldo:** Backups diarios de servidores, Backups diarios de bases de datos, Backups adicionales cada 7 horas hacia proveedor alterno y Copias almacenadas en ubicaciones independientes. 

**Pruebas de Restauración:** Se realizan pruebas periódicas de recuperación completa. Se validan tiempos de recuperación y consistencia de datos. Se documentan resultados. 

**Plan de Recuperación ante Desastres** (DRP): En caso de indisponibilidad del proveedor principal -> Activación del plan, Despliegue en proveedor alterno, Restauración de infraestructura, Validación operativa y comunicación a clientes. 

**Objetivos de Recuperación:**  
-	RTO (Recovery Time Objective): 1 a 3 horas. 
-	RPO (Recovery Point Objective): máximo 7 horas. 

**Revisión:** El plan será revisado al menos una vez al año o ante cambios significativos en la infraestructura. 

## 12. Gestión de Riesgos de Proveedores 

Esta política define el marco de gestión de riesgos aplicable a proveedores y terceros que participan en la operación de la plataforma SaaS Ingecloud, con el objetivo de identificar, evaluar y mitigar riesgos de seguridad, disponibilidad y cumplimiento asociados a la cadena de suministro tecnológica.  

La gestión de riesgos de proveedores busca garantizar que los servicios prestados por terceros mantengan niveles adecuados de seguridad y confiabilidad para proteger los datos y operaciones de los clientes. 

**Alcance:** Esta política aplica a todos los proveedores que intervienen en la operación de la plataforma tecnológica, incluyendo: Proveedores de infraestructura Cloud, Proveedores de servicios de seguridad, Proveedores de almacenamiento o backup y Cualquier tercero que procese o almacene datos de clientes. 

**Marco de Gestión de Riesgos:** Ingecon Group SAS implementa un proceso de evaluación de riesgos basado en las siguientes etapas: 

**Identificación de proveedores críticos.** Se identifican proveedores que cumplen funciones esenciales para la operación de la plataforma, tales como: 
-	Infraestructura de servidores 
-	Servicios de red y seguridad 
-	Almacenamiento de datos y copias de seguridad 
 
**Evaluación de seguridad del proveedor.** Antes de utilizar un proveedor tecnológico se revisan aspectos como: 
-	Reputación y trayectoria en la industria 
-	Controles de seguridad implementados 
-	Certificaciones de seguridad (cuando estén disponibles) 
-	Disponibilidad y resiliencia de la infraestructura 
 
**Clasificación de riesgo.** Los proveedores se clasifican según su nivel de impacto en la operación del servicio: 
-	Crítico: proveedores de infraestructura o seguridad 
-	Alto: proveedores que almacenan datos 
-	Medio: proveedores de soporte o herramientas auxiliares 

**Evaluación de proveedores actuales.** La plataforma Ingecloud utiliza proveedores tecnológicos reconocidos en la industria cloud: 

Infraestructura cloud: La infraestructura principal se encuentra alojada en Hetzner, proveedor internacional de servicios de nube que ofrece controles de 	seguridad de red, aislamiento de infraestructura y mecanismos de protección contra amenazas. 

Protección de red y seguridad: La protección perimetral y el filtrado de tráfico se gestionan mediante Cloudflare, incluyendo: 
-	Web Application Firewall (WAF) 
-	Protección contra ataques DDoS 
-	Rate limiting 
-	Proxy inverso seguro 
 
Almacenamiento de copias de seguridad: Los respaldos adicionales de infraestructura y datos se almacenan en servicios cloud externos como *DigitalOcean*, con el objetivo de mantener redundancia y resiliencia ante fallas del proveedor principal. 

**Revisión periódica de proveedores.** Los proveedores tecnológicos son revisados periódicamente considerando: 
-	Estabilidad del servicio 
-	Incidentes de seguridad reportados 
-	Cambios en políticas de seguridad del proveedor 
-	Disponibilidad y continuidad del servicio 
 
En caso de identificarse riesgos relevantes, se evaluarán alternativas tecnológicas o controles adicionales de mitigación. 

**Estrategias de mitigación de riesgos.** Para reducir la dependencia de proveedores individuales, la organización implementa medidas como: 
- 	Copias de seguridad externas en proveedores independientes 
-	Capacidad de restaurar infraestructura en proveedores alternativos 
-	Uso de servicios de seguridad independientes del proveedor de infraestructura 
 
Estas medidas permiten mantener la continuidad del servicio ante incidentes o interrupciones de proveedores. 

**Responsabilidades.** La gestión de riesgos de proveedores es responsabilidad del área de tecnología de Ingecon Group SAS, encargada de: 
-	Evaluar proveedores antes de su uso 
-	Revisar periódicamente su desempeño y seguridad 
-	Implementar controles de mitigación cuando sea necesario 
 
**Revisión de la política** 
Esta política será revisada periódicamente para asegurar que continúe siendo adecuada frente a los riesgos asociados a la cadena de suministro tecnológica. 

## 13. Auditoría y Mejora Continua 
La política será revisada anualmente o ante cambios relevantes en la operación. Se implementarán mejoras continuas conforme a evolución de amenazas o requisitos regulatorios. 

---
 
Representante Legal: **Cesar Augusto Rodriguez**
Firma: Cesar Augusto Rodriguez  
Fecha: 1 de enero del 2026 

Responsable de Tecnología: **Junior Luciano Rivas**

 Firma: **Junior Luciano Rivas** 

 
