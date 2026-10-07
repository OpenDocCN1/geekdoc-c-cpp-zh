and pip. You can use pip to install yotta. You also need to install the GCC ARM cross compiler gcc-arm-none-eabi. On Ubuntu you need gcc-arm-embedded instead.

To summarize, make sure you have installed:

+   1. Python
2. pip
3. CMake
4. Ninja
5. GNU Arm Embedded Toolchain
6. srec_cat.exe
7. yotta

All of these have to be on the path and hence executable from the command line. Apart from Python and pip, which are needed to install yotta, these can be installed in any order.

# Creating a Micro:bit Project

You don't need to know all of the yotta commands to create and work with a micro:bit project. To create a new project you first create a new project directory and while in the directory use the command:
yotta init

If yotta cannot be found then you need to check that it is on the path.
For example, under Windows:

```
mkdir pulse
cd pulse
yotta init
```

At this point you will be asked a set of questions:

+   1. Name of module - defaults to name of directory
2. Initial version - defaults to 0.0.0
3. Is this an executable? - Yes in this case, defaults to No
4. short description - whatever you want to put
5. Author - whatever you want to put
6. License - your preferred license, defaults to Apache 2.0