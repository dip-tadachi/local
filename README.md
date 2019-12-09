# local

- mac / windows(10) compatible docker-comopse

## preparation

### /etc/hosts

1. install `SwitchHosts!` (option)
2. add `127.0.0.1    www.plantuml.docker`
3. add `127.0.0.1    quickchart.docker`

### proxy

1. install `cntlm` (option)
2. add `*.docker` in NoProxy

### nginx-proxy

1. install `mkcert`
2. `cd nginx-proxy/certs`
3. `mkcert -install`
4. `mkcert "*.plantuml.docker" plantuml.docker`
5. `mv _wildcard.plantuml.docker+1-key.pem plantuml.docker.key`
6. `mv _wildcard.plantuml.docker+1.pem plantuml.docker.crt`
7. `mkcert "*.quickchart.docker" quickchart.docker`
8. `mv _wildcard.quickchart.docker+1-key.pem plantuml.docker.key`
9. `mv _wildcard.quickchart.docker+1.pem plantuml.docker.crt`

### plantuml-server

1. `cd plantuml-server`
2. `chmod +x docker-entrypoint-custom.sh` (mac only)

## network

1. `docker network create --driver bridge nginx-proxy`

## docker-compose (up)

1. `cd nginx-proxy`
2. `docker-compose build`
3. `docker-compose up -d`
4. `cd plantuml-server`
5. `docker-compose build`
6. `docker-compose up -d`
7. `cd quickchart`
8. `docker-compose up -d`

## docker-compose (down)

1. `cd nginx-proxy`
2. `docker-compose down -v --remove-orphans`
3. `cd plantuml-server`
4. `docker-compose down -v --remove-orphans`
5. `cd quickchart`
6. `docker-compose down -v --remove-orphans`
