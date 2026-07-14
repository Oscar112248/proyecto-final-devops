# Proyecto Final DevOps

Aplicacion web desarrollada con FastAPI para el Trabajo Final DevOps. El proyecto construye una imagen Docker, publica la imagen en Docker Hub mediante GitHub Actions y expone una pagina de verificacion con informacion del grupo y del contenedor.

## Datos del Grupo

- Grupo: Grupo 3
- Integrantes: Daniel Alquinga, Oscar Maldonado
- Curso: Curso de Profesionalizacion en DevOps

## Estructura

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

## Ejecucion Local

```bash
pip install -r requirements.txt
cd app
uvicorn main:app --host 0.0.0.0 --port 8000
```

Abrir `http://localhost:8000`.

## Construccion Docker

```bash
docker build -t devops-final-project:v1 .
```

## Ejecucion del Contenedor para Grupo 3

```bash
docker run -d \
  --name devops-final-project-grupo3 \
  -p 8003:8000 \
  -e GROUP_NAME="Grupo 3" \
  -e GROUP_MEMBERS="Daniel Alquinga, Oscar Maldonado" \
  -e COURSE_NAME="Curso de Profesionalizacion en DevOps" \
  <usuario-dockerhub>/devops-final-project:v1
```

URL: `http://localhost:8003`

## Endpoints

- `/`: pagina principal
- `/health`: estado de salud del servicio
- `/info`: informacion de la aplicacion y del contenedor
- `/metrics`: metricas basicas

## Verificacion

```bash
docker image ls
docker ps -a --filter "name=devops-final-project"
docker inspect --format='{{.State.Health.Status}}' devops-final-project-grupo3
curl http://localhost:8003/health
curl http://localhost:8003/info
curl http://localhost:8003/metrics
```

## GitHub Actions

El workflow `.github/workflows/dockerhub.yml` construye la imagen con el `Dockerfile` y la publica en Docker Hub con la etiqueta `v1`.

Secrets requeridos en GitHub:

- `DOCKERHUB_USERNAME`
- `DOCKERHUB_TOKEN`

Imagen esperada:

```text
<usuario-dockerhub>/devops-final-project:v1
```
