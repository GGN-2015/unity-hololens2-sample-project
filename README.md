# 如何创建一个 Hololens2 示例项目

本节内容将为你介绍此项目是如何创建而成的。本项目使用 Hololens2 以及 MRTK3 创建一个示例项目。
- 参考教程：https://learn.microsoft.com/en-us/training/paths/beginner-hololens-2-tutorials/

## 基本步骤

> [!IMPORTANT]
> 目前，直接使用 Visual Studio Installer 已经无法安装 Visual Stduio 2022 的社区版，因此请使用 Unity Hub 的安装功能，为你使用的 Unity Editor 配备合适版本的 Visual Studio

1. 安装 Unity Hub
    - 安装 Unity Editor 版本：`2022.3.62f3c1 LTS`
    - **注意**，如果你使用了 `Unity Editor 2022.3.62f3c1 LTS`，在这个阶段，请额外安装 Visual Studio 2022，新于这个版本的 Visual Studio 是无法用于编译此版本 Unity 的项目的。
    - 在 Unity Hub -> Installs 找到指定版本的 Unity Editor 再点击其选项卡右上角的齿轮
        - 至少在其中添加 VS2022, UWP Build Support, Windows Build Support IL2CPP,
    - 另外你还需要在 Visual Studio Installer 中找到 Visual Studio 2022
        - 并额外安装 WinUI, .NET 相关组件
2. 安装 Windows SDK
    - 参考：https://learn.microsoft.com/en-us/windows/apps/windows-sdk/downloads
3. 下载 `MixedRealityFeatureTool`
    - 这个工具可以用于给特定的 Unity 项目导入 MRTK3 插件
    - 参考：https://www.microsoft.com/en-us/download/details.aspx?id=102778
4. 创建一个新的 Unity 项目
    - 使用 `3D (Built-In Render Pipeline)` 模板创建一个项目
    - 参考：https://learn.microsoft.com/en-us/training/modules/learn-mrtk-tutorials/1-3-exercise-configure-unity-for-windows-mixed-reality
5. 切换构建平台到 UWP/Arm64
    - 可能需要 Unity Hub 安装相关组件：Universal Windows Platform Build Support
    - 参考：https://learn.microsoft.com/en-us/training/modules/learn-mrtk-tutorials/1-3-exercise-configure-unity-for-windows-mixed-reality
    - 安装完成后可能需要重启 Unity Editor
6. 使用 Mixed Reality Feature Tool 将 MRTK3 的相关包导入到先前的 Unity 项目中
    - 在将 MRTK3 导入相关包之前，建议先使用 Unity Editor 启动项目
    - Mixed Reality Feature Tool 启动可能需要一段时间更新目录到本地
    - 参考：https://learn.microsoft.com/en-us/training/modules/learn-mrtk-tutorials/1-5-exercise-configure-resources
    - MRTK3 相关包导入项目后，回到 Unity Editor，会自动编译新引入的脚本（需要花一段时间）
7. 配置 XR Plugin Management 并构建一个场景
    - 参考：https://learn.microsoft.com/en-us/training/modules/learn-mrtk-tutorials/ 中 `Configure the Unity project` 一节
8. 创建可交互对象：
    - 参考：https://learn.microsoft.com/en-us/training/modules/learn-mrtk-tutorials/1-7-exercise-hand-interaction-with-objectmanipulator
    - 使用这种方法创建的可交互对象可以使用左手右手捏住并移动，也可以使用两个手同时捏住然后缩放

## 部署项目到 Hololens2

> [!TIP]
> 请善于使用 Device Portal，Device Portal 的网页版提供了丰富的辅助功能，可以用于将设备上路径的文件发送到其他电脑等等。

1. 确保你的 Hololens2 和你的开发用电脑位于同一个局域网中
2. 确保你的 Hololens2 已经打开并配置好了 Device Portal
3. 在 Hololens 上提前安装好 “适用于 Windows Mixed Reality 的 OpenXR 工具（使用）”
4. 在 Build Settings 里面
    - 将 Build and Run on 后填写 `Remove Device (via Device Portal)`
    - 然后正确填写 Device Portal 的 Address/Username/Password
    - 编译并部署过程中，可能需要相当长的时间，需要保证头显开启
5. 解决 Visual Studio 组件缺失问题
    - 使用 Visual Studio 打开 Build 生的文件夹中的 sln 文件
    - 打开后，Visual Studio 会提示缺失的环境
