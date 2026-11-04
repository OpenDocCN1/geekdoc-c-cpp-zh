![](bbox=[0.124, 0.109, 0.216, 0.181])

Open source software is written by collaborating groups of volunteer programmers and is usually free to the world.

A description of how to make C# and other .NET languages portable to other operating systems is far beyond the scope of this book. But you can expect that within a few years, the C# Windows programs you discover how to write in this book will run on all sorts of hardware under all sorts of operating systems — matching the claim of Sun Microsystems' Java language to run on any machine. That's undoubtedly a good thing, even for Microsoft. The road to that point is still under construction, so it's no doubt riddled with potholes and obstacles to true universal portability for C#. But it's no longer just Microsoft's road.

For the moment, however, Microsoft Visual Studio has the most mature versions of C# and .NET and the most feature-filled toolset for programming with them.

> **Note:** Though three authors contributed to this book, saying I rather than we throughout the main text seemed more economical, so that's what we (or I) do throughout.

# What's New in C# 4.0

Although much of C# 4.0 is still virtually the same as the previous version, this new version adds some exciting new features, most of which revolve around COM Interop, to assist with Office development. The big new additions that this book covers include these topics:

+   - **Dynamic types:** Functional programming is all the rage these days, with the cool kids programming in Ruby and Haskell. Functional programming certainly has some benefits that have a place in the more tightly woven world of C#, and dynamic typing is one of them. As supported in C++ and Visual Basic, dynamic types allow runtime declaration when you don't know the type of a variable and then have the compiler figure it out. Properly used, dynamic typing is quite powerful; poorly used, it's quite dangerous.
+   - **Named and optional parameters:** In C# 3.0, you had to provide a value for every parameter in a method call. In C# 4.0 — again, to optimize interaction with COM — you can mark parameters as optional and accept outside objects that have optional parameters.
+   - **Variance in generics:** Although objects in previous versions of C# are variant, generic collections of objects are invariant. This statement means that although the compiler accepts an apple when you're asked for a fruit, it doesn't accept a basket of apples when you're asked for a basket of fruit. This issue is fixed in C# 4.0.