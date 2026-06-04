---
title: Mac右键neovim编辑配置
tags:
  - 右键
  - neovim
createTime: 2026/06/04 15:53:30
permalink: /blog/ejw2at23/
---

# 全能右键配置
简介
--

> 全能右键是 Mac 上的一款自定义右键功能的 APP

新建文件
----

```text-x-sh
#!/bin/bash
BASE_NAME="新建文件"
folder_name="$BASE_NAME"

# 检查基础文件是否存在
if [ -f "$PATH/$folder_name" ]; then
    counter=2
    # 查找下一个可用的编号
    while [ -f "$PATH/$BASE_NAME $counter" ]; do
        ((counter++))
    done
    folder_name="$BASE_NAME $counter"
fi

# 创建文件
touch "$PATH/$folder_name"
```

新建文件夹
-----

```text-x-sh
#!/bin/bash
BASE_NAME="未命名文件夹"
folder_name="$BASE_NAME"
counter=2

# 检查基础文件夹是否存在
if [ -d "$PATH/$folder_name" ]; then
    # 查找下一个可用的编号
    while [ -d "$PATH/$BASE_NAME $counter" ]; do
        ((counter++))
    done
    folder_name="$BASE_NAME $counter"
fi

# 创建文件夹
mkdir -p "$PATH/$folder_name"
```

Edit with Neovim
----------------

```text-x-sh
#!/bin/bash

# 启动 wezterm
/Applications/WezTerm.app/Contents/MacOS/wezterm start /opt/homebrew/bin/nvim "$PATH" &

# 后台检测并置顶
{
    for i in {1..10}; do
        sleep 0.5
        if osascript -e 'application "WezTerm" is running' 2>/dev/null | grep -q "true"; then
            osascript -e 'tell application "WezTerm" to activate'
            break
        fi
    done
} &
```

在此打开 Wezterm
------------

```text-x-sh
#!/bin/bash

# 启动 wezterm
/Applications/WezTerm.app/Contents/MacOS/wezterm start --cwd "$PATH" &

# 后台检测并置顶
{
    for i in {1..10}; do
        sleep 0.5
        if osascript -e 'application "WezTerm" is running' 2>/dev/null | grep -q "true"; then
            osascript -e 'tell application "WezTerm" to activate'
            break
        fi
    done
} &
```

图标
--

> 给这些右键功能指定菜单图标

新建文件和新建菜单文件从 => `` /System/Library/CoreServices/CoreTypes.bundle/Contents/Resources` `` 复制出来并使用，它们分别为：`GenericDocumentIcon.icns` 和 `GenericFolderIcon.icns`

**wezterm**

> 来源于官网 https://wezterm.org

从官方以检查提取也就是 https://wezterm.org/favicon.svg

```text-x-sh
<?xml version="1.0" encoding="UTF-8" standalone="no"?>
<svg xmlns:dc="http://purl.org/dc/elements/1.1/" xmlns:cc="http://creativecommons.org/ns#" xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#" xmlns:svg="http://www.w3.org/2000/svg" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:sodipodi="http://sodipodi.sourceforge.net/DTD/sodipodi-0.dtd" xmlns:inkscape="http://www.inkscape.org/namespaces/inkscape" width="55.010815mm" height="55mm" viewBox="0 0 55.010814 55" version="1.1" id="svg8" inkscape:version="1.0.1 (c497b03c, 2020-09-10)" sodipodi:docname="wezterm-icon.svg" inkscape:export-filename="/Users/wez/Documents/wezterm-icon.png" inkscape:export-xdpi="59.112728" inkscape:export-ydpi="59.112728">
  <defs id="defs2">
    <linearGradient inkscape:collect="always" id="linearGradient1113">
      <stop style="stop-color:#2b383f;stop-opacity:1" offset="0" id="stop1109"/>
      <stop style="stop-color:#172024;stop-opacity:1" offset="1" id="stop1111"/>
    </linearGradient>
    <inkscape:path-effect effect="fillet_chamfer" id="path-effect943" is_visible="true" lpeversion="1" satellites_param="F,0,0,1,0,2.6458333,0,1 @ F,0,0,1,0,2.6458333,0,1 @ F,0,0,1,0,0,0,1 @ F,0,0,1,0,0,0,1" unit="px" method="auto" mode="F" radius="10" chamfer_steps="1" flexible="false" use_knot_distance="true" apply_no_radius="true" apply_with_radius="true" only_selected="false" hide_knots="false"/>
    <inkscape:path-effect effect="fillet_chamfer" id="path-effect939" is_visible="true" lpeversion="1" satellites_param="F,0,0,1,0,0,0,1 @ F,0,0,1,0,0,0,1 @ F,0,0,1,0,0,0,1 @ F,0,0,1,0,0,0,1" unit="px" method="auto" mode="C" radius="10" chamfer_steps="1" flexible="false" use_knot_distance="true" apply_no_radius="true" apply_with_radius="true" only_selected="true" hide_knots="false"/>
    <inkscape:path-effect effect="fillet_chamfer" id="path-effect934" is_visible="true" lpeversion="1" satellites_param="F,1,0,1,0,0.1,0,1 @ F,1,0,1,0,0.1,0,1 @ F,1,0,1,0,0.1,0,1 @ F,1,0,1,0,0.1,0,1" unit="px" method="auto" mode="F" radius="10" chamfer_steps="1" flexible="true" use_knot_distance="true" apply_no_radius="true" apply_with_radius="true" only_selected="false" hide_knots="false"/>
    <linearGradient inkscape:collect="always" id="linearGradient905">
      <stop style="stop-color:#ff00ff;stop-opacity:1;" offset="0" id="stop901"/>
      <stop style="stop-color:#ff00ff;stop-opacity:0;" offset="1" id="stop903"/>
    </linearGradient>
    <inkscape:path-effect effect="fillet_chamfer" id="path-effect3137" is_visible="true" lpeversion="1" satellites_param="F,1,0,1,0,0.1,0,1 @ F,1,0,1,0,0.1,0,1 @ F,1,0,1,0,0.1,0,1 @ F,1,0,1,0,0.1,0,1" unit="px" method="auto" mode="F" radius="10" chamfer_steps="1" flexible="true" use_knot_distance="true" apply_no_radius="true" apply_with_radius="true" only_selected="false" hide_knots="false"/>
    <inkscape:path-effect effect="fillet_chamfer" id="path-effect2756" is_visible="true" lpeversion="1" satellites_param="F,1,0,1,0,0.2,0,1 @ F,1,0,1,0,0.2,0,1 @ F,1,0,1,0,0.2,0,1 @ F,1,0,1,0,0.2,0,1" unit="px" method="auto" mode="F" radius="20" chamfer_steps="1" flexible="true" use_knot_distance="true" apply_no_radius="true" apply_with_radius="true" only_selected="false" hide_knots="false"/>
    <linearGradient inkscape:collect="always" xlink:href="#linearGradient905" id="linearGradient907" x1="39.079655" y1="72.459702" x2="90.17334" y2="72.459702" gradientUnits="userSpaceOnUse"/>
    <linearGradient inkscape:collect="always" xlink:href="#linearGradient1113" id="linearGradient1115" x1="66.095612" y1="43.676846" x2="66.095612" y2="98.112801" gradientUnits="userSpaceOnUse"/>
  </defs>
  <sodipodi:namedview id="base" pagecolor="#ffffff" bordercolor="#666666" borderopacity="1.0" inkscape:pageopacity="0.0" inkscape:pageshadow="2" inkscape:zoom="2.8190618" inkscape:cx="85.466562" inkscape:cy="106.8872" inkscape:document-units="mm" inkscape:current-layer="layer1" inkscape:document-rotation="0" showgrid="false" inkscape:window-width="1252" inkscape:window-height="847" inkscape:window-x="54" inkscape:window-y="25" inkscape:window-maximized="0" fit-margin-top="0" fit-margin-left="0" fit-margin-right="0" fit-margin-bottom="0"/>
  <metadata id="metadata5">
    <rdf:RDF>
      <cc:Work rdf:about="">
        <dc:format>image/svg+xml</dc:format>
        <dc:type rdf:resource="http://purl.org/dc/dcmitype/StillImage"/>
        <dc:title/>
        <dc:creator>
          <cc:Agent>
            <dc:title>Wez Furlong</dc:title>
          </cc:Agent>
        </dc:creator>
      </cc:Work>
    </rdf:RDF>
  </metadata>
  <g inkscape:label="Layer 1" inkscape:groupmode="layer" id="layer1" transform="translate(-37.656612,-43.207115)">
    <path style="opacity:1;fill:url(#linearGradient1115);fill-opacity:1;stroke:none;stroke-width:7.01263;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:4;stroke-dasharray:none" id="rect10" width="55" height="55" x="37.656612" y="43.207115" sodipodi:type="rect" d="m 48.656612,43.207115 h 33 a 11,11 45 0 1 11,11 v 33 a 11,11 135 0 1 -11,11 h -33 a 11,11 45 0 1 -11,-11 v -33 a 11,11 135 0 1 11,-11 z" inkscape:path-effect="#path-effect2756"/>
    <g aria-label="$W" id="text3144" style="font-style:normal;font-variant:normal;font-weight:normal;font-stretch:normal;font-size:47.9778px;line-height:1.25;font-family:'Operator Mono';-inkscape-font-specification:'Operator Mono';fill:#4e49ee;fill-opacity:1;stroke-width:0.264583" transform="matrix(0.84051205,0,0,0.84423619,11.628829,8.3486634)">
      <path d="m 47.07925,66.906972 c 0,-1.247423 1.247423,-2.015068 4.270024,-2.015068 l -1.007534,5.517447 c -1.871134,-1.247423 -3.26249,-2.39889 -3.26249,-3.502379 z m 8.06027,13.625694 c 0,1.295401 -1.295401,2.159001 -4.270024,2.302935 l 1.055511,-5.853292 c 1.871135,1.247423 3.214513,2.350912 3.214513,3.550357 z m -5.277558,11.99445 0.911578,-5.421491 c 7.244648,-0.67169 10.075338,-3.598335 10.075338,-6.812848 0,-3.310468 -4.030135,-5.901269 -7.724426,-8.156225 l 1.343379,-7.100715 c 1.535289,0.143934 3.358446,0.431801 5.517447,0.863601 l 0.623711,-4.941713 C 58.977744,60.717836 57.442454,60.62188 56.00312,60.525924 l 1.10349,-5.277558 -4.749802,-0.04798 -0.911579,5.373513 c -7.244647,0.575734 -10.075337,3.598335 -10.075337,6.812847 0,3.262491 4.030135,5.757336 7.724425,7.916337 l -1.343378,7.436559 c -1.727201,-0.09596 -3.838224,-0.383822 -6.285092,-0.815623 l -0.959556,4.941714 c 2.063046,0.239889 3.982158,0.383822 5.709358,0.4318 l -1.055511,5.181602 z" style="font-style:normal;font-variant:normal;font-weight:normal;font-stretch:normal;font-size:47.9778px;font-family:'Operator Mono';-inkscape-font-specification:'Operator Mono';fill:#4e49ee;fill-opacity:1;stroke-width:0.264583" id="path854"/>
      <path d="m 81.132992,88.73687 h 5.373513 c 0.671689,-5.613403 1.631245,-16.936163 2.254957,-29.746235 h -5.133625 c -0.143933,3.022601 -0.671689,21.014275 -0.8636,22.501587 h -0.143934 c -1.2954,-4.845757 -2.350912,-8.779937 -3.646312,-13.577717 h -2.926646 c -1.247423,4.79778 -2.111023,8.396115 -3.406424,13.577717 H 72.44901 C 72.305077,80.00491 71.489454,62.013236 71.393499,58.990635 h -5.325536 c 0.623711,12.810072 1.53529,24.132832 2.206979,29.746235 H 73.5525 l 3.69429,-14.249406 z" style="font-style:normal;font-variant:normal;font-weight:normal;font-stretch:normal;font-size:47.9778px;font-family:'Operator Mono';-inkscape-font-specification:'Operator Mono';fill:#4e49ee;fill-opacity:1;stroke-width:0.264583" id="path856"/>
    </g>
  </g>
</svg>
```

**Neovim**

> 来源于官网 https://neovim.io/

```text-x-sh
<svg xmlns="http://www.w3.org/2000/svg" width="173" height="50" viewBox="0 0 305 214" aria-label="Neovim">
  <title>Neovim</title>
  <defs>
    <linearGradient x1="50%" y1="0" x2="50%" y2="100%" id="a">
      <stop stop-color="#16B0ED" stop-opacity=".8" offset="0"></stop>
      <stop stop-color="#0F59B2" stop-opacity=".837" offset="100%"></stop>
    </linearGradient>
    <linearGradient x1="50%" y1="0" x2="50%" y2="100%" id="b">
      <stop stop-color="#7DB643" offset="0"></stop>
      <stop stop-color="#367533" offset="100%"></stop>
    </linearGradient>
    <linearGradient x1="50%" y1="0" x2="50%" y2="100%" id="c">
      <stop stop-color="#88C649" stop-opacity=".8" offset="0"></stop>
      <stop stop-color="#439240" stop-opacity=".84" offset="100%"></stop>
    </linearGradient>
  </defs>
  <g fill="none" fill-rule="evenodd">
    <!-- 只保留左侧的立体Logo部分 -->
    <path d="M.027 45.459 45.224-.173v212.171L.027 166.894V45.459z" fill="url(#a)" transform="translate(1 1)"></path>
    <path d="M129.337 45.89 175.152-.149l-.928 212.146-45.197-45.104.31-121.005z" fill="url(#b)" transform="matrix(-1 0 0 1 305 1)"></path>
    <path d="M45.194-.137 162.7 179.173l-32.882 32.881L12.25 33.141 45.194-.137z" fill="url(#c)" transform="translate(1 1)"></path>
    <path d="M46.234 84.032l-.063 7.063-36.28-53.563 3.36-3.422 32.983 49.922z" fill-opacity=".13" fill="#000"></path>
    <!-- 已移除所有文字部分 -->
  </g>
</svg>
```
