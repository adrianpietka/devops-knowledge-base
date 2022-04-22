# Docker Compose

**Invalid interpolation format for "environment" option in service "xxx": "secret=\$2y\$12"**

Bad:

```yaml
environment:
  - secret=$2y$12
```

Good:

```yaml
environment:
  - secret=$$2y$$12
```