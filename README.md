## Общее описание

Репозиторий содержит набор шаблонов для gitlab-ci

## Полезные ссылки

Какой никакой wiki можно посмотреть тут [https://preset-for-future.gitlab.io/templates](https://preset-for-future.gitlab.io/templates)

Репозиторий с tools [https://preset-for-future.gitlab.io/tools](https://preset-for-future.gitlab.io/tools)

>Логика именования: <br>
>$stage.$tool.gitlab-ci.yml <br>
>stage - стейдж который содержиться в данных темплейтах (чаще всего, но бывает и сразу несколько) <br>
>tool - Инструмент который в основном используется внутри этого шаблона <br>
>gitlab-ci.yml - Расширение которое указывает на то что этот шаблон для gitlab <br>

## Пример использования

Пример можно посмотреть в group-for-test/repo-for-test

Чаще всего весь gitlab-ci.yml для проектов будет выглядеть так

```yaml
---
include:
  - project: 'ci-cd/templates'
    ref: master
    file: 'build.docker.gitlab-ci.yml'
  - project: 'ci-cd/templates'
    ref: master
    file: 'deploy.helm.gitlab-ci.yml'
  - project: 'ci-cd/templates'
    ref: master
    file: 'deploy.wiki.gitlab-ci.yml'
```

Проект в котором лежат шаблоны чаще всего 'ci-cd/templates' но в целом можно шаблонизировать
```sh
CI_TEMPLATE_PROJECT=ci-cd/templates
```
