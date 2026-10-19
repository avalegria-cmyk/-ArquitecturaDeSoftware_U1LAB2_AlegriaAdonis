# RRHH SOA

## Entorno Docker

La práctica usa Node.js 22 (cumple el requisito de Node.js 18 o superior), dos bases PostgreSQL 15 y MongoDB 7. Docker instala las dependencias dentro de cada imagen; no hace falta instalar Node.js ni las bases de datos en el equipo.

- Gateway: Express, Axios, dotenv, JWT, express-rate-limit, Winston y http-proxy-middleware.
- Empleados y nómina: dependencias comunes más Sequelize, pg y pg-hstore.
- Reclutamiento: dependencias comunes más Mongoose.

Desde esta carpeta, validar y construir las imágenes:

```sh
docker compose config --quiet
docker compose build
```

Estado actual: estructura y dependencias. Todavía falta implementar `src/index.js` en el gateway y en cada servicio. `docker compose up` podrá arrancar las aplicaciones cuando existan esos archivos.

Para iniciar solo las bases de datos:

```sh
docker compose up -d postgres_emp postgres_nom mongo
```

Una vez implementadas las aplicaciones:

```sh
docker compose up --build
docker compose down
```

El gateway publica el puerto 3000. Los servicios y las bases se comunican dentro de la red de Docker mediante sus nombres. Los datos se conservan en volúmenes. Las credenciales incluidas son exclusivamente para esta práctica local; JWT_SECRET se puede definir en el entorno o en un archivo .env de la raíz.
