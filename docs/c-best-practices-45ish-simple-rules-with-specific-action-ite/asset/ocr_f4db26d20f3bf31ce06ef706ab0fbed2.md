# #6. Exercise: Use the Tools: Static Analysis

Static analysis tools are tools that analyze your code without compiling or executing it. Your compiler is one such tool and your first line of defense.

Many such tools are free and some are free for open source projects.

cppcheck and clang-tidy are two popular and free tools with major IDE and editor integration.

# ## Enable More Static Analysis

Visual Studio: look into Microsoft's static analyzer that ships with it. Consider using Clang Power Tools. Download cppcheck's addon for visual studio

CMake: Enable cppcheck and clang-tidy integration

# ## Resources

+   - cppbestpractices list of static analyzers¹

> > ^¹https://github.com/lefticus/cppbestpractices/blob/master/02-Use_the_Tools_Available.md#static-analyzers