---
title: Tmate
createTime: 2025/10/21 16:55:45
permalink: /cli/3kadhems/
---
### 简介
Tmate 是基于 Tmux 的远程共享终端工具 —— 可以让别人实时连接你的终端进行协作调试

### 安装

::: code-tabs
@tab debian/ubuntu

```shell
apt install tmate
```

@tab alpine

```shell
apk add tmate
```

:::

### 配置
Tmate 和 Tmux 共享配置

```shell
# 启用
tmate
```

**查看所有连接地址**
```shell
tmate show-messages
```

::: warning
仅将只读链接发送给用户
:::
