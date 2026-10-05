The cd command means "change directory." This command sets the console's working directory to the development folder you previously created. If you are working in another folder, you can adjust the path given in the cd command to your work area.

You are ready to edit your code. If your environment is set up so that your editor program is in the system path, you can type

```
notepad++ simple.cpp
```

If you are using Vim, type

```
gvim simple.cpp
```

If the file simple.cpp already exists, you can type

```
devenv simple.cpp
```

to launch the Visual Studio editor.

Within the editor type in your program and save it to a file.

When you have finished creating the source file, you will need to build the executable program. Switch back to the Visual Studio Command Prompt window, and issue the command

```
cl /W3 /EHsc /Za simple.cpp
```

The cl (/W3 "cee", not "cee one") command, which stands for compile and link, preprocesses, compiles, and links the program. The /W3 switch uses the Level 3 warning level. Level 3 warnings provide more thorough analysis of your source code and can detect more mistakes. If you omit the /W3 switch, the compiler operates at level 1. Level 1 is insufficient for catching many mistakes by both beginning and experienced C++ programmers. By the default IDE compiler uses level 3, and the level can be changed by adjusting the project's properties. On the command line, specifying /W4 (the highest warning) is just as easy as specifying /W3. It is better to use /W4 so the compiler can do a thorough check for potential programmer mistakes. The /EHsc is required for all C++ programs we write. The /Za switch makes sure the compiler complies with standard C++ language rules and does not allow any Microsoft-specific language extensions.

If you want to reduce the level of detail in the output produced by the compiler and linker, you can add the additional switch /nologo:

```
cl /W4 /EHsc /Za /nologo simple.cpp
```