# Install Caddy 2 with Docker on Ubuntu

* Ubuntu 22.04

## Install Docker

```shell
curl -fsSL https://get.docker.com -o get-docker.sh
DRY_RUN=1 sudo sh ./get-docker.sh
```

See [Install Docker Engine on Ubuntu](https://docs.docker.com/engine/install/ubuntu/#install-using-the-convenience-script)

## Install Docker Compose

```shell
curl -SL https://get.daocloud.io/docker/compose/releases/download/v2.14.0/docker-compose-linux-x86_64 -o /usr/local/bin/docker-compose
```

See [Install the Compose standalone](https://docs.docker.com/compose/install/other/)


```shell
chmod +x /usr/local/bin/docker-compose
```

Check version

```shell
docker-compose -v
```

If OK, shows:
```
Docker Compose version v2.14.0
```

## docker-compose.yml

用`touch`命令创建一个文件名为 `docker-compose.yml`的文件。用`vi`命令打开，粘贴以下配置：

```shell
cd /opt/data/
mkdir caddy
cd caddy
mkdir data
mkdir config
touch docker-compose.yml
```

Copy and paste the configuration

```yaml
version: "3.7"

services:
        caddy:
                image: caddy:2-alpine
                restart: unless-stopped
                ports:
                        - "80:80"
                        - "443:443"
                volumes:
                        - ./Caddyfile:/etc/caddy/Caddyfile
                        - ./data:/data # Optional
                        - ./config:/config # Optional
```

## Config Caddy

用`touch`命令创建`Caddyfile`，粘贴以下配置：

```json
yourdomain.com {
  respond "Hello, Caddy!"
}
```

DNS A记录指向你的公网IP地址。

Open browser, visit: [https://yourdomain.com]()。

If OK, `Hello, Caddy!` will shown.

```
cd 
```


Update Caddyfile to:

```
yourdomain.com {
  root * /data
  file_server
}
```