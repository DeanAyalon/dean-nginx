# About
This repository contains the configuration for the Nginx used as a proxy, running on my server.<br>
It is part of the [dean-server](https://github.com/DeanAyalon/dean-server) monorepo

This repository uses [nginx-proxy](https://github.com/nginx-proxy/nginx-proxy), which, using environment variables, automatically assigns an http/s proxy to running Docker containers

# Use
## Setup
### Requirements
- Docker Engine or Docker Desktop, with Docker Compose installed (Built in)
    - This repository uses the new `docker compose`, it is unknown how well it would work with legacy `docker-compose` versions

### Certificates
`nginx-proxy` fetches the certificates in the following path:
> MOUNT/{domain}.crt<br>
  MOUNT/{domain}.key<br>
  MOUNT/default.crt<br>
  MOUNT/default.key

### Containers
Containers need to be set up with the following environment variable for nginx-proxy to route to them:
- `VIRTUAL_HOST` with the value as the full domain to assign that service
> ex. `VIRTUAL_HOST=verdaccio.deanayalon.com`

## Run
Docker Compose can be ran from the context of this repository, but it is recommended to use it from the context of the entire [dean-server](https://github.com/DeanAyalon/dean-server) monorepo

### Profiles
This repository contains multiple profiles using separate configurations.

Use: `docker compose --profile <profile> <command>`

Profiles:
* **live**: Production nginx, uses nginx-proxy to automatically set up reverse-proxy to containers
* **certs**: Spin up Certbot to request new certificates
* **certs-test**: Spin up Certbot to simulate certificate requests

## Featured Technologies
[![Docker](https://img.shields.io/badge/docker-1D63ED?style=for-the-badge&logo=docker&logoColor=white)](https://hub.docker.com/repository/docker/nginxproxy/nginx-proxy)
[![Nginx](https://img.shields.io/badge/nginx-009639?style=for-the-badge&logo=nginx)](https://nginx.com)<br>
[![nginx-proxy](https://custom-icon-badges.demolab.com/badge/nginx--proxy-F0F0F0?style=for-the-badge&logo=nginx-proxy-identicon&logoColor=D4AB64)](https://github.com/nginx-proxy/nginx-proxy)
