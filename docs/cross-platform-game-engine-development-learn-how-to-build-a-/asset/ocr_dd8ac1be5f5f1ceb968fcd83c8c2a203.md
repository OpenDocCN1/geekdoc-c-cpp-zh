# Installing yaml-cpp (Windows)

This section will go through how to install yaml-cpp on the Windows platform. We'll clone the repository and build the library using CMake.

# Cloning yaml-cpp

yaml-cpp can be cloned from GitHub via the homepage or a command line. The build files are found here: https://github.com/jbeder/yaml-cpp.

To clone the repository from GitHub, use the following command: This will download all of the files required to compile the library. The keyword "recursive" is not required for the command to function, but it only ensures that if yaml-cpp has submodules, they are also cloned.

```
git clone --recursive https://github.com/jbeder/yaml-cpp.git
```

> Note : You must have "git" installed on your machine to execute the command above. If you don't, you can use the following instructions.

Download the source code as shown in the following picture.

![](bbox=[0.085, 0.465, 0.915, 0.75])

Figure 48 Downloading yaml-cpp

This will download the source code as a ZIP file, which must be decompressed using WinRAR, ZIP, or any other package manager tool. Now that we have the source code downloaded, let's compile it.

# Building yaml-cpp

As mentioned earlier we are going to use CMake to compile yaml-cpp. Below is a set of commands that can be used to build the library.