# About
This repository contains the configuration for the Nginx used as a proxy, running on my server.

The latest version of this repository uses [nginx-proxy](https://github.com/nginx-proxy/nginx-proxy), which, using environment variables, automatically assigns an http/s proxy to running Docker containers

# Use
## Setup
## Requirements
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
* **legacy**: Legacy nginx, uses manual configuration, not updated or supported.

# Legacy
The legacy version uses a raw nginx image and a manual configuration file, which is **not** up to date with current server configuration.

**Currently, the legacy version is DEPRECATED.** Development will continue if nginx-proxy is ever abandoned, for any reason. and a manual configuration is necessary.<br>

### Setup
#### Certificates
The certificates are set up to be taken from the mount in the following path:
> MOUNT/{hostname}/<br>
    - fullpath.pem<br>
    - privkey.pem

#### Configuration
The configuration is currently set up to reverse-proxy:
- verdaccio
- verdaccio-dev
- filemaker

For any changes, modify the [configuration file](./legacy/conf/app.conf)



## Featured Technologies
[![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)](https://docker.com)
[![Nginx](https://img.shields.io/badge/nginx-009639.svg?style=for-the-badge&logo=nginx&logoColor=white)](https://npmjs.com)

[nginx-proxy](https://github.com/nginx-proxy/nginx-proxy)