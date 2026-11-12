```
{
  "tasks": [
    {
      "type": "shell",
      "label": "build everything",
      "windows": { "command": "${workspaceFolder}/build-win.bat" },
      "linux": { "command": "${workspaceFolder}/build-linux.sh" },
      "problemMatcher": [ "$gcc" ],
      "options": { "cwd": "${workspaceFolder}" },
      "group": { "kind": "build", "isDefault": true },
    },
  ],
  "version": "2.0.0"
}
```

This file is used to configure VS-Code tasks like build tasks, clean tasks, and so on. Because VS-Code does not know how to compile our project by default, we must tell it exactly what to do by giving it a command or Shell script that will be executed when we request that the project be compiled.

# # Build Shell Scripts

In the root directory of our project’s tree (Figure 17), you can see two script files: build-win.bat and build-linux.sh, for Windows and Linux, respectively.

# build-win.bat (Windows)

```
@echo off

if not exist build mkdir build

rem generate cmake files
cmake -O. -B ./build -DCMAKE_BUILD_TYPE=Debug -
DBUILD_SHARED_LIBS=ON

rem copy assets & dll files to output dir
robocopy "./resource" "./build/bin/Debug/assets" /E
robocopy "./windows/bin/" "./build/bin/Debug/" /E

rem compile project
cd build && cmake --build .
echo compilation finished!
```

# build-linux.sh (Linux)