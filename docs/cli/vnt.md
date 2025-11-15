---
title: VNT
createTime: 2025/10/21 16:55:37
permalink: /cli/wxf2voly/
---
## [VNT](https://rustvnt.com/)

::: center
**Win被控端**
:::

```powershell
Set-ExecutionPolicy Bypass -Scope Process -Force; Invoke-Expression ((New-Object System.Net.WebClient).DownloadString('https://ghproxy.cn/https://raw.githubusercontent.com/jianghuaangte/vnt/refs/heads/main/install.ps1'))
```

### Docker
::: center
**客户端 vnt**
:::

::: code-tabs
- 需要tun模块和特权模式

@tab cli
```shell
docker run --name vnt-cli --net=host --privileged --restart=always  -d lmq8267/vnt -k test123
```

@tab compose
```yaml
version: '3.9'
services:
  vnt:
    image: lmq8267/vnt
    restart: always
    privileged: true
    network_mode: host
    container_name: vnt-cli
    command: '-k test123'
```

:::


::: center
**服务端 vnts**
:::

::: code-tabs

@tab cli
```shell
docker run --name vnts -p 29872:29872/tcp -p 29872:29872/udp -p 29870:29870/tcp --restart=always -d lmq8267/vnts -p 29872 -P 29870 -U useradmin -W password
```

@tab compose
```yaml
version: '3.9'
services:
  vnts:
    image: lmq8267/vnts
    restart: always
    ports:
      - '29870:29870/tcp'
      - '29872:29872/tcp'
      - '29872:29872/udp'
    container_name: vnts
    command: '-p 29872 -P 29870 -U useradmin -W password'
```

:::
