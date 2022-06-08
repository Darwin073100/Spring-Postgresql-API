# Creación De Un API REST Con SprinBoot & PostgreSQL
Creación de un API REST para un supermercado con SpringBoot, framework de java y usando un gestor de bases de datos PostgreSQL.

### Versión de JAVA
- openjdk 11.0.15 2022-04-19
- OpenJDK Runtime Environment (build 11.0.15+10-Ubuntu-0ubuntu0.20.04.1)
- OpenJDK 64-Bit Server VM (build 11.0.15+10-Ubuntu-0ubuntu0.20.04.1, mixed mode, sharing)

### Dependencias Utilizadas
- Spring Web
- Spring Data JPA
- Spring Security
- PostgreSQL Driver
- Springfox Swagger2
- Springfox Swagger UI
- MapStruct
- MapStruct Processor

## Despliegue Del API En Heroku
1. Para realizar el despliegue del Api tendras que instalar el Heroku CLI, como también debes tener una cuenta ya vinculada o crear una.
   [Install CLI of Heroku](https://devcenter.heroku.com/articles/heroku-clihttp:// "Install CLI of Heroku")

2. Despues de haber instalado el CLI vamos a loguearnos para que nos de permisos de acceder al host.
   $`heroku login`

3. Despues de la autentificación vamos a crear el proyecto.
   $`heroku create projectName`

4. Agregar el complemento respecto al motor de base de datos que vamos a utilizar, en este caso es **PostgrSQL**.
   $`heroku addons:create heroku-postgresq`

5. Visualizar as configuraciones para ver los datos que llevaremos a pgAdmin y crear nustras tablas y registros.
   $`heroku config`
   ***Salida:***
   === platzimarketedwin Config Vars
   DATABASE_URL: postgres://vzwngwugfdrlgm:a1d260f2ucnstdjgfkjsgfnkfbhjgbdf688702d29861b190c92123b9a1db1d31ca0e22d74@ec2-32-70-10-940.compute-1.amazonaws.com:5432/d84cohn9u0smhv

   Como vemos nos manda una cadena donde vienen los siguientes como, usuario, contraseña, host, puerto y la BD.
    - ***USER:*** vzwngwugfdrlgm
    - ***PASSWORD:*** a1d260f2ucnstdjgfkjsgfnkfbhjgbdf688702d29861b190c92123b9a1db1d31ca0e22d74
    - ***HOST NAME:*** ec2-32-70-10-940.compute-6.amazonaws.com
    - ***PORT:*** 5432
    - ***DATABASE:*** d84cohn9u0smhv

   Con estos datos deberiamos crear una nueva conexión, buscar nuestra BD en el browser de pgAdmin y crear nustras entidades y sus registros y de mas.

6. Nos vamos a nuestro proyecto, al archivo **application.properties** y ponemos que perfil vamos a usar en este caso es el de **pdn**, despues en el archivo **application-pdn.properties** pondremos lo siguiente:

        server.port=${PORT}
    	spring.datasource.url=${SPRING_DATASOURCE_URL}
    	spring.datasource.username=${SPRING_DATASOURCE_USERNAME}
    	spring.datasource.password=${SPRING_DATASOURCE_PASSWORD}
7. Vamos a crear un archivo **system.properties** en la raiz del proyecto, escribiremos la siguiente linea de codigo para decirle a heroku la version del OpenJdk que ustilizamos.
   `java.runtime.version=11`

8. Crearemos otro archivo sin extencion llamado **Procfile** igualmente en la raiz del proyecto, donde ira la ruta del archivo **.jar** que tiene la aplicación auto contenida, dentro ira lo siguiente:
   `web: java -jar build/libs/platzi-market-1.0.jar`

9. Una vez ya tengamos nuestra base de datos con sus respectivas tablas, pasaremos a desplegar la aplicación de Spring.

***Importante:*** Debes tener el proyecto en el repositorio de Github con la rama master actualizada y con las configuraciones listas, para que keroku obtenga el codigo desde ahí, si ya tenemos eso en la consola nos posicionamos en la raiz del proyecto y ejecutamos lo siguiente.
$`git push heroku master`

