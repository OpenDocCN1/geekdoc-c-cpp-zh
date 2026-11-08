# 4.2.3 The Details

Modules introduces a few new terms which I want to present before I use them.

# 4.2.3.1 Terminology

A module consists of one or more module units. A **module unit** is a special translation unit that has a module declaration. The module declaration must be the first declaration of this special translation unit, except the global module fragment. Each module unit is associated with a `ModuleName`:

```
Module declaration ModuleName
[export] module ModuleName [:ModulePartition]
```

The keyword export and the module partition :ModulePartition are optional.

+   - **ModuleName**: The ModuleName can have a dot. Dots have no special meaning but help to express hierarchical modules.
+   - **export**: Module declarations using the keyword **export** are called **module interface units**; otherwise, they are called **module implementation units**.
+   - **ModulePartition**: A module partition is either an **internal partition** or an **interface partition**. An internal partition is not visible from outside the module and provides declarations and definitions of the module. An interface partition participates extends the exported interface of the module.
+   - **Named module**: A named module is the collection of module units with the same module name.
+   - **Primary module interface**: Each named module must have precisely one module interface unit that is not a module partition. This module interface unit is called the primary module interface unit. Its exported content will be available to exporting clients.

# 4.2.3.2 Compiler Support

Using modules, you must use a very recent Clang, GCC, or Microsoft compiler. Even if you have the newest C++ compiler, not all features of modules in C++20 are supported. This holds, in particular, true for the Clang and GCC compiler.

The compilation of a module is challenging. For that reason, I show as an example the compilation of the module with the big three: the Microsoft compiler, the Clang compiler, and the GCC compiler. Additionally, I present the various flags you must use to use modules successfully.

![](bbox=[0.117, 0.786, 0.176, 0.831])

# Compilation of a Module

Typically, a module consists of declarations and definitions. Consequently, compiling a module consists of two steps.

+   - Precompile the module’s declarations into a compiler-specific format.
+   - Compile the module’s definitions into an object file.