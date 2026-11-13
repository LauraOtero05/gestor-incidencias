# Despliegue de una aplicación web con Docker Compose

Creación de un contenedor de docker con docker compose y conexión entre el frontend, backend y database mediante contenedores

**1. ¿Por qué el frontend no necesita conectarse a PostgreSQL?**

Porque el frontend se comunica con el backend, que es el encargado de gestionar las peticiones y comunicarse con la base de datos. 

**2. ¿Por qué el backend pertenece a dos redes?**

Porque necesita comunicarse tanto con el frontend como con la base de datos. Al estar conectado a las dos redes, puede recibir las peticiones del frontend y consultar o guardar información en PostgreSQL.

**3. ¿Qué servicio necesita publicar un puerto en el anfitrión?**

El frontend, porque es el servicio al que necesitamos acceder desde nuestro navegador, que está fuera de los contenedores.

**4. ¿Por qué publicar PostgreSQL hacia fuera no es la solución adecuada para un fallo de comunicación interno?**

Porque no necesitamos acceder directamente a la base de datos desde nuestro ordenador. PostgreSQL se comunica con el backend mediante una red interna de Docker. Si existe un problema de comunicación entre ellos, hay que revisar esa conexión interna y no publicar el puerto hacia fuera.

**5. ¿Qué ventaja ofrece Docker Compose respecto a ejecutar los tres contenedores manualmente?**

Permite gestionar los tres contenedores desde un mismo archivo de configuración, haciendo que sea mucho más fácil iniciar, detener y configurar todos los servicios a la vez, sin tener que ejecutarlos uno por uno.

**6. ¿Por qué hemos dividido la arquitectura en dos redes?**

Porque no todos los contenedores necesitan comunicarse entre sí. El frontend solo necesita comunicarse con el backend, mientras que el backend necesita comunicarse con la base de datos. Por eso hemos creado dos redes para separar las conexiones y mejorar la organización y la seguridad.

**7. ¿Por qué el backend utiliza `db` como dirección de PostgreSQL?**

Porque `db` es el nombre que le hemos dado al servicio de PostgreSQL en el archivo de Docker Compose. Docker permite que los contenedores se encuentren entre sí utilizando el nombre del servicio dentro de la misma red.

**8. ¿Qué diferencia existe entre detener un proyecto y eliminar sus volúmenes?**

Al detener el proyecto, los contenedores dejan de ejecutarse, pero los datos almacenados en los volúmenes se mantienen. En cambio, si eliminamos los volúmenes, perdemos la información que estaba guardada en ellos.

**9. ¿Qué consecuencias tendría para la empresa perder el volumen de PostgreSQL?**

La empresa perdería todos los datos almacenados en la base de datos. Esto podría provocar problemas importantes en el funcionamiento de la aplicación y pérdidas de información que podrían ser difíciles de recuperar.
