With small programs, you can define names within the global namespace without running into any problems. Within larger code bases the potential for name clashes increases, so you should use namespaces to partition your code into logical groupings. That way, each code segment is self-contained from a naming perspective, and name clashes are prevented.

# Defining a Namespace

A namespace definition has the following form:

```
```cpp
namespace mySpace
{
    // Code you want to have in the namespace,
    // including function definitions and declarations,
    // global variables, enum types, templates, etc.
}
```
```

Note that no semicolon is required after the closing brace in a namespace definition. The namespace name here is mySpace. The braces enclose the scope for the namespace mySpace, and every name declared within the namespace scope has the name mySpace attached to it.

> > **Caution**  You must not include the main() function within a namespace. The runtime environment expects main() to be defined in the global namespace.

You can extend a namespace scope by adding a second namespace block with the same name. For example, a program file might contain the following:

```
```cpp
namespace mySpace
{
    // This defines namespace mySpace
    // The initial code in the namespace goes here
}
namespace network
{
    // Code in a new namespace, network
}
namespace mySpace
{
    /* This extends the mySpace namespace
       Code in here can refer to names in the previous
       mySpace namespace block without qualification */
}
```
```