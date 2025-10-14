# Fcitx5 Steam IBus Frontend

A fcitx5 frontend developed for Steam Big Picture/SteamOS/Steam Deck users.

一个 fcitx5 前端，为 Steam 大屏幕/SteamOS/Steam Deck 用户开发。

## 安装

### 通过 AUR

如果您是 Arch Linux 用户，推荐使用 AUR 包安装。

对于常见的 AUR 助手 `yay`，执行以下命令即可安装：

```bash
yay -S fcitx5-steam-ibus-frontend
```

### Flatpak

先确保拥有 Flatpak 环境且已安装好 `org.fcitx.Fcitx5`

执行：

```bash
flatpak install --user --no-gpg-verify https://chenx-dust.github.io/fcitx5-steam-ibus-frontend/org.fcitx.Fcitx5.Addon.SteamIBusFrontend.flatpakref
```

### 手动安装

请先确保已经安装了 Git，CMake 和 GCC。

```bash
git clone https://github.com/chenx-dust/fcitx5-steam-ibus-frontend.git
cd fcitx5-steam-ibus-frontend
mkdir build && cd build
cmake ..
make
sudo make install
```

如果在后面步骤 fcitx5 无法找到 `libsteamibusfrontend.so` ，可能需要删除 `build` 文件夹，将 CMake 命令替换为：

```bash
cmake -DCMAKE_INSTALL_PREFIX=/usr -DCMAKE_INSTALL_LIBDIR=/usr/lib ..
```

重新进行编译与安装。

## 使用

**首先**，应当利用 `fcitx5-configtool` 或者其他工具，将需要使用的输入法加入进默认的输入法组中。

需要注意的是，使用本插件时应当禁用自带的 ibusfrontend 前端，否则会产生冲突。

### 手动启动

在进入 Steam 大屏幕后，利用 SSH 等方式启动，命令为：

```bash
export DISPLAY=:1   # 大多数情况，按需调整为 Steam 大屏幕所在的 DISPLAY
fcitx5 --enable steamibusfrontend --disable ibusfrontend -r
```

### Systemd 启动

（暂无）

## 兼容性

目前确认 `fcitx5-chinese-addons` 完全兼容。其他输入法可能有无法翻页、无法选择候选词等问题，请反馈。目前确认简体中文（拼音）、日语、韩语具有完全自由的输入法切换功能，其他输入法可能无法自由切换，只能在纯字母键盘和启用输入法的键盘中切换，可以通过默认输入法组的默认输入法进行配置。

## 授权

本项目基于 fcitx5 的 ibusfrontend 源代码修改而来，继承其授权协议 LGPL-2.1-or-later 。
