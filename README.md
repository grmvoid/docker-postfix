## Quick reference
- **Image based on**:   
  [alpine](https://hub.docker.com/_/alpine)

- **Supported architectures**:    
  `linux/amd64`, `linux/arm64`

- **Maintained by**:  
  [grmvoid](https://github.com/grmvoid)

- **Where to file issues**:    
  [https://github.com/grmvoid/docker-php/issues](https://github.com/grmvoid/docker-postfix/issues?q=)

## Supported tags and respective `Dockerfile` links

- [`3.9.1`, `3.9`](https://github.com/grmvoid/docker-postfix/blob/master/3.9/Dockerfile)

## How to usage this image

### start a postfix instance

```bash
docker run --name some-postfix -d grmvoid/postfix:3.9.1
```

### ... via [`docker-compose`](https://github.com/docker/compose)
Example `docker-compose.yml` for `postfix`:

```yaml
version: '3.1'

services:
    postfix:
        image: grmvoid/postfix:3.9.1
        restart: always
        ports:
            - "25:25/tcp"
            - "587:587/tcp"
```

## LICENSE

View [license](https://de.postfix.org/ftpmirror/LICENSE) information for the software contained in this image.