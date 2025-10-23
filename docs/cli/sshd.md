---
title: sshd
createTime: 2025/10/23 13:43:38
permalink: /cli/kyayijds/
---
## sshd
有两个不同的容器支持 sshd 容器开发

:::code-tabs
@tab openssh-server
```shell{12-13}
version: '3.8'
services:
  openssh-server:
    hostname: openssh-server   # 主机名
    image: linuxserver/openssh-server:latest
    container_name: openssh-server
    environment:
      - PUID=1000              # 使用普通用户权限（推荐不要用0）
      - PGID=1000
      - TZ=Asia/Shanghai
      - PASSWORD_ACCESS=true   # 启用密码登录
      - USER_NAME=ll           # 设定用户名，不能为root
      - USER_PASSWORD=123456   # 设定密码
      - SUDO_ACCESS=true       # sudo
    ports:
      - 2222:2222              # 映射 SSH 端口
# network_mode: "host" 
    restart: unless-stopped
```

@tab testcontainers-sshd
```shell{2}
version: '3.8'
# 默认用户/密码:root
services:
  sshd:
    image: testcontainers/sshd:1.3.0
    container_name: sshd-tunnel
    ports:
      - "2222:22"         # ssh 端口
      - "60000:60000/udp" # mosh 端口
      - "60001:60001/udp" # mosh 端口
      - "60002:60002/udp" # mosh 端口
    restart: unless-stopped
```
:::

