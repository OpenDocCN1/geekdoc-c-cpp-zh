folders before proceeding.

We stated in the introduction that our project would consist of an engine library and a game executable. As a result, we have a folder called "engine" and another called "game" in our project folder tree.
The folder "windows" will be used to store all dependencies related to the
Windows platform like .lib, .dll files, and external include header files.
To enable VS-Code to use the C/C++ extension we installed previously, we must
first create a folder named ".vscode" in which we will place the three JSON files
shown below: "c_cpp_properties.json", "launch.json", and "tasks.json".
Let's go through each file role one by one.

# c_cpp_properties.json

```
```json
{
  "configurations": [
    {
      "name": "configs",
      "includePath": [
        "${workspaceFolder}/windows/includes/**",
        "${workspaceFolder}/engines/src/**"
      ],
      "defines": ["_DEBUG", "FUSE_EXPORT"],
      "cStandard": "c17",
      "cppStandard": "c++17",
      "intelliSenseMode": "${default}"
    }
  ],
  "version": 4
}
```
```

This file is used to configure the C/C++ extension in VS-Code to offer proper
IntelliSense, error checking, and syntax highlighting. It is important to note that
this has no effect on the code compilation process. Its purpose is only to improve
our coding experience in VS-Code.
The symbols defined here are only for code highlighting. The same is true for the
C++ language standard; it's only to improve code completion. The IntelliSense
mode is set to "default" to make sure we are using the current system default
mode. We can also specify a mode like: "clang-x64".

# launch.json