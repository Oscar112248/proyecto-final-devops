# Informe del Trabajo Final DevOps

## 1. Datos del grupo

- Grupo: Grupo 3
- Integrantes: Daniel Alquinga, Oscar Maldonado
- Curso: Curso de Profesionalizacion en DevOps

## 2. Objetivos

- Crear una aplicacion web con FastAPI.
- Construir una imagen Docker versionada.
- Publicar la imagen en Docker Hub mediante GitHub Actions.
- Ejecutar el contenedor usando variables de entorno del grupo.
- Verificar el estado del servicio y los endpoints solicitados.

## 3. Estructura del proyecto

```text
proyecto-final-devops
|-- app
|   |-- main.py
|   `-- templates
|       `-- index.html
|-- .github
|   `-- workflows
|       `-- dockerhub.yml
|-- .dockerignore
|-- .gitignore
|-- Dockerfile
|-- INFORME.md
|-- README.md
|-- VERSION
`-- requirements.txt
```

## 4. Configuracion de Git y GitFlow

El proyecto se mantiene en un repositorio Git llamado `proyecto-final-devops`. Para cumplir GitFlow, el repositorio debe contar con las ramas `main` y `develop`, y la version final debe integrarse desde una rama `release`.

Comandos de referencia:

```bash
git branch develop
git checkout -b release/v1.0.0 develop
git checkout main
git merge release/v1.0.0
git tag v1.0.0
```

## 5. Agregacion de contenido e historial de commits

Se agregaron los archivos base de la aplicacion FastAPI, plantilla HTML, dependencias, Dockerfile, archivos de exclusion, workflow de GitHub Actions y documentacion del proyecto.

Comandos de referencia para confirmar cambios:

```bash
git add .
git commit -m "Completa trabajo final DevOps"
```

## 6. Creacion del versionamiento con release

La version de la aplicacion se define como `1.0.0` en el archivo `VERSION` y la imagen Docker se publica con la etiqueta `v1`.

Etiqueta Git recomendada:

```bash
git tag v1.0.0
```

## 7. Publicacion en GitHub

Repositorio GitHub:

```text
https://github.com/<usuario>/proyecto-final-devops
```

Comandos de referencia:

```bash
git remote add origin https://github.com/<usuario>/proyecto-final-devops.git
git push -u origin main
git push origin develop
git push origin --tags
```

## 8. Configuracion de GitHub Actions

El workflow se encuentra en `.github/workflows/dockerhub.yml` y realiza las siguientes acciones:

- Descarga el codigo del repositorio.
- Configura Docker Buildx.
- Inicia sesion en Docker Hub usando secrets.
- Construye y publica la imagen `devops-final-project:v1`.

Secrets requeridos:

- `DOCKERHUB_USERNAME`
- `DOCKERHUB_TOKEN`

## 9. Publicacion en Docker Hub

Repositorio Docker Hub:

```text
https://hub.docker.com/r/<usuario-dockerhub>/devops-final-project
```

Imagen publicada:

```text
<usuario-dockerhub>/devops-final-project:v1
```

Evidencia requerida: captura de pantalla de la imagen publicada en Docker Hub.

## 10. Ejecucion del contenedor

Comando para el Grupo 3:

```bash
docker run -d \
  --name devops-final-project-grupo3 \
  -p 8003:8000 \
  -e GROUP_NAME="Grupo 3" \
  -e GROUP_MEMBERS="Daniel Alquinga, Oscar Maldonado" \
  -e COURSE_NAME="Curso de Profesionalizacion en DevOps" \
  <usuario-dockerhub>/devops-final-project:v1
```

URL de acceso:

```text
http://localhost:8003
```

## 11. Verificacion de la imagen

```bash
docker image ls
docker image ls | grep devops-final-project
```

Resultado esperado:

```text
<usuario-dockerhub>/devops-final-project   v1   <IMAGE_ID>   <CREATED>   <SIZE>
```

## 12. Verificacion del contenedor

```bash
docker ps -a --filter "name=devops-final-project"
docker inspect --format='{{.State.Health.Status}}' devops-final-project-grupo3
```

Estado esperado:

```text
healthy
```

## 13. Pruebas de funcionamiento

Pagina principal:

```text
http://localhost:8003
```

Endpoints:

```bash
curl http://localhost:8003/health
curl http://localhost:8003/info
curl http://localhost:8003/metrics
```

La pagina debe mostrar el grupo, integrantes, curso, estado del servicio, entorno de ejecucion, informacion del contenedor y endpoints disponibles.

## 14. Resultados

La aplicacion queda preparada para construirse como imagen Docker, ejecutarse en el puerto asignado al Grupo 3 y publicarse automaticamente en Docker Hub mediante GitHub Actions.

Evidencia requerida: captura de pantalla de la pagina de inicio ejecutandose en `http://localhost:8003`.

## 15. Conclusiones

El proyecto integra practicas basicas de DevOps: control de versiones, contenedores Docker, healthcheck, variables de entorno, automatizacion CI/CD con GitHub Actions y documentacion tecnica en Markdown.
