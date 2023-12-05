### start with docker
```json
cd bin/
```
### source tree folder code and docker
```
.source code
.(folder docker-compose)
├── docker-compose.yml
├── docs.md
├── nginx
│         ├── Dockerfile
│         ├── config
│         │         └── default.conf
│         └── nginx.conf
└── php
    └── Dockerfile

```
### prepare environment
```json
make env
```
### build image
```json
make build
```

### start docker
```json
  make start
```

### exec service
```json
make exec service={container_name}
```

### stop docker
```json
make stop
```