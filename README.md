For chinese version of readme, see [./README_ZH.md](./README_ZH.md)

This project uses HoloLens 2 and MRTK3 to create a sample project.
- Reference Tutorial: https://learn.microsoft.com/en-us/training/paths/beginner-hololens-2-tutorials/

If you want to directly reproduce this project without creating one from scratch, please refer to *How to Compile and Reproduce This Project Based on the Current Project*.

If you want to manually reimplement the content of this project, please refer to *How to Create This HoloLens 2 Sample Project*.

# How to Compile and Reproduce This Project Based on the Current Project

1. Configure Unity Editor `2022.3.62f3c1 LTS` and Visual Studio 2022
    - Visual Studio 2022 should be downloaded via the Installs page in Unity Hub.
2. Open the project inside `./Hololens2Test` using Unity Hub.
3. Open the scene:
    - File -> Open Scene
    - Select `Assets/Scenes/Hololen2Scene.unity`
4. Reconfigure settings under File -> Build Settings
    - UWP
    - ARM64
    - Remote Device (via Device Portal)
       - Fill in the correct Address, Username and Password
       - It is recommended to test the Device Portal address in a browser to verify connectivity
       - Navigate to System -> Preferences -> Device Security
           - Either disable the SSL connection requirement option
           - Or download and install the certificate file named `rootcertificate.cer`
    - Click Switch Platform after completing configuration.
5. Go to Edit -> Project Settings -> Project Validation and click Fix All
    - Minor trivial errors that cannot be fixed can be ignored.

For remaining procedures, see the section *Deploy the Project to HoloLens 2*.

# How to Create This HoloLens 2 Sample Project

This section introduces the creation workflow of this project.

## Conventions

- Project files are stored in the `./Hololens2Test` directory
- Build outputs are stored in the `./Hololens2Test/_build` directory

## Basic Steps

> [!IMPORTANT]
> The Community edition of Visual Studio 2022 can no longer be installed directly via Visual Studio Installer. Please use the installation feature in Unity Hub to install a compatible version of Visual Studio for your Unity Editor.

1. Install Unity Hub
    - Install Unity Editor version: `2022.3.62f3c1 LTS`
    - **Note**: If you use `Unity Editor 2022.3.62f3c1 LTS`, you must additionally install Visual Studio 2022. Newer versions of Visual Studio are incompatible for compiling projects of this Unity version.
    - In Unity Hub -> Installs, locate the specified Unity Editor version, click the gear icon in the upper-right corner of its tab
        - At minimum, install VS2022, UWP Build Support, and Windows Build Support (IL2CPP)
    - Additionally, locate Visual Studio 2022 in Visual Studio Installer
        - Install extra WinUI and .NET related components
2. Install the Windows SDK
    - Reference: https://learn.microsoft.com/en-us/windows/apps/windows-sdk/downloads
3. Download Mixed Reality Feature Tool
    - This tool is used to import MRTK3 packages into designated Unity projects
    - Reference: https://www.microsoft.com/en-us/download/details.aspx?id=102778
4. Create a new Unity project
    - Create a project using the `3D (Built-In Render Pipeline)` template
    - Reference: https://learn.microsoft.com/en-us/training/modules/learn-mrtk-tutorials/1-3-exercise-configure-unity-for-windows-mixed-reality
5. Switch the build platform to UWP/ARM64
    - You may need to install Universal Windows Platform Build Support via Unity Hub
    - Reference: https://learn.microsoft.com/en-us/training/modules/learn-mrtk-tutorials/1-3-exercise-configure-unity-for-windows-mixed-reality
    - Restart Unity Editor after installation if required
6. Import MRTK3 packages into the Unity project using Mixed Reality Feature Tool
    - It is recommended to launch the project in Unity Editor first before importing MRTK3 packages
    - Mixed Reality Feature Tool may take some time to update local catalogs on startup
    - Reference: https://learn.microsoft.com/en-us/training/modules/learn-mrtk-tutorials/1-5-exercise-configure-resources
    - After importing MRTK3 packages, return to Unity Editor; newly imported scripts will compile automatically, which may take a while
7. Configure XR Plugin Management and create a scene
    - Refer to the *Configure the Unity project* section at https://learn.microsoft.com/en-us/training/modules/learn-mrtk-tutorials/
8. Create interactable objects:
    - Reference: https://learn.microsoft.com/en-us/training/modules/learn-mrtk-tutorials/1-7-exercise-hand-interaction-with-objectmanipulator
    - Objects created this way can be grabbed and moved with either hand, or scaled by pinching with both hands simultaneously

## Deploy the Project to HoloLens 2

> [!TIP]
> Make full use of Device Portal. Its web interface provides rich auxiliary functions, such as transferring files from the device to other computers.

> [!TIP]
> If Developer Mode is not enabled on your Windows PC, please enable it:
> - Path: `Win+I` > System > Advanced > Developer Mode

1. Ensure your HoloLens 2 and development PC are connected to the same local area network.
2. Confirm HoloLens 2 is powered on and Device Portal is properly configured.
3. Pre-install *OpenXR Tools for Windows Mixed Reality* on HoloLens 2.
4. In Build Settings
    - Set Build and Run on to `Remote Device (via Device Portal)`
    - Fill in the correct Device Portal Address, Username and Password
    - Compilation and deployment may take a long time; keep the headset powered on during the process.
5. Resolve missing Visual Studio components
    - Open the generated solution `.sln` file in the build folder with Visual Studio
    - Visual Studio will prompt for missing environment components after opening.
6. Perform Build and Run. Refer to the common troubleshooting solutions below if errors occur.
    - To work with the automated scripts provided in this project
    - Save build outputs to the `./Hololens2Test/_build` directory
    - Ensure HoloLens 2 is unlocked before building; otherwise Unity may fail to connect via Device Portal
        - Connection failure is highly likely if you unlock the headset after starting compilation
    - Initial clean build and deployment takes approximately 4 minutes
    - Incremental build with cache takes approximately 1.5 minutes

## Common Solutions for Build Errors

> [!NOTE]
> Other potential errors and fixes are listed below. Note: Rebuild the project after applying any fix.
> - No valid MRTK Profile for build target platform.
>   - Run Fix All under Edit -> Project Settings -> Project Validation
> - Failed to open DevicePortal connection to 'xxx.xxx.xxx.xxx'
>   - First verify Device Portal web access via a browser. If accessible
>   - The Device Portal credentials in Build Settings are likely lost; re-enter them.
> - Selected Visual Studio is missing required components and may not be able to build the generated project.
>   - Open the `.sln` file under `./Hololens2Test/_build` in Visual Studio to diagnose missing components
>   - Install required components following the prompts.
> - Build Failed with lengthy compile command, containing error MSB3774: Could not find SDK "WindowsMobile, Version=10.0.2xxxx.0"
>   - Method 1: Use the automated script provided in this project
>       - Run the Python script `./fix_win_mobile.py`
>   - Method 2: Manual fix if the script does not resolve the error
>       - Open the `.sln` file in Visual Studio 2022
>       - Unload the `Hololens2Test` main solution in Solution Explorer
>       - Locate and delete the `ItemGroup` containing `WindowsMobile` in the project code, then reload the solution
> - Deployment Error with filename similar to ...x64.appx in error logs
>   - Set the target architecture to ARM64 in Build Settings
