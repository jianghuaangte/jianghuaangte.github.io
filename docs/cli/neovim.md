---
title: Neovim
createTime: 2025/10/21 17:47:43
permalink: /cli/u6kqsl6n/
---
## Neovim 配置
安装`neovim`并提供最小的配置文件  
Win 必须以`管理员`权限运行


::: code-tabs#neovim

@tab glibc
```shell
curl -fsSL https://ghproxy.cn/https://raw.githubusercontent.com/jianghuaangte/Neovim/refs/heads/main/install-glibc.sh | bash
```


@tab musl

```shell
wget -O - https://ghproxy.cn/https://raw.githubusercontent.com/jianghuaangte/Neovim/refs/heads/main/install-musl.sh | sh
```

@tab win

```powershell
$env:GH_PROXY = "https://ghproxy.cn/"
Set-ExecutionPolicy Bypass -Scope Process -Force; Invoke-Expression ((New-Object System.Net.WebClient).DownloadString('https://ghproxy.cn/https://raw.githubusercontent.com/jianghuaangte/Neovim/refs/heads/main/install-win.ps1'))
```

:::
