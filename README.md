# SXE-Odoo_Instalacion

---
# Configuración de Odoo con Docker-Compose

Este repositorio contiene una configuración básica para ejecutar Odoo utilizando Docker y Docker-Compose.

## Configuración

La configuración se realiza a través del archivo `docker-compose.yml`. Este archivo define dos servicios: `web` y `mydb`.

El archivo `docker-compose.yml` es un archivo de configuración que permite definir y administrar múltiples contenedores como un solo servicio. En este caso, se utilizan dos servicios: `web` y `mydb`.

## Docker-Compose

```markdown
## Explicación del archivo docker-compose.yml

El archivo `docker-compose.yml` define la configuración de los servicios que se ejecutarán en los contenedores. Aquí está la explicación de cada sección:

### Versión

```yaml
version: '3.1'
```

Esta línea especifica la versión de Docker Compose que se está utilizando. La versión '3.1' es una versión comúnmente utilizada que es compatible con la mayoría de las características de Docker Compose.

### Servicios

```yaml
services:
```

Esta sección define los servicios que se ejecutarán en los contenedores. En este caso, se definen dos servicios: `web` y `mydb`.

#### Servicio web

```yaml
  web:
    image: odoo:16.0
    depends_on:
      - mydb
    ports:
      - "8069:8069"
    environment:
      - HOST=mydb
      - USER=odoo
      - PASSWORD=myodoo
```

El servicio `web` es el contenedor que ejecuta la aplicación Odoo. Aquí está la explicación de cada parte:

- `image: odoo:16.0`: Esta línea especifica la imagen de Docker que se utilizará para este servicio. En este caso, se utiliza la imagen `odoo:16.0`.

- `depends_on: - mydb`: Esta línea indica que el servicio `web` depende del servicio `mydb`. Esto significa que Docker Compose se asegurará de que el servicio `mydb` esté en funcionamiento antes de iniciar el servicio `web`.

- `ports: - "8069:8069"`: Esta línea mapea el puerto 8069 del contenedor al puerto 8069 de la máquina host. Esto permite acceder a la aplicación Odoo en el puerto 8069 de la máquina host.

- `environment:`: Esta sección define las variables de entorno que se pasarán al contenedor. Estas variables se utilizan para configurar la conexión a la base de datos.


#### Servicio mydb

```yaml
  mydb:
    image: postgres:15
    ports:
      - "5432:5432"
    environment:
      - POSTGRES_DB=postgres
      - POSTGRES_PASSWORD=myodoo
      - POSTGRES_USER=odoo
```

El servicio `mydb` es el contenedor que ejecuta la base de datos PostgreSQL. Aquí está la explicación de cada parte:

- `image: postgres:15`: Esta línea especifica la imagen de Docker que se utilizará para este servicio. En este caso, se utiliza la imagen `postgres:15`.

- `ports: - "5432:5432"`: Esta línea mapea el puerto 5432 del contenedor al puerto 5432 de la máquina host. Esto permite acceder a la base de datos PostgreSQL en el puerto 5432 de la máquina host.

- `environment:`: Esta sección define las variables de entorno que se pasarán al contenedor. Estas variables se utilizan para configurar la base de datos PostgreSQL.

Este servicio utiliza la imagen `odoo:16.0` y depende del servicio `mydb`. Se expone el puerto 8069 y se configura con las variables de entorno necesarias para conectarse a la base de datos.


Este servicio utiliza la imagen `postgres:15` y expone el puerto 5432. Se configura con las variables de entorno necesarias para crear una base de datos de Postgres.
```

Cada servicio tiene su propia configuración, que incluye la imagen que se utilizará, los puertos que se expondrán, las dependencias entre servicios y las variables de entorno.
## Uso

Para lanzar los contenedores, ejecuta el siguiente comando en la terminal:

```bash
docker-compose up
```

## Enlazar PyCharm con Docker y la base de datos

Para enlazar PyCharm con Docker, necesitas configurar Docker como tu intérprete de Python en PyCharm. Para hacer esto, ve a `File > Settings > Project > Python Interpreter` y selecciona Docker.

Para enlazar PyCharm con la base de datos, puedes usar la herramienta Database de PyCharm. Ve a `View > Tool Windows > Database`. Haz clic en el signo más y selecciona `Data Source > PostgreSQL`. Luego, introduce la información de tu base de datos.

## Solución de problemas

Si el puerto 5432 está ocupado en tu máquina local, puedes cambiar el puerto en el archivo `docker-compose.yml`. Por ejemplo, puedes cambiar la línea `- "5432:5432"` a `- "5433:5432"` para exponer el puerto 5432 del contenedor como el puerto 5433 en tu máquina local.

## Capturas de pantalla

(Por favor, añade aquí tus capturas de pantalla)
