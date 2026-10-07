# Your First Program - Blinky

The time comes to run your first program and deal with some details of using VS Code.

You can use either the V1 or V2 development environment and hence target either version of the micro:bit. It is assumed that you have set up a project called BlinkyV1 or BlinkyV2 following the instructions given earlier. Load the project into VS Code and do a clean configure and a clean rebuild. Next, delete all of the source files in the source directory, which is in the project root for both versions. Create a new file called main.cpp, or simply copy the code into the existing file, containing the following code:

```
#include "MicroBit.h"
MicroBit ubit;
int main()
{
  ubit.init();
  ubit.display.setDisplayMode(DISPLAY_MODE_GRESCALE);
  for (;;) {
    ubit.display.setPixelValue(2, 2, 255);
    ubit.sleep(1000);
    ubit.display.setPixelValue(2, 2, 0);
    ubit.sleep(1000);
  }
}
```

Exactly the same code will work with the V1 or the V2 micro:bit. Do a clean reconfigure and a clean rebuild of the project. As usual you will see a lot of warnings scroll past for the V1 compile, but the build should finish without errors.

You will find the generated hex files in ~/BlinkyV1/build/source for the V1 program and the file you want to download is BlinkyV1-combined.hex.

For the V2 program you will find the hex in the project root and it is called MICROBIT.hex.

If you have set the templates correctly, you should see the middle LED in the display flash at 1 second intervals. Notice that if you simply change the main program, or make minor changes to any program in the project, you should only need to do a build and not a clean build.

Everything should work as advertised, including IntelliSense, auto-complete and error flagging. If not sure that the .vscode/c_properties.json file contains the line:

```
"compileCommands": "${workspaceFolder}/build/compile_commands.json",
```