# Use
The latest version of this repository uses [nginx-proxy](https://github.com/nginx-proxy/nginx-proxy), which, using environment variables, automatically assigns an http/s proxy to running Docker containers

## Setup
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
