---
title: Zsh
createTime: 2025/10/21 14:11:47
permalink: /cli/5o0qtomr/
---
## Zsh

### 安装
多系统下的安装`zsh`命令
::: code-tabs#shell-cmd

@tab debian/ubuntu
```shell
apt install zsh
```


@tab apline

```shell
apk add zsh
```

:::

### 默认 shell
修改默认 shell 为`zsh`

```shell
sudo chsh -s $(which zsh)
# or
chsh -s $(which zsh)
```

### Oh My Zsh
安装命令

```shell
REMOTE=https://ghfast.top/https://github.com/ohmyzsh/ohmyzsh.git sh -c "$(curl -fsSL https://ghfast.top/https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

## 添加普通用户
```shell
apt install sudo
# 创建用户并加入 sudo 组
useradd -m -s /bin/bash -G sudo myuser
# 设置密码
passwd myuser
# 关闭使用 root 密码登录ssh
nvim /etc/ssh/sshd_confg
```
