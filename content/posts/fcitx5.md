+++
# date = '2025-04-06T22:04:04+08:00'
date = '2025-04-07T15:41:59+08:00'
draft = false
title = 'Fedora 安装中文输入法（Fcitx 5）'
# weight = 2
categories = ["Linux"]
tags = ["Fcitx", "IME", "Linux"]
keywords = [ "fcitx", "fcitx5", "输入法" ]
summary = 'Fedora Linux (Workstation) 上安装 Fcitx 5 框架并配置中文输入法'
pin = true
+++

不想折腾的直接使用系统自带的 IBus，添加一个智能拼音输入法，再安装一个 IBus Tweaker 扩展进行简单配置即可，缺点是词库不太行；ibus-rime 就没必要了，建议直接 Fcitx 5

## 安装 [Fcitx 5](https://fcitx-im.org/wiki/Install_Fcitx_5/zh-cn)

安装 Fcitx 5 主程序和一些相关的模块，参考 [I18N/Fcitx5](https://fedoraproject.org/wiki/I18N/Fcitx5)

```bash
sudo dnf install fcitx5 fcitx5-chinese-addons fcitx5-configtool fcitx5-rime fcitx5-qt fcitx5-gtk fcitx5-autostart.noarch
sudo dnf remove "fcitx5*"   # 这是卸载命令
```

## 下载词库

[雾凇拼音](https://github.com/iDvel/rime-ice)——长期维护的简体词库

```bash
# 创建文件夹（如果不存在）
mkdir -p ~/.local/share/fcitx5/rime/
# 克隆雾凇拼音这个Rime配置到本地（我克隆到了 ~/Downloads 目录）
git clone https://github.com/iDvel/rime-ice.git rime --depth 1
# 复制上面克隆到本地的文件夹内的所有文件到刚创建的文件夹
cp ~/Downloads/rime/* ~/.local/share/fcitx5/rime
```


## 简单配置

- 通过快捷键选择输入方案

- 修改每页候选词个数

编辑 ***~/.local/share/fcitx5/rime/default.yaml*** 文件，修改 `page_size` 这行：

```yaml
# ~/.local/share/fcitx5/rime/default.yaml
page_size: 9
```

- 隐藏拼音注释

候选框默认会显示拼音注释，比如：你好[ni hao]，我使用小鹤双拼，所以编辑 ***~/.local/share/fcitx5/rime/double_pinyin_flypy.schema.yaml***，注释下面这两行：

```yaml
# ~/.local/share/fcitx5/rime/double_pinyin_flypy.schema.yaml
spelling_hints: 8
always_show_comments: true
```

- 添加 Rime

打开 Fcitx5 Configuration 这个图形化工具添加 Rime

- 环境变量

编辑 ***~/.bash_profile***，添加下面三行：

```bash
export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
export XMODIFIERS=@im=fcitx
```

- 重新加载配置

通过 Gnome Tweaks 设置开机启动，重新登录或者重启，然后打字测试

- Gnome 扩展

安装 Input Method Panel 扩展以实现 UI 统一、托盘显示输入法图标、调整候选词字号等 🔚
