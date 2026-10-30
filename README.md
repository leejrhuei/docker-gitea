### 项目结构

```
docker-gitea
├─ conf                     配置目录
│   ├─ nginx                Nginx配置目录
│       ├─ conf.d           Nginx项目配置目录
│   ├─ pr-agent             PR-Agent配置目录
├─ data                     数据目录
├─ log                      日志目录
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

2. gitea ai review

```text
新建账号：登录root账号，右上角头像->管理后台->身份及认证->帐户管理->创建新帐户(如ai-review)
账号令牌：登录ai-review账号，右上角头像->设置->应用->令牌(read:user、read:repository、write:issue)
仓库授权：仓库->设置->协作者，添加ai-review账号(可写权限)
钩子设置：仓库->设置->Web钩子
        目标 URL：http://pr-agent:3000/api/v1/gitea_webhooks
        密钥：自定义
        触发条件：自定义事件(合并请求、合并请求已评论)
```

### QA

1. CentOS 7.x 安装 Docker 社区版本？

```shell
# 添加Docker软件包源
sudo wget -O /etc/yum.repos.d/docker-ce.repo http://mirrors.cloud.aliyuncs.com/docker-ce/linux/centos/docker-ce.repo
sudo sed -i 's|https://mirrors.aliyun.com|http://mirrors.cloud.aliyuncs.com|g' /etc/yum.repos.d/docker-ce.repo
# 安装Docker社区版本，容器运行时containerd.io，以及Docker构建和Compose插件
sudo yum -y install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# 启动Docker
sudo systemctl start docker
# 设置Docker守护进程在系统启动时自动启动
sudo systemctl enable docker
```

2. /etc/docker/daemon.json 配置镜像源？

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
