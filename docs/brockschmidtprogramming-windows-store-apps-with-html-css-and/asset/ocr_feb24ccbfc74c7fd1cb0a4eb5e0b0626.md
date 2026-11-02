![](bbox=[0.13, 0.07, 0.88, 0.47])

FIGURE 1-5 Process isolation for Windows Store apps.

# Sidebar: Mixed Language Apps

Windows Store apps written in JavaScript can access only WinRT APIs directly. Apps or libraries written in C#, Visual Basic, and C++ also have access to a subset of Win32 and .NET APIs, as documented on Win32 and COM for Windows Store apps. Unfair? Not entirely, because you can write a WinRT component in those other languages that make functionality built with those other APIs available in the JavaScript environment (through the same projection mechanism that WinRT itself uses). Because these components are compiled into binary dynamic-link libraries (DLLs), they will also typically run faster than the equivalent code written in JavaScript and also offer some degree of intellectual property protection (e.g., hiding algorithms either through obfuscation or by using a fully compiled language like C++).

*Such mixed language apps thus use HTML/CSS for their presentation layer and JavaScript for some app logic while placing the most performance critical or sensitive code in compiled DLLs. The dynamic nature of JavaScript, in fact, makes it a great language for gluing together multiple components. We'll see more in Chapter 18, "WinRT Components."*

Note that when your main app is written in JavaScript, we recommend using only WinRT components written in C++ to avoid having two managed environments loaded into the same process. Using WinRT components written in C# or Visual Basic does work but incurs a significant memory overhead and risks memory leaks across multiple garbage collectors.