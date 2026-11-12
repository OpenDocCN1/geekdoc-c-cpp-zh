![](bbox=[0.085, 0.055, 0.905, 0.365])

Figure 6 Visual Studio Code

# # Installing CMake

CMake is an open-source, cross-platform tool that generates native build tool files specific to your compiler and platform by using compiler and platform specific configuration files.

Pre-compiled binaries for Windows are available as MSI packages at https://cmake.org/download/. "Windows x64 Installer" for 64-bit systems and "Windows i386 Installer" for 32-bit systems. Execute the downloaded MSI- package to install CMake and make sure to select "Add CMake to the system PATH for all users" as well. It will be installed globally on your machine so that third-party software such as Vs-Code can access it. After the installation is complete, open the Command Prompt and run the following command to verify if it is installed on your system.

```
cmake --versi on

Microsoft Windows [Version 10.0.19044.1466]
(c) Microsoft Corporation. All rights reserved.

C:\Users\Franc>cmake --version
cmake version 3.20.2
```

# # Installing Microsoft Visual C++ Compiler Toolset.

Although we will edit our source code in VS-Code, we still have to compile and debug the code using the debugger and compiler installed on our system. This step can be redundant if you already have **Visual Studio 2017 or later** and the **Desktop Development with C++** module installed on your machine. Download