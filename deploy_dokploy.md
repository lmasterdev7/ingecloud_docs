# Despliegue de aplicación Ingecloud en Dokploy

## Introducción
El objetivo de este documento, es realizar un despliegue efectivo de la aplicación Ingecloud para una empresa. Se ha estructurado de tal forma que lo pasos se vayan sucediendo de manera ordenada sin saltarse ninguno, a fin que el despliegue sea el correcto.

Por seguridad no se incluyen credenciales de las bases de datos, en su lugar verá "valores por defecto" o "contraseña de ingecon", estos datos los tiene cualquiera de los técnicos de Ingecon Group SAS.

Por cuanto la aplicación Dokploy está en constante actualización, quizás algunas imágenes no sean exactamente igual como aparecen en este documento, pero el líneas generales el funcionamiento es igual.

---
## Procedimiento de despliegue

### Ingreso a Dokploy
1. Ingrese a un navegador web, preferiblemente Google Chrome y digite la siguiente url cp.ingecloud.app a fin de ingresar a la página web orquestadora de los despliegues de Ingecloud. 
2. Ingrese el *Email* del administrador y el *Password*, luego presione el botón *Login*.
![Logo](img/a-inicio-sesion.png)

### Creación del proyecto
1. Ingrese al menú *Project* desde la barra lateral izquierda.
![Logo](img/c-ingresar-projectos.png)
2. Presione el botón *Create Project*.
3. Llene el formulario con el nombre de la empresa abreviado en *name*, y en *Description* con el puerto de la base de datos que sigue. Siempre debe mirar cual fue el último despliegue y seguir con el consecutivo, **Si ya existe el puerto y no tiene cuidado podría perderse información.** Revise la serie.
![Logo](img/e-agregar-proyecto.png)
4. Luego presione *Create*, automaticamente lo llevara dentro de la empresa nueva, donde desplegará los servicios necesarios.
![Logo](img/f-dentro-proyecto.png)

### Despliegue de Servicios
#### Base de Datos:
Dentro de la empresa que acaba de crear, presione *Create Service*, y del submenú que se abre presione *Database*. Llene la plantilla con estos valores y luego presione *Create*:
* *Select a database*: PostgreSQL
* *Name*: db
* *Select a Server*: db 
* *Database Name*: <nombre_empresa>
* *Database User*: ingecon
* *Database Password*: <contraseña_de_ingecon>
* *Docker image*: postgres:16.9
![Logo](img/g-opciones-servicios.png)

Ingrese a db dándole clic. 
Seleccione la pestaña *Advanced* y diríjase al bloque *Volumes* y modifique el *Volume Name* debe quedar <nombre_empresa>-db-data, luego presione *update*.  

Luego seleccione la pestaña *Backups* y presione *Create Backup*. Llene la plantilla con los siguientes datos y luego presione *Create*:

* *Select Destination:* cloudflare
* *Database:* <nombre_empresa>
* *Schedule:* 0 3 * * *
* *Prefix Destination:* /<nombre_empresa>/db
* *Keep the latest:* 20

Por último diríjase a la pestaña *General*, al bloque *External Credentials* en el campo *External Port(Internet)* y escriba el puerto de la base de datos y luego presione *Save*.

Con esa opción deberá iniciarse la base de datos, sino aparece el círculo verde presione *Deploy*.

#### Redis
Dentro de la empresa que acaba de crear, presione *Create Service*, y del submenú que se abre presione *Database*. Llene la plantilla con estos valores y luego presione *Create*:
* *Select a database*: Redis
* *Name*: redis
* *Select a Server*: db 
* *Database Password*: <contraseña_de_ingecon>
* *Docker image*: redis:7

Ingrese a redis dándole clic. 
Seleccione la pestaña *Advanced* y diríjase al bloque *Volumes* y modifique el *Volume Name* debe quedar <nombre_empresa>-redis-data, luego presione *update*.

Por último diríjase a la pestaña *General*, al bloque *External Credentials* en el campo *External Port(Internet)* y escriba el puerto de la base de datos y luego presione *Save*.

Con esa opción deberá iniciarse la base de datos, sino aparece el círculo verde presione *Deploy*. El puerto de redis es el mismo de la db pero no con 100## sino 200##.

#### App
Dentro de la empresa que acaba de crear, presione *Create Service*, y del submenú que se abre presione *Aplication*. Llene la plantilla con estos valores y luego presione *Create*:
* *Name*: app
* *Select a Server*: Dokploy

Ingrese a la app dándole clic. En la pestaña *General* en el bloque *Provider* digite el formulario y luego presione *Save*:
* *Github Account*: dokploy-ingeconcr-github
* *Repositorio*: ingecon-cloud
* *Branch*: main 
* *Build Path*: /
* *Trigger Type*: On Tag

Luego llene el formulario *Build Type* con los siguientes datos y luego presione *Save*:
* *Build Type*: Dockerfile
* *Docker File*: Dockerfile
* *Docker Context path*: ./

Diríjase a la pestaña *Environment* y pegue el siguiente código, recuerde modificar el puerto de la base de datos de Postgres y Redis y el nombre de empresa y luego presionar el botón *Save*:
~~~bash
# Nombre del archivo principal de la aplicación Flask 
FLASK_APP=factory:create_app

# Clave secreta para manejar sesiones y cookies de manera, y de la API
SECRET_KEY='9MqiO5Lp2:4g);>wNbwl.H@JD+jx4+cb'
API_NUBE_TOKEN='DE.+Zr%(YReSS+;}MdEUsYm6'

# Tipo de motor de base de datos (sqlserver o postgresql), DB_TYPE=sqlserver
DB_TYPE=postgresql
POSTGRESQL_URL=postgresql+psycopg2://ingecon:Biometria8411*@10.10.10.3:<puerto_base_datos>/<nombre_empresa>

# configuración de correo
MAIL_SERVER=mail.ingecongroup.com
MAIL_PORT=465
MAIL_USE_SSL=True
MAIL_USERNAME=noreplytest@ingecongroup.com
MAIL_PASSWORD=)_qBz5J8D$YF9{As
MAIL_DEFAULT_SENDER_NAME=Notificacion IngeCloud
MAIL_DEFAULT_SENDER_EMAIL=noreplytest@ingecongroup.com

# Redis / Celery
CELERY_BROKER_URL=redis://default:Biometria8411*@10.10.10.3:<puerto_de_redis>/0
CELERY_RESULT_BACKEND=redis://default:Biometria8411*@10.10.10.3:<puerto_de_redis>/1
~~~


Vaya a la pestaña *Domains* y agregue estos dos dominios usando el botón *Add Domain* y luego *Create*:
	
<u>Dominio 1</u>:
* *Host:* <nombre_empresa>.ingecloud.app
* *Path:* /
* *Internal Path:* /
* *Container Port:* 5000
* *HTTPS:* True
* *Certificate Provider:* Let's Encrypt

<u>Dominio 2</u>:
* *Host:* <nombre_empresa>.ingecon.site
* *Path:* /
* *Internal Path:* /
* *Container Port:* 5000
* *HTTPS:* True
* *Certificate Provider:* Let's Encrypt

Continúe en la pestaña *Volume Backups* y añada un *Add Volume Backup*, llene el formulario con estos valores y luego presione *Create Volume Backup*:

* *Task Name:* <nombre_empresa>-uploads
* *Schedule:* 0 3 * * *
* *Destination:* cloudflare
* *Volume Name:* <nombre_empresa>-uploads
* *Backup Prefix:* /<nombre_empresa>/volume
* *Keep Latest Backups:* 10

Por último diríjase a la pestaña Advanced al bloque Volumes y añada dos volúmenes con estos datos usando el botón *Add Volume* y luego *Create*:

<u>Volumen 1</u>:
* *Select the Mount Type:* Volume Mount
* *Volume Name:* <nombre_empresa>-uploads
* *Mount Path:* /app/static/uploads

<u>Volumen 2</u>:
* *Select the Mount Type:* Volume Mount
* *Volume Name:* <nombre_empresa>-migrations
* *Mount Path:* /app/migrations

Luego concluya dirigiéndose a la pestaña general y presionando *Deploy* para desplegar la app.

Con estos pasos sino hubo ningún error ya debería tener acceso a la aplicación desde la página web.

