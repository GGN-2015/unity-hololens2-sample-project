本项目使用 Hololens2 以及 MRTK3 创建一个示例项目。
- 参考教程：https://learn.microsoft.com/en-us/training/paths/beginner-hololens-2-tutorials/

如果你想直接复现本项目而不自己动手创建项目，可以参考 “如何从当前项目出发编译并复现本项目”

如果你想自己动手重新实现本项目中的内容，可以参考 “如何创建本 Hololens2 示例项目”

# 如何从当前项目出发编译并复现本项目

1. 配置 Unity Editor `2022.3.62f3c1 LTS` 以及 Visual Studio 2022
    - Visual Studio 2022 要用 Unity Hub 的 Installs 界面下载
2. 使用 Unity Hub 打开 `./Hololens2Test` 中的项目
3. 打开场景：
    - File -> Open Scene
    - 选择 `Asserts/Secens/Hololen2Scene.unity`
4. 重新填写 File -> Build Settings
    - UWP
    - ARM64
    - Remote Decive (via Device Portal)
       - 填写正确的 Address/Username/Password
       - Device Portal 的 Address 最好到浏览器测试一下看看是否能连上
       - 最好到 System -> Preferences -> Decive Security 里面
           - 要么关闭 SSL connection 的 reqire 选项
           - 要么下载证书 (名为 `rootcertificate.cer` 的文件) 并安装
    - 配置好后点击 Switch Platform
5. 到 Edit -> Project Settings -> Project Validation 里面做 Fix All
    - 可能会剩一些不重要的错误 Fix 不掉，不用管他

剩余的操作详见 “部署项目到 Hololens2” 一节。


# 如何创建本 Hololens2 示例项目

本节内容将为你介绍此项目是如何创建而成的。

## 约定

- 项目文件存储在 `./Hololens2Test` 目录
- 打包构建项目存储在 `./Hololens2Test/_build` 目录

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

> [!TIP]
> 如果你的电脑没有打开 Windows 开发者模式，你需要将其开启:
> - 详见：`Win+I` -> 系统 -> 高级 -> 开发者模式

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
6. Build and Run，如果遇到报错可以参考下面的解决方案。
    - 为了与本项目中提供的自动化脚本配合。
    - 你需要将 build 项目保存到 `./Hololens2Test/_build` 目录中
    - 在 build 前请确保 Hololens2 已经解锁，否则 Unity 将无法通过 Device Portal 连接 Hololens2
        - 如果你已经编译上了，再去开 Hololens2 大概率会连接失败
    - 在没有编译缓存的前提下，初次编译部署项目大约需要 4min 时间
    - 在有缓存的前提下，编译并部署项目大约需要 1.5min 时间

## 编译报错的常见解决方案

> [!NOTE]
> 一些可能出现的其他报错以及解决方式：(注意：每次解决报错后需要重新 Build)
> - No valid MRTK Profile for build target platform. 
>   - 去 Edit -> Project Settings -> Project Validation 里面 Fix 一下
> - Failed to open DevicePortal connection to 'xxx.xxx.xxx.xxx'
>   - 先用浏览器测试一下 DevicePortal 的网页端是否可用，如果可用
>   - 大概率是 Build Settings 里面的 Device Portal 口令丢失了，重新填写一下就行
> - Selected Visual Studio is missing required components and may not be able to build the generated project.
>   - 把 `./Hololens2Test/_build` 里面的项目的 `.sln` 文件用 Visual Studio 打开一下，诊断缺失组件
>   - 再按照提示安装即可
> - Build Failed 然后很长的编译命令，报错信息中出现 error MSB3774: 找不到 SDK“WindowsMobile, Version=10.0.2xxxx.0”
>   - 方法一：使用本项目提供的自动化脚本
>       - 运行 `./fix_win_mobile.py` 这个 python 脚本即可
>   - 方法二：手动解决（如果脚本运行后报错不变）
>       - 用 Visual Studio 2022 打开 `.sln` 文件
>       - 然后到资源管理器把 `Hololens2Test` （主解决方案）卸载
>       - 到代码里面找到包含 `WindowsMobile` 的 `ItemGroup`，然后将其删掉，删掉后再冲下加载这个
> - Deployment Error，报错信息中能看到类似 ...x64.appx 的文件名
>   - 到 Build Settings 里面目标架构选择 ARM64
