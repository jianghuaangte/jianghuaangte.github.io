---
title: 共享终端会话
tags:
  - tmux
  - tmate
  - ttyd
  - vnt
  - 共享
createTime: 2026/04/20 15:53:30
permalink: /blog/ejwyatq3/
---

## 共享终端
两种方案各有优缺点，下面将逐一进行说明

### TTYD（推荐）
优点：
- 无需安装openssh-client，只需要浏览器即可。
- 可以完全使用 tmux 的配置文件

缺点：
- 安全性有待考验

方案思路：
服务端tmux -> 服务端TTYD -> 服务端loophole -> VNT组网 -> 客户端网页访问  

为什么要用loophole ，因为如果客户是在 openwrt 等设备中运行的 vnt，那作为宿主机的Windows是无法访问 10.26.0.x 的 ttyd 投屏

**具体实现**
- [loophole 网站发布](https://github.com/loophole/cli)
- [VNT 组网](https://github.com/vnt-dev/vnt)
- [TTYD 网页终端](https://github.com/tsl0922/ttyd)

```shell
tmux
# -W 客户端可写，不建议添加
nohup ./ttyd -p 8880 tmux attach -t 0 >/dev/null 2>&1 &
# 登录 loophole，输入验证码在网页验证
./loophole account login
# 暴露本地 8880 端口的 Web 服务，并指定自定义二级域名
nohup ./loophole http 8880 -u admin -p 123456 --hostname ttyd >/dev/null 2>&1 &
# 访问网站
https://ttyd.loophole.site
# VNT组网，这里省略
tmux 连接客户端 ssh
```


### Tmate
优点：
- 客户端不需要安装 tmate 就能实时共享会话

缺点：
- tmate 无法完全使用 tmux 的配置文件
- tmate 自带的服务器有时会延迟高
- 部分架构无法安装 tmate 导致 -> 服务端安装 tmate -> 客户端连接 -> 服务端通过vnt等组网工具再通过ssh连接客户端
- 客户端需要安装 openssh-client Windows 一般没有安装

方案思路：
服务端Tmate -> 客户端连接 -> VNT 组网 -> 服务端连接 VNT 组网后的客户端SSHD



