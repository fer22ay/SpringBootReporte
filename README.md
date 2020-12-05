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
