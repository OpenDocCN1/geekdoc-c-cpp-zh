Just like a path name, a module name is made up of letters, digits, underscores, and periods. Also, just as with path names, there is no hierarchical relationship between modules. If you had a module com.horstmann and another module com.horstmann.corejava, they would be unrelated, as far as the module system is concerned.

When creating a module for use by others, it is important to ensure that its name is globally unique. It is expected that most module names will follow the “reverse domain name” convention, just like package names.

The easiest approach is to name a module after the top-level package that the module provides. For example, the SLF4J logging façade has a module org.slf4j with packages org.slf4j, org.slf4j.spi, org.slf4j.event, and org.slf4j.helpers.

This convention prevents package name conflicts in modules. Any given package can only be placed in one module. If your module names are unique and your package names start with the module name, then your package names will also be unique.

You can use shorter module names for modules that are not meant to be used by other programmers, such as a module containing an application program. Just to show that it can be done, I will do the same in this chapter. Modules with what could plausibly be library code will have names such as com.horstmann.util, and modules containing programs (with a class that has a main method) will have catchy names such as v2ch09.hellomod.

> > **NOTE:** Module names are only used in module declarations. In the source files for your Java classes, you never refer to module names; instead, use package names the way they have always been used.

# ### 9.3 The Modular “Hello, World!” Program

Let us put the traditional “Hello, World!” program into a module. First, we need to put the class into a package—the “unnamed package” cannot be contained in a module. Here it is:

```
```java
package com.horstmann.hello;

public class HelloWorld
{
   public static void main(String[] args)
   {
      System.out.println("Hello, Modular World!");
   }
}
```
```