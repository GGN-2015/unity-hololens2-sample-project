# 如何创建一个 Hololens2 示例项目

本项目使用 Hololens2 以及 MRTK3 创建一个示例项目。
- 参考教程：https://learn.microsoft.com/en-us/training/paths/beginner-hololens-2-tutorials/

## 基本步骤

1. 安装 Unity Hub
    - 安装 Unity Editor 版本：`2022.3.62f3c1 LTS`
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
6. 
