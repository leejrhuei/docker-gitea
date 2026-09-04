### 项目结构

```
docker-gitea
├─ gitea                    Gitea目录
├─ mysql                    MySQL目录
├─ nginx                    Nginx目录
│   ├─ conf                 Nginx项目配置目录
├─ docker-compose.yml       容器配置文件
├─ README.md                说明文档
```

### 部署配置

1. gitea/conf/app.ini

```ini
[server]
DOMAIN = gitea.xxx.com
SSH_DOMAIN = gitea.xxx.com
ROOT_URL = http://gitea.xxx.com

[ssh.minimum_key_sizes]
RSA = 2048
```

### QA

1. /etc/docker/daemon.json配置镜像加速器？

```json
{
  "registry-mirrors": [
    "https://2a6bf1988cb6428c877f723ec7530dbc.mirror.swr.myhuaweicloud.com",
    "https://docker.1ms.run",
    "https://proxy.vvvv.ee",
    "https://wget.la",
    "https://dockerproxy.net"
  ]
}
```
