# Class Inheritance and Virtual Functions

```
for each(IContainer^ container in containers)
    stack->Push(container);

Console::WriteLine(
    L"Popping the containers off the stack presents them in reverse order:");
Object^ item;
while((item = stack->Pop()) != nullptr)
    safe_cast<IContainer^>(item)->ShowVolume();

Console::WriteLine();
return 0;
}
```

You also need to add the GlassBox.h header to the project with the same code as in Ex9_15 so you can copy the file to this project directory and then add it to the project by right-clicking Header Files in the Solution Explorer tab and selecting Add > Existing Item from the context menu. Of course, the GlassBox class is derived from the Box class, so the compiler needs to know where to find the Box class definition. In this case it’s in the library you created in the previous project, so add the following directive to the GlassBox.h header file after the #pragma once directive:

```
#using <Ex9_16lib.dll>
```

The Box class name is defined within the Ex9_16lib namespace, so you also need to add a using statement for that following the #using directive:

```
using namespace Ex9_16lib;
```

To enable the compiler to find the library, copy the Ex9_16lib.dll file from the Ex9_16lib project to the debug subdirectory to the Ex9_16 solution directory that contains the Ex9_16.exe file. You could specify the full path to the assembly in the #using directive, but it is more usual to put any class libraries that a project uses in the directory that contains the executable for an application. It’s easy to get the directories muddled here. The Ex9_16lib.dll file is in the debug subdirectory to the Ex9_16lib solution directory, not the debug subdirectory to the Ex9_16lib project directory. You are copying the library file to the debug subdirectory of the Ex9_16 solution directory. Make sure you copy the .dll file to the correct directory or the library won’t be found.

Because the classes in the external assembly are in their own namespace, you have a using directive for the Ex9_16lib namespace name. Without this you would have to qualify the IContainer, Box, and Stack names with the namespace name so you would write Ex9_16lib::Box instead of just Box for example.

The remainder of the code is exactly the same as in the main() function for Ex9_15; no changes are necessary because you are now using classes from an external assembly. If you execute the program, you’ll see the output is the same as that from Ex9_15.