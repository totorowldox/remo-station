---
title: Windows Terminal 的初始美化
published: 2025-11-22
tags: []
description: 关于新安装的 Windows Terminal 的美化……
category: Windows
draft: false
---


> 前言：最近新买的笔记本预装了 Windows 11 ，虽然我确实很想装上 NixOS ，但是~~暂时~~懒得折腾了啊哈哈

## 1. 安装 [Starship](https://starship.rs/) 

### 1.1 下载 Starship
<details> 
<summary>使用 winget</summary>

```ps
winget install --id Starship.Starship
```
</details>

<details> 
<summary>使用 chocolatey</summary>

```ps
choco install starship
```
</details>

### 1.2 创建 Windows Terminal 的 profile

```ps
New-Item -ItemType File -Path $PROFILE -Force 
```

使用文本编辑器修改 `$PROFILE` ，加入
```ps
Invoke-Expression (&starship init powershell)
```
如果 Windows Terminal 是新安装的，此时 `$PROFILE` 应该只有一行

### 1.3 使用一个预设
因为我自己用 Catppuccin 比较久，所以在这里也直接用上了
```ps
New-Item -ItemType Directory -Path $env:USERPROFILE/.config
starship preset catppuccin-powerline -o $env:USERPROFILE/.config/starship.toml
```

## 2. 设置 Windows Terminal
### 2.1 字体
安装 [Maple Mono](https://github.com/subframe7536/maple-font)

然后在 Windows Terminal 的设置->默认值->外观->字体 设置
### 2.2 自定义配色
设置左下角打开 JSON 文件，
在 `"schemes": []` 里加入配色选项

配色选项可以从[这里](https://windowsterminalthemes.dev/)获取

同样在 Windows Terminal 的设置->默认值->外观->配色 设置
### 2.3 删除烦人的开幕词！
<details>
<summary>这简直烦透了！</summary>

> Windows PowerShell </br>
版权所有（C） Microsoft Corporation。保留所有权利。</br>
安装最新的 PowerShell，了解新功能和改进！https://aka.ms/PSWindows

</details>

在 Windows Terminal 的设置-> Windows PowerShell ->命令行 中加入 `-NoLogo` 选项即可

现在命令行应该长得像 `%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe -NoLogo`

## 3. 安装自动补全
在 PowerShell（管理员） 中运行 `Install-Module PSReadLine -Force` 即可！

## 4. 以后的工作
- 安装 zoxide, fzf, yazi 等工具

## 现在你的 Windows Terminal 应该长得像这样了！
![Preview](https://i.imgur.com/ZctW35B.png)