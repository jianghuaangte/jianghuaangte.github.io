---
title: Neovim
createTime: 2025/10/21 17:47:43
permalink: /cli/u6kqsl6n/
---
## Neovim 配置
安装`neovim`并提供最小的配置文件

::: code-tabs#neovim

@tab glibc
```shell
curl -fsSL \
     https://ghproxy.cn/https:/raw.githubusercontent.com/free-150/scripts/refs/heads/main/nvim.sh \
     | bash -s -- -m https://ghproxy.cn
```


@tab musl

```shell
wget -O - https://raw.gitcode.com/guoweiwangluo/neovim/raw/main/install-alpine.sh | sh
```

:::
