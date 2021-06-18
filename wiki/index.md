## Общее описание

Репа содержит кучку шаблонов для gitlab-ci которые можно инклюдить:
```yaml
include:
  - project: 'ci-cd/templates'
    ref: master
    file: 'deploy.wiki.gitlab-ci.yml'
```
