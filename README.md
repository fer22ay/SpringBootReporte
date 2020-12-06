# SpringBootReporte
Ejemplo de reporte con Spring Boot via aplicacion Rest


## Docker Conexion MySQL
Version MySQL 8.0
Docker version 19.03.13

### Descarga de imagen de MySQL
Aclaro que esta descarga se hizo desde la terminal de Windows 10 (CMD)

#### Descarga de imagen
`C:\name>docker pull mysql:8.0`

#### Luego corremos el contendor

`C:\name>docker run -d -p 33060:3306 --name mysql-db -e MYSQL_ROOT_PASSWORD=password mysql:8.0`

- -d: Deatached Mode es la forma en que indicamos que corra en background.
- -p: puerto, el contenedor corre en el puerto 3306 pero hacemos un bind para que lo escuchemos en Host el puerto 33060
- -name: para no tener que hacer referencia al hash le asignamos un nombre.
- -e: environment le asignamos la contraseña.


#### Ingreso a shell de mysql para creacion de la base de datos

`C:\name>docker exec -it mysql-db mysql -u root -p`

## Docker Conexion PostgreSQL
Version de PosgreSQL 10.15

#### Descargar Imagen de PosgreSQL 10.15
`C:\name>docker pull postgres:10.15`

#### Inicializar el contenedor de PosgtreSQL
`C:\name>docker run -d --name postgrs -v C:/Users/aambr/postgres-data:/var/lib/postgresql/data -e POSTGRES_PASSWORD=postgres10 -p 5433:5433 postgres:10.15`

- Es necesario especificar el directorio donde estaran las configuraciones de postgres, ya que sino no podra hacer la conexion via localhost.

- Aunque se especifico el puerto en el comando de docker se debe configurar tambien en el archivo postgresql.conf para especificar el puerto.

#### Conexion a shell de postgres
`C:\name>docker exec -it postgres psql -U postgres`

- Esta opcion hasta cierto punto puede ser opcional, ya que podemos utilizar un gestor de base de datos grafico.

#### Creacion de usuario y base datos

`CREATE USER "NAME_USER" WITH PASSWORD 'PASSWORD';`

`ALTER ROLE "NAME_USER WITH LOGIN;`

`ALTER ROLE "NAME_USER" WITH CREATEDB;`

`CREATE DATABASE "NAME_DATABASE" WITH OWNER "NAME_USER";`

#### Comandos necesarios para acceder a la data del esquema

`GRANT ALL PRIVILEGES ON ALL TABLES IN SCHEMA name_schema TO name_user;`

`GRANT USAGE ON SCHEMA name_schema TO name_user;`

#### Conexion desde terminal (CMD)

`C:\name>psql -h localhost -p 5433 -U market`

- Luego nos solicitara el password este por defecto fue el que configuramos al inicializar el contenedor de postgres

## Conexion a spring boot

+ spring.datasource.url=jdbc:postgresql://localhost:5433/NAME_DATABASE
+ spring.datasource.username=NAME_USER
+ spring.datasource.password=PASSWORD_USER
+ spring.jpa.show-sql=true
