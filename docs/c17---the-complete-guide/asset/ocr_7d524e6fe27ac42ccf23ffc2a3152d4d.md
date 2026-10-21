```
return msg;
}
...
};
```

+   - You can use variable templates (since C++14):
+     `template<typename T = std::string>`
+     `T myGlobalMsg{"OK"};`

+   - You can define a class template for the static member(s):
+     `template<typename = void>`
+     `class MyClassStatics`
+     `{`
+     `    static std::string msg;`
+     `};`
+   
+     `template<typename T>`
+     `std::string MyClassStatics<T>::msg{"OK"};`
+   
+     and then even derive from it:
+     `class MyClass : public MyClassStatics<>`
+     `{`
+     `    ...`
+     `};`

However, all of these approaches lead to significant overhead, less readability, and/or different ways to use the global variable. In addition, the initialization of a global variable might be postponed until its first use, which disables applications in which we want to initialize objects at program start (such as when using an object to monitor the process).

# 3.2 Using Inline Variables

Now, with inline, you can have a single globally available object by defining it only in a header file, which might be included by multiple CPP files:

```
class MyClass {
    inline static std::string msg{"OK"};  // OK since C++17
    ...
};
```

```
inline MyClass myGlobalObj;  // OK even if included/defined by multiple CPP files
```

Formally, the inline used here has the same semantics as a function declared inline:

+   - It can be defined in multiple translation units, provided all definitions are identical.

+   - It must be defined in every translation unit in which it is used.

Both are given by including the definition from the same header file. The resulting behavior of the program is as if there were exactly one variable.