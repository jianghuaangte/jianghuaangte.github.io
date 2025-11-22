---
title: WezTerm
createTime: 2025/10/21 13:26:43
permalink: /cli/shsfkhcc/
---
## WezTerm

### 安装
终端软件安装
[官网](https://wezterm.org/)
|[Github](https://bgithub.xyz/wezterm/wezterm/releases)

### 配置文件
- 提供类似于 oh my wezterm 的配置

```shell
git clone https://ghfast.top/https://github.com/KevinSilvester/wezterm-config.git ~/.config/wezterm
```

### 字体
- JetBrainsMono.tar.xz
::: code-tabs
@tab ~/.config/wezterm/config/fonts.lua
```lua
-- 注意区分左mac、右其它系统
local font_size = platform.is_mac and 16 or 9.75
```

:::


### 默认 shell
- 可以使用`which <shell>` 查看你的 shell 位置
::: code-tabs
@tab ~/.config/wezterm//config/domains.lua
```lua :collapsed-lines
-- 这是设置 win
if platform.is_win then
   options.default_prog = { 'pwsh', '-NoLogo' }  -- 在这里指定默认shell // [!code highlight]
   options.launch_menu = {
      { label = 'PowerShell Core', args = { 'pwsh', '-NoLogo' } },
      { label = 'PowerShell Desktop', args = { 'powershell' } },
      { label = 'Command Prompt', args = { 'cmd' } },
      { label = 'Nushell', args = { 'nu' } },
      { label = 'Msys2', args = { 'ucrt64.cmd' } },
      {
         label = 'Git Bash',
         args = { 'C:\\Users\\kevin\\scoop\\apps\\git\\current\\bin\\bash.exe' },
      },
   }
-- 这是设置 Mac
elseif platform.is_mac then
   options.default_prog = { '/bin/zsh', '-l' }   -- 在这里指定默认shell // [!code highlight]
   options.launch_menu = {
      { label = 'Bash', args = { 'bash', '-l' } },
      { label = 'Fish', args = { '/opt/homebrew/bin/fish', '-l' } },
      { label = 'Nushell', args = { '/opt/homebrew/bin/nu', '-l' } },
      { label = 'Zsh', args = { 'zsh', '-l' } },
   }
-- 这是设置 Linux
elseif platform.is_linux then
   options.default_prog = { 'fish', '-l' }  -- 在这里指定默认shell // [!code highlight]
   options.launch_menu = {
      { label = 'Bash', args = { 'bash', '-l' } },
      { label = 'Fish', args = { 'fish', '-l' } },
      { label = 'Zsh', args = { 'zsh', '-l' } },
   }
end
```

:::

### 配置SSH
- F3 输入`/`查找关键词
- Mac 必须设置使用`标准按键`才能使用F3
- 必须要有`multiplexing = 'None'`否则会走wezterm 自身的server 协议
::: code-tabs
@tab ~/.config/wezterm/config/launch.lua
```lua :collapsed-lines
local platform = require('utils.platform')

-- 在这里添加本地ssh // [!code focus:27]
local options = {
   -- ref: https://wezfurlong.org/wezterm/config/lua/SshDomain.html
   ssh_domains = {
      {
         name = 'ssh-synology',
         username = 'tsihnhn',
         remote_address = '192.168.2.200:22',
        --  ssh_option = {
        --    identityfile = '~/.ssh/id_rsa.pub',
        --  },
         multiplexing = 'None',
        -- default_prog = { 'zsh', '-l' },
        -- assume_shell = 'Posix',
      },
      {
         name = 'ssh-n1',
         username = 'root',
         remote_address = '192.168.3.101:22',
        --  ssh_option = {
        --    identityfile = '~/.ssh/id_rsa.pub',
        --  },
         multiplexing = 'None',
        -- default_prog = { 'zsh', '-l' },
        -- assume_shell = 'Posix',
      },
   },

   -- ref: https://wezfurlong.org/wezterm/multiplexing.html#unix-domains
   unix_domains = {},

   -- ref: https://wezfurlong.org/wezterm/config/lua/WslDomain.html
   wsl_domains = {},
}

if platform.is_win then
   options.ssh_domains = {
      {
         name = 'ssh:wsl',
         remote_address = 'localhost',
         multiplexing = 'None',
         default_prog = { 'fish', '-l' },
         assume_shell = 'Posix',
      },
   }

   options.wsl_domains = {
      {
         name = 'wsl:ubuntu-fish',
         distribution = 'Ubuntu',
         username = 'kevin',
         default_cwd = '/home/kevin',
         default_prog = { 'fish', '-l' },
      },
      {
         name = 'wsl:ubuntu-bash',
         distribution = 'Ubuntu',
         username = 'kevin',
         default_cwd = '/home/kevin',
         default_prog = { 'bash', '-l' },
      },
   }
end

return options
```
:::
