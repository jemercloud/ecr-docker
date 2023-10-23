# ECR-Docker

La acción ECR-Docker es una acción compuesta diseñada para construir una imagen Docker del repositorio actual y luego enviarla a un repositorio especificado de Amazon Elastic Container Registry (ECR).

### Características
* Hace el checkout del código fuente con actions/checkout@v4.
* Inicia sesión en Amazon ECR usando aws-actions/amazon-ecr-login@v2.
* Genera metadatos para Docker con docker/metadata-action@v4.
* Configura el entorno de construcción con docker/setup-buildx-action@v2.
* Construye y envía la imagen a ECR con docker/build-push-action@v4.

### Inputs:
* `dockerTag`: Etiqueta para la imagen Docker. (Requerido)
* `ecrImageName`: Nombre del repositorio para ECR. (Requerido)

### Outputs:
* `registry`: Registro ECR.
* `image`:  Imagen ECR con nombre completo y etiqueta


## Ejemplo

```yaml
name: ECR Docker Build and Push

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest
    steps:

    - name: ECR Docker Action
      uses: jemercloud/ecr-docker@v1
      with:
        dockerTag: ${{ github.event.release.tag_name }}
        ecrImageName: 'random-microservice-api'
```