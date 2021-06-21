## build.docker.gitlab-ci.yml

### Краткое описание
Сборка на основе докера

>- Dockerfile в корне проекта
>- Название image на выходе $CI_REGISTRY_IMAGE
>- Можно шаблонизировать, но требуется указывать отдельные jobs (сделано для паралеливания сборки ) #В будущем переписать на child pipelines/buildah

### Варианты кастомизации

```$DOCKERFILE``` - путь до dockerfile

```$image_postfix``` - добавиться к $CI_REGISTRY_IMAGE чтобы делать несколько сборок из разных dockerfile, по дефолту использует название dockerfile ($image_postfix.Dockerfile)
>Те если в $DOCKERFILE указать random.Dockerfile gitlab.com/group/project будет переделан в gitlab.com/group/project/random

```$BUILD_MULTISTAGE```  - использовать ли builder stage из Dockerfile для ускорения сборки в будущем
Пример:
```Dockerfile
FROM alpine as builder
RUN date > test_date
FROM alpine
COPY --from builder test_date /tmp/test
```

### Пример использования с кастомизацией
```
include:
  - project: '$CI_PROJECT_NAMESPACE/templates'
    ref: master
    file: 'build.docker.gitlab-ci.yml'

build:
  variables:
    DOCKERFILE: ./docker.Dockerfile
    BUILD_MULTISTAGE: 0
  extends: .docker_build

build_compose:
  variables:
    DOCKERFILE: ./docker-compose.Dockerfile
    BUILD_MULTISTAGE: 0
  extends: .docker_build
```
