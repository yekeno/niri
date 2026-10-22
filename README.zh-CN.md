[English](README.md) | **简体中文**

<h1 align="center"><img alt="niri" src="https://github.com/user-attachments/assets/07d05cd0-d5dc-4a28-9a35-51bae8f119a0"></h1>
<p align="center">一个可滚动平铺的 Wayland 合成器。</p>
<p align="center">
    <a href="https://matrix.to/#/#niri:matrix.org"><img alt="Matrix" src="https://img.shields.io/badge/matrix-%23niri-blue?logo=matrix"></a>
    <a href="https://github.com/niri-wm/niri/blob/main/LICENSE"><img alt="GitHub License" src="https://img.shields.io/github/license/niri-wm/niri"></a>
    <a href="https://github.com/niri-wm/niri/releases"><img alt="GitHub Release" src="https://img.shields.io/github/v/release/niri-wm/niri?logo=github"></a>
</p>

<p align="center">
    <a href="https://niri-wm.github.io/niri/Getting-Started.html">快速开始</a> | <a href="https://niri-wm.github.io/niri/Configuration%3A-Introduction.html">配置</a> | <a href="https://github.com/niri-wm/niri/discussions/325">配置展示</a>
</p>

<img width="1280" height="720" alt="niri 打开了几个窗口" src="https://github.com/user-attachments/assets/dea5909e-1859-4aaa-9d88-d37f9663e00b" />

## yekeno 分支：中文输入法的光标 IPC

本分支在上游 niri（v26.04-192-g4263c9a1）之上增加了一个 `TextInputRect`
IPC 请求。它以输出逻辑坐标返回当前焦点文本输入的光标矩形，使外部
fcitx5/Rime 候选窗能在 Wayland 上跟随光标。

```text
→ "TextInputRect"
← {"Ok":{"TextInputRect":{"x":812,"y":244,"width":2,"height":18}}}
```

该功能由 **[rime-popup](https://github.com/yekeno/rime-popup)** 使用：这是一个
layer-shell 守护进程，在光标下方绘制带序号的 fcitx5 候选词。它还需要一个小的
[smithay 分支](https://github.com/yekeno/smithay/tree/niri-text-input-rect)
来暴露光标矩形；本仓库的 `[patch]` 段会自动指向它。

- 完整设计、数据流、构建与用法：[`docs/text-input-rect.zh-CN.md`](docs/text-input-rect.zh-CN.md)
- 配套项目：https://github.com/yekeno/rime-popup
- 验证环境：Ubuntu 22.04.5 LTS、Wayland、fcitx5 5.0.14 + fcitx5-rime

## 关于

窗口以列的形式排列在一条向右无限延伸的条带上。打开新窗口永远不会导致已有
窗口改变大小。

每个显示器都有自己独立的窗口条带。窗口永远不会“溢出”到相邻显示器。

工作区是动态的，并垂直排列。每个显示器有独立的工作区集合，并且始终在最下方
保留一个空工作区。

在显示器断开和重新连接时，工作区布局会尽可能保留。显示器断开时，它的工作区
会移到另一个显示器；重新连接后，它们会回到原来的显示器。

## 特性

- 从零开始为可滚动平铺设计
- 类似 GNOME 的[动态工作区](https://niri-wm.github.io/niri/Workspaces.html)
- 可缩放工作区和窗口的[概览](https://github.com/user-attachments/assets/379a5d1f-acdb-4c11-b36c-e85fd91f0995)
- 内置截图 UI
- 通过 xdg-desktop-portal-gnome 进行显示器和窗口录屏
    - 可以[屏蔽](https://niri-wm.github.io/niri/Configuration%3A-Window-Rules.html#block-out-from)敏感窗口，使其不出现在录屏中
    - [动态投屏目标](https://niri-wm.github.io/niri/Screencasting.html#dynamic-screencast-target)可在运行中切换内容
- [触摸板](https://github.com/niri-wm/niri/assets/1794388/946a910e-9bec-4cd1-a923-4a9421707515)与[鼠标](https://github.com/niri-wm/niri/assets/1794388/8464e65d-4bf2-44fa-8c8e-5883355bd000)手势
- 将窗口组合为[标签页](https://niri-wm.github.io/niri/Tabs.html)
- 可配置布局：间距、边框、struts、窗口尺寸
- 支持 Oklab 和 Oklch 的[渐变边框](https://niri-wm.github.io/niri/Configuration%3A-Layout.html#gradients)
- 窗口和 layer-shell 表面的[背景模糊](https://niri-wm.github.io/niri/Window-Effects.html)
- [动画](https://github.com/niri-wm/niri/assets/1794388/ce178da2-af9e-4c51-876f-8709c241d95e)，支持[自定义着色器](https://github.com/niri-wm/niri/assets/1794388/27a238d6-0a22-4692-b794-30dc7a626fad)
- 配置实时重载
- 支持[屏幕阅读器](https://niri-wm.github.io/niri/Accessibility.html)

## 视频演示

https://github.com/niri-wm/niri/assets/1794388/bce834b0-f205-434e-a027-b373495f9729

也可以看看这些展示 niri 大量功能的视频：

- [Niri Is My New Favorite Wayland Compositor](https://www.youtube.com/watch?v=DeYx2exm04M)，作者 Brodie Robertson
- [How Is niri This Good? Live Demo + Config](https://www.youtube.com/watch?v=7XmD5UyyhZQ)，作者 Nick Janetakis

## 状态

niri 已足够稳定，可用于日常使用，并实现了 Wayland 合成器的大多数常见功能。
许多人把 niri 作为日常主力，并乐意在 [Matrix 频道]中提供帮助。

试试看吧！
按照[快速开始](https://niri-wm.github.io/niri/Getting-Started.html)页面的说明
操作。再搭配一个桌面 shell，例如 [DankMaterialShell] 或 [Noctalia]（也可以
搭建更传统的环境）：niri 本身并不是完整的桌面环境。
另外可以看看 [awesome-niri]，这是一个 niri 相关链接和项目的列表。

以下是一些你可能关心的问题：

- **多显示器**：支持，这是从一开始就存在的核心设计。混合 DPI 也可用。
- **分数缩放**：支持，并且 niri 的所有 UI 都保持像素级清晰。
- **NVIDIA**：似乎可以正常工作。
- **浮动窗口**：支持，从 niri 25.01 开始。
- **输入设备**：niri 支持数位板、触摸板和触摸屏。
可以把数位板映射到指定显示器，或使用 [OpenTabletDriver]。
我们支持触摸板手势，但暂不支持触摸屏手势。
- **Wlr 协议**：支持，包括 layer-shell、gamma-control、screencopy 等大多数
重要协议。可以在 [wayland.app](https://wayland.app) 每个协议页面底部查看
支持情况。
- **性能**：虽然我在性能较强的机器上运行 niri，但我一直注意性能表现。
我见过有人在 2008 年的 Eee PC 900 上流畅使用它。
- **Xwayland**：从 niri 25.08 开始，通过 xwayland-satellite
[集成](https://niri-wm.github.io/niri/Xwayland.html#using-xwayland-satellite)。

## 媒体

[niri: Making a Wayland compositor in Rust](https://youtu.be/Kmz8ODolnDg?list=PLRdS-n5seLRqrmWDQY4KDqtRMfIwU0U3T) · *2024 年 12 月*

我在 2024 年莫斯科 RustCon 上关于 niri 的演讲，介绍了如何进行随机属性测试和
性能分析，以及如何测量输入延迟。演讲为俄语，但我准备了完整的英文字幕，
可在 YouTube 的字幕语言选择器中找到。

[An interview with Ivan, the developer behind Niri](https://www.trommelspeicher.de/podcast/special_the_developer_behind_niri) · *2025 年 6 月*

德国科技播客 Das Triumvirat 的采访（英语）。我们聊了 niri 的开发和历史，
以及我构建和维护 niri 的经历。

[A tour of the niri scrolling-tiling Wayland compositor](https://lwn.net/Articles/1025866/) · *2025 年 7 月*

一篇 LWN 文章，对 niri 做了很好的概述和介绍。

[How to test a Wayland compositor?](https://youtu.be/w44fYK5z418?list=PLK4NE4dSsLlw) · *2026 年 10 月*

我关于 niri 中一些测试技术的演讲：属性测试、快照测试、客户端-服务端测试。
前半部分与 RustCon 演讲重叠，后半部分是新内容。演讲为俄语，但我准备了完整
的英文字幕，可在 YouTube 的字幕语言选择器中找到。

## 贡献

如果你想帮助 niri，有很多编码和非编码的方式。概览见
[CONTRIBUTING.md](https://github.com/niri-wm/niri/blob/main/CONTRIBUTING.md)。

## 灵感来源

niri 深受 [PaperWM] 启发，后者在 GNOME Shell 之上实现了可滚动平铺。

促使我尝试编写自己的合成器的原因之一，是能够正确地分离显示器。
作为 GNOME Shell 扩展，PaperWM 必须对抗 Shell 的全局窗口坐标空间，以防止
窗口溢出。

## 其他可滚动平铺项目

以下项目实现了类似的工作流：

- [PaperWM]：GNOME Shell 之上的可滚动平铺。
- [karousel]：KDE 之上的可滚动平铺。
- [scroll](https://github.com/dawsers/scroll) 和 [papersway]：sway/i3 之上的可滚动平铺。
- Hyprland 内置了[滚动布局](https://wiki.hypr.land/Configuring/Layouts/Scrolling-Layout/)。
- [Paneru] 和 [PaperWM.spoon]：macOS 之上的可滚动平铺。

## 联系

我们的主要交流渠道是 Matrix 聊天，欢迎加入提问：https://matrix.to/#/#niri:matrix.org

我们还有一个社区 Discord 服务器：https://discord.gg/vT8Sfjy7sx

[PaperWM]: https://github.com/paperwm/PaperWM
[waybar]: https://github.com/Alexays/Waybar
[fuzzel]: https://codeberg.org/dnkl/fuzzel
[awesome-niri]: https://github.com/niri-wm/awesome-niri
[karousel]: https://github.com/peterfajdiga/karousel
[papersway]: https://spwhitton.name/tech/code/papersway/
[Paneru]: https://github.com/karinushka/paneru
[PaperWM.spoon]: https://github.com/mogenson/PaperWM.spoon
[Matrix 频道]: https://matrix.to/#/#niri:matrix.org
[OpenTabletDriver]: https://opentabletdriver.net/
[DankMaterialShell]: https://danklinux.com/
[Noctalia]: https://noctalia.dev/
