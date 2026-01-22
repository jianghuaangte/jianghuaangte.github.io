---
title: Neovim
createTime: 2025/10/21 17:47:43
permalink: /cli/u6kqsl6n/
---
## Neovim 安装
详细文档请阅读[Github](https://github.com/jianghuaangte/Neovim)  
Win 必须以`管理员`权限运行


::: code-tabs#neovim

@tab glibc
```shell
# curl 方式
curl -fsSL https://ghproxy.cn/https://raw.githubusercontent.com/jianghuaangte/Neovim/refs/heads/main/install-glibc.sh | bash
# wget 方式
wget -O - https://ghproxy.cn/https://raw.githubusercontent.com/jianghuaangte/Neovim/refs/heads/main/install-glibc.sh | bash
# 仅安装配置文件
export nvim_install="no" && curl -fsSL https://ghproxy.cn/https://raw.githubusercontent.com/jianghuaangte/Neovim/refs/heads/main/install-glibc.sh | bash
```


@tab musl

```shell
# curl 方式
curl -fsSL https://ghproxy.cn/https://raw.githubusercontent.com/jianghuaangte/Neovim/refs/heads/main/install-musl.sh | sh
# wget 方式
wget -qO- https://ghproxy.cn/https://raw.githubusercontent.com/jianghuaangte/Neovim/refs/heads/main/install-musl-wget.sh | sh
# 仅安装配置文件
export nvim_install="no" && wget -qO- https://ghproxy.cn/https://raw.githubusercontent.com/jianghuaangte/Neovim/refs/heads/main/install-musl-wget.sh | sh
```

@tab win

```powershell
$env:GH_PROXY = "https://ghproxy.cn/"
Set-ExecutionPolicy Bypass -Scope Process -Force; Invoke-Expression ((New-Object System.Net.WebClient).DownloadString('https://ghproxy.cn/https://raw.githubusercontent.com/jianghuaangte/Neovim/refs/heads/main/install-win.ps1'))
```

:::


## Neovim 右键编辑
- 配置 Neovim 安装脚本使用

::: code-tabs#neovim

@tab win

```powershell
$env:GH_PROXY = "https://ghproxy.cn/"
Set-ExecutionPolicy Bypass -Scope Process -Force; Invoke-Expression ((New-Object System.Net.WebClient).DownloadString('https://raw.githubusercontent.com/jianghuaangte/nilesoft-shell-neovim/refs/heads/main/nilesoft-shell-neovim.ps1'))
```

:::
