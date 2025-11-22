---
title: 关于我踩到的 1Password 的 SSH Agent 的坑……
published: 2025-11-22
tags: []
description: 修复 1Password SSH Agent 在 Windows 上不正常工作的问题
category: Windows
draft: false
---


> 众所周知， [1Password](https://1password.com/) 是一款十分好用的密码管理器

在我这新笔记本配置 1Password SSH Agent 的时候，`ssh -T git@github.com` 总是不通……

重新按照[说明](https://developer.1password.com/docs/ssh/get-started/)配置了一遍，仍然输出 `git@github.com: Permission denied (publickey).`

但是可以正常用里面的 ssh 密钥签名 git commit ，因此怀疑是 OpenSSH 的配置出问题了。

查询一番后发现，在 `~/.ssh/config` 里加入这两行即可：

```
Host *
    IdentityAgent "\\\\.\\pipe\\openssh-ssh-agent"
```

> `\\.\pipe\openssh-ssh-agent` 是 Windows 上 OpenSSH 实现中的一个命名管道，它充当了与后台运行的 SSH 密钥管理代理 (SSH Agent) 通信的接口。

而 1Password SSH Agent 就是取代了这个 `\\.\pipe\openssh-ssh-agent` 来工作的，虽然我也不太清楚为什么 OpenSSH 原来不走这个管道……
