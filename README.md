# RRHH SOA · Órbita

Aplicación de recursos humanos con API Gateway y servicios de empleados, nómina y reclutamiento. Incluye una interfaz web responsive en español, sin dependencias de frontend ni recursos externos.

## Iniciar

Con Docker Desktop en ejecución, desde esta carpeta:

```bash
docker compose up -d --build
```

Abre **http://localhost:3000**. Acceso de laboratorio: usuario `admin` o `rrhh`, contraseña `1234`.

La interfaz permite:

- Consultar el resumen del equipo, departamentos, vacantes abiertas y candidaturas.
- Buscar, registrar y editar empleados, incluido su estado activo/inactivo.
- Calcular y guardar nóminas, y consultar el historial por empleado.
- Crear y editar vacantes; registrar candidatos y actualizar su etapa y notas.

La sesión se conserva en la pestaña mediante `sessionStorage`. Las operaciones utilizan los endpoints existentes del Gateway con autenticación JWT. Los datos mostrados provienen de los servicios; no se insertan registros de demostración.

## Desarrollo de la interfaz

Archivos: `gateway/public/index.html`, `styles.css` y `app.js`. Express sirve estos recursos desde el Gateway. Después de modificar la interfaz:

```bash
docker compose up -d --build --no-deps gateway
```

Servicios: Gateway (3000), empleados (3001, PostgreSQL), nómina (3002, PostgreSQL) y reclutamiento (3003, MongoDB). Comprueba el estado con `docker compose ps` y los registros con `docker compose logs gateway`.

Para detener sin eliminar los datos:

```bash
docker compose down
```

Los volúmenes conservan las bases de datos. Las credenciales y secretos incluidos corresponden al laboratorio.
