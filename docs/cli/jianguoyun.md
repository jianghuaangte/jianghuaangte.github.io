---
title: JianGuoYun
createTime: 2025/10/21 20:57:29
permalink: /cli/2ko7a68q/
---

## 坚果云


:::code-tabs
@tab bash
```shell :collapsed-lines
#!/usr/bin/env bash

# 固定密码
PASSWORD="adaqcm4m5ujvpewb"
# WebDAV 基础地址
BASE_URL="https://dav.jianguoyun.com/dav/files/"

usage() {
    echo "用法:"
    echo "  上传: $0 <账号> -u <localfile>"
    echo "  下载: $0 <账号> -d <remotefile>"
    echo "  删除: $0 <账号> -r <remotefile>"
    exit 1
}

if [ $# -lt 3 ]; then
    usage
fi

ACCOUNT="$1"
ACTION="$2"

case "$ACTION" in
    -u) # 上传
        LOCALFILE="$3"
        if [ ! -f "$LOCALFILE" ]; then
            echo "错误: 本地文件 $LOCALFILE 不存在"
            exit 1
        fi
        FILENAME=$(basename "$LOCALFILE")
        echo "正在上传 $LOCALFILE 到 ${BASE_URL}${FILENAME} ..."
        curl --user "$ACCOUNT:$PASSWORD" -T "$LOCALFILE" "${BASE_URL}${FILENAME}"
        ;;
    -d) # 下载
        REMOTEFILE="$3"
        echo "正在下载 ${REMOTEFILE} 到 ./${REMOTEFILE} ..."
        curl --user "$ACCOUNT:$PASSWORD" "${BASE_URL}${REMOTEFILE}" -o "./${REMOTEFILE}"
        ;;
    -r) # 删除
        REMOTEFILE="$3"
        echo "正在删除远程文件 ${BASE_URL}${REMOTEFILE} ..."
        curl --user "$ACCOUNT:$PASSWORD" -X DELETE "${BASE_URL}${REMOTEFILE}"
        ;;
    *)
        usage
        ;;
esac
```
@tab ash
```shell :collapsed-lines
#!/bin/sh

# 固定密码
PASSWORD="adaqcm"
# WebDAV 基础地址
BASE_URL="https://dav.jianguoyun.com/dav/files/"

usage() {
    echo "用法:"
    echo "  上传: $0 <账号> -u <localfile>"
    echo "  下载: $0 <账号> -d <remotefile>"
    echo "  删除: $0 <账号> -r <remotefile>"
    exit 1
}

if [ $# -lt 3 ]; then
    usage
fi

ACCOUNT="$1"
ACTION="$2"

get_basename() {
    # BusyBox sh 版本 basename
    echo "${1##*/}"
}

case "$ACTION" in
    -u) # 上传
        LOCALFILE="$3"
        if [ ! -f "$LOCALFILE" ]; then
            echo "错误: 本地文件 $LOCALFILE 不存在"
            exit 1
        fi
        FILENAME=$(get_basename "$LOCALFILE")
        echo "正在上传 $LOCALFILE 到 ${BASE_URL}${FILENAME} ..."
        curl --user "$ACCOUNT:$PASSWORD" -T "$LOCALFILE" "${BASE_URL}${FILENAME}"
        ;;
    -d) # 下载
        REMOTEFILE="$3"
        echo "正在下载 ${REMOTEFILE} 到 ./${REMOTEFILE} ..."
        curl --user "$ACCOUNT:$PASSWORD" "${BASE_URL}${REMOTEFILE}" -o "./${REMOTEFILE}"
        ;;
    -r) # 删除
        REMOTEFILE="$3"
        echo "正在删除远程文件 ${BASE_URL}${REMOTEFILE} ..."
        curl --user "$ACCOUNT:$PASSWORD" -X DELETE "${BASE_URL}${REMOTEFILE}"
        ;;
    *)
        usage
        ;;
esac
```
:::

### 使用
::: code-tabs
@tab bash
```shell
# 上传
bash scripts.sh <账号> -u 本地文件
# 下载
bash scripts.sh <账号> -d 远程文件名（不要路径）
# 删除坚果云文件
bash scripts.sh <账号> -r 远程文件名（不要路径）
```
@tab ash
```shell
# 上传
sh scripts.sh <账号> -u 本地文件
```
:::

PS  
- 下载默认放在当前目录
- 上传可以指定路径，下载只需要指定文件名（删除同理）
