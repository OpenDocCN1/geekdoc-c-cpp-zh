This declaration works in functions and namespaces but not in classes (where it would collide with other `using` declarations). The term “name hiding” is meant literally as can be seen in the following example:

Click here to view code image

```
void f(string s) { ... } // # 1
namespace inner {
    void f(int i) { ... } // # 2
    f("from global"); // Error: #2 hides #1
}
```

If we declare or define a function in an inner scope it not only hides the function overload with the same signature but all overloads from outer scope. Actually any entity named f (class, variable, ... ) would hide the global function f. To make it available for a function call, we can make it visible with a `using` declaration:

Click here to view code image

```
void f(string s) { ... } // # 1
namespace inner {
    void f(int i) { ... } // # 2
    using ::f;
    f("from global"); // now calls #1
}
```

Importing a name into a namespace within header files considerably increases the danger of name conflicts because the name remains visible in all subsequent files of a compile unit. `using` within a function (even in header files) is less critical because the imported name is only visible till the end of the function. Similarly, we can import an entire namespace with a `using` directive:

```
void fun ( ... )
{
    using namespace c1::c2;
    cc x;
    ...
    cc y;
}
```

As before, it can be done within a function or another namespace but not in a class scope. The statement: