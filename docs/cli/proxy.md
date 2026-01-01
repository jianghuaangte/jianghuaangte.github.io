---
title: Proxy
createTime: 2025/10/21 19:05:56
permalink: /cli/qigic98q/
---

### 终端代理

::: code-tabs
@tab *nix

```shell
# 代理
export http_proxy=http://127.0.0.1:7890
export https_proxy=$http_proxy
export ALL_PROXY=socks5://localhost:7890

# 取消
unset http_proxy
unset https_proxy
unset no_proxy
unset ALL_PROXY
```

@tab Win-cmd
```shell
# 代理
set http_proxy=http://127.0.0.1:1802
set https_proxy=http://127.0.0.1:1802

# 取消
set http_proxy=
set https_proxy=
```

@tab Win-Posh
```shell
# http(s)
$env:http_proxy = "http://<ip>:<port>"
$env:https_proxy = "http://<ip>:<port>"

# socks5
$env:all_proxy="socks5://127.0.0.1:1081"

# 取消
Remove-Item Env:HTTP_PROXY -ErrorAction Ignore
Remove-Item Env:HTTPS_PROXY -ErrorAction Ignore
Remove-Item Env:NO_PROXY -ErrorAction Ignore
```


:::

---
### Git 
::: code-tabs
@tab 代理
设置代理
```shell
git config --global https.proxy https://127.0.0.1:19810
git config --global http.proxy http://127.0.0.1:19810

# 取消
git config --global --unset http.proxy
git config --global --unset https.proxy
```
:::

---
### SSH
::: code-tabs
@tab ~/.ssh/config
```shell
Host github.com
  HostName github.com
  User git
  ProxyCommand nc -v -x 127.0.0.1:7890 %h %p
```
:::
