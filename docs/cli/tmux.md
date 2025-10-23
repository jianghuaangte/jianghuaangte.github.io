---
title: Tmux
createTime: 2025/10/21 17:53:46
permalink: /cli/gi1pdhq5/
---
## Tmux

### 安装

::: code-tabs#neovim

@tab debian/ubuntu
```shell
apt update
apt install tmux
```


@tab alpine

```shell
apk update
apk add tmux
```

:::


---
## Oh My Tmux
配置 tmux

**依赖**:  
- awk
- perl（支持 Time：：HiRes）
- grep
- sed

**终端要求**
- 支持真彩色
- 支持 OSC52


### 安装

```shell
export OH_MY_TMUX_REPOSITORY="https://ghfast.top/https://github.com/gpakosz/.tmux.git"
curl -fsSL "https://ghfast.top/https://github.com/gpakosz/.tmux/raw/refs/heads/master/install.sh#$(date +%s)" | bash
```


### 配置
vi 模式
::: code-tabs#ohmytmux

@tab .zshrc

```shell
# 启用vi操作
echo 'export EDITOR=vim' >> ~/.zshrc
```

:::

---

禁嵌套、色彩支持
::: code-tabs
@tab .zshrc
```shell
# 仅在外层终端设置 TERM
echo 'export TERM=xterm-256color' >> ~/.zshrc
```


:::

---

自启动

::: code-tabs#configs

@tab .zshrc

```shell
echo '
if [ -x "$(command -v tmux)" ] && [ -z "${TMUX}" ]; then
    exec tmux new-session -A -s ${USER} >/dev/null 2>&1
fi' >> ~/.zshrc
```

:::

---
生效
```shell
source ~/.zshrc
```



### 偏好设置

OSC52 复制
::: code-tabs

@tab ~/.config/tmux/tmux.conf.local

```shell
echo 'set -g set-clipboard on' >> ~/.config/tmux/.tmux.conf.local
```

:::
---

::: code-tabs
@tab ~/.config/tmux/tmux.conf.local

```shell
# 覆盖C-a
echo 'set -g prefix2 C-b' >> ~/.tmux.conf.local
# 覆盖延迟操作
echo 'set -sg repeat-time 10' >> ~/.tmux.conf.local
```
:::
