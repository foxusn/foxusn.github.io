+++
date = '2025-05-10T18:22:43+08:00'
draft = false
title = 'SSH 笔记'
summary = 'SSH（Secure Shell） 相关笔记'
tags = [ "SSH", "GitHub", "Linux" ]
keywords = [ "SSH", "GitHub" ]
ShowToc = false
pin = true
+++


## 检查 openssh 是否已安装

```bash
dnf list installed openssh
which ssh                       # 输出 /usr/sbin/ssh
systemctl status sshd
```

## 生成 ed25519 密钥对

```bash
ssh-keygen -t ed25519 -C "your_email@example.com" -f ~/.ssh/github_ed25519 -N ""
# ~/.ssh 如果不存在会自动创建；-N 参数设置 passphrase 为空
```

## 添加到 SSH agent

```bash
eval "$(ssh-agent -s)"         # 启动 SSH Agent（后台进程）
ssh-add ~/.ssh/github_ed25519  # 把 SSH 私钥添加进 SSH agent，让系统记住它
```

## 测试 SSH 连接

```bash
ssh-add -l                     # 检查本地 SSH key
ssh -T git@github.com          # 测试 SSH 连接
```
