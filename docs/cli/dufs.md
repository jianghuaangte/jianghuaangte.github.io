---
title: Dufs
createTime: 2025/11/15 10:56:19
permalink: /cli/ci6hznca/
---
## Dufs
[Dufs](https://github.com/sigoden/dufs) 是一款独特的实用文件服务器，支持静态服务、上传、搜索、访问控制、webdav

::: code-tabs#shell-cmd

@tab cli
```shell
docker run -v `pwd`:/data -p 5000:5000 --rm -it sigoden/dufs /data -A
```


@tab compose

```yml
version: '3'
services:
  dufs:
    image: sigoden/dufs
    ports:
    - 5000:5000
    volumes:
    - .:/data
    command: /data -A
    restart: unless-stopped
```

:::

