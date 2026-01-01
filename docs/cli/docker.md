---
title: docker
createTime: 2026/01/01 10:03:57
permalink: /cli/h3aehs7v/
---
## 安装
::: code-tabs
@tab 中科大源
```shell
curl -fsSL https://get.docker.com -o get-docker.sh
sudo DOWNLOAD_URL=https://mirrors.ustc.edu.cn/docker-ce sh get-docker.sh
```

@tab Github 源
```shell
curl -fsSL https://raw.githubusercontent.com/docker/docker-install/master/install.sh -o get-docker.sh
sh get-docker.sh
```
:::

## 容器镜像源

::: code-tabs
@tab *Unix
```shell
echo '{
  "registry-mirrors": [
    "https://docker.milu.moe",
    "https://docker.1ms.run",
    "https://ghcr.milu.moe"
  ],
  "dns": ["8.8.8.8", "114.114.114.114"]
}' | sudo tee /etc/docker/daemon.json > /dev/null

systemctl daemon-reload
systemctl restart docker
```

@tab DSM7.2
```shell
# 备份
cp /var/packages/ContainerManager/etc/dockerd.json /var/packages/ContainerManager/etc/dockerd.json.bak
# 编辑
vim /var/packages/ContainerManager/etc/dockerd.json
# 重启
synosystemctl restart pkgctl-ContainerManager
```

:::
