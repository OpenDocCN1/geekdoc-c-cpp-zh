```
~~~
fig16_05.cpp:12:47: error: declaration of 'cube' must be imported from mod-
ule 'deitel.math' before it is required
   std::cout << "cube(3) = " << deitel::math::cube(3) << '\n';
                               ^
/usr/src/lesson16/fig16_04-05/deitel.math.ixx:12:8: note: declaration here is
not visible
   int cube(int x) {
   ^
1 error generated.
~~~
```

# ## 16.7 Global Module Fragment

As we mentioned, some headers cannot be compiled as **header units** because they require **preprocessor state**, such as macros defined in your translation unit or other headers. Such headers can be `#included` for use in a **module unit** by placing them in the **global module fragment**<sup>48</sup>

```
~~~cpp
module;
~~~
```

which you place before the `module` declaration at the beginning of a module unit. The **global module fragment** may contain only preprocessor directives. A **module interface unit** can export a declaration that was `#included` in the **global module fragment**, so other **implementation units** that `import` the module can use that declaration.<sup>49</sup> **Global module fragments** from all module units are placed into the **global module**, which also contains non-modularized code in non-module translation units, such as the one containing `main`.

# ## 16.8 Separating Interface from Implementation

In Chapters 9 and 10, we defined classes using `.h` headers and `.cpp` source-code files to separate a class’s interface from its implementation. Modules also support separating interface from implementation:

+   - You can split your interface and implementation into separate files (shown in Sections 16.8.1–16.8.2).
+   - You can define your interface and implementation in one source file (discussed in Section 16.8.3).

# ### 16.8.1 Example: Module Implementation Units

Sometimes it’s helpful to break a large module into smaller, more manageable pieces—for example, when a team of developers is working on different aspects of the same module. You can split a module definition into multiple source files. Let’s use a **primary module interface unit** for a module’s interface and a separate source code file for the **module’s implementation details**.

+   48. “C++ Standard: 10 Modules—10.4 Global Module Fragment.” Accessed April 18, 2023. https://timsong-cpp.github.io/cppwp/n4861/module.global.frag.
+   49. Dos Reis, “Programming with C++ Modules: Guide for the Working Software Developer.”