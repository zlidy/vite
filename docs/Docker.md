# Docker

从 2017 年 3 月开始 docker 在原来的基础上分为两个分支版本: Docker CE 和 Docker EE：Docker CE 即社区免费版；Docker EE 即企业版，强调安全，但需付费使用；按照官网上Docker Engine - Community包现在就是叫做Docker CE。

------

### 卸载老的Docker及依赖

为什么你可能还需要删除较低的Docker安装？因为较旧版本的Docker被称为docker或docker-engine（它是一个简化Docker安装的命令行工具，通过一个简单的命令行即可在相应的平台上安装Docker，比如VirtualBox、 Digital Ocean、Microsoft Azure）

------

```shell
sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine
```

### 安装一些依赖库

- yum-utils 提供 yum-config-manager 类库
- device-mapper-persistent-data 和 lvm2 被devicemapper 存储驱动依赖

```shell
sudo yum install -y yum-utils \
  device-mapper-persistent-data \
  lvm2
```

设置稳定版本的库

```shell
sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo
```

### 安装Docker CE

```shell
yum install -y docker-ce
```

安装完之后启动

```shell
sudo systemctl start docker
```

测试是否安装成功

```shell
[root@pdai ~]# systemctl status docker
● docker.service - Docker Application Container Engine
   Loaded: loaded (/usr/lib/systemd/system/docker.service; disabled; vendor preset: disabled)
   Active: active (running) since Mon 2020-02-17 13:57:45 CST; 39s ago
     Docs: https://docs.docker.com
 Main PID: 26029 (dockerd)
    Tasks: 8
   Memory: 36.9M
   CGroup: /system.slice/docker.service
           └─26029 /usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd
```

