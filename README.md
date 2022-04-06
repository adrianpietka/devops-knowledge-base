# DevOps - Knowledge Base

## Uruchamianie lokalnego serwera

```
docker run --rm -it -p 8000:8000 -v ${PWD}:/docs squidfunk/mkdocs-material
```

## Budowanie wersji statycznej

```
docker run --rm -it -p 8000:8000 -v ${PWD}:/docs squidfunk/mkdocs-material build
```