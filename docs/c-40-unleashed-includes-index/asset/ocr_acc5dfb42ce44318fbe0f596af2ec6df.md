![](bbox=[0.08, 0.12, 0.6, 0.45])

FIGURE 24.2 COM interfaces push the declaration space problem one level up.

# HEADER NIGHTMARES

The use of headers in C and C++ is a notorious source of headaches. Various reasons come to mind, including the problems with duplicate definitions (requiring use of preprocessor tricks), the order of inclusion, and the separate notion of lib files that have to be linked in for things to work.

In the world of .NET, assemblies are self-describing and also act as the means to refer to a library during development time. Although reference assemblies are dehydrated from a code perspective (hence they're somewhat like very rich headers, including type and member information), they don't suffer from the problems related to headers.

It's clear that the approaches taken by the C-influenced world of Win32, COM, and so on have various drawbacks, such as the following:

+   - Discoverability of APIs is quite painful because all functions and types live in a single flat namespace (which can also lead to name clashes).
+   - Tooling can't help much with finding APIs, and providing decent IntelliSense support is challenging.
+   - Building applications requires multiple references to libraries, including the use of headers and a link-time reference to a library file.

# Assemblies and Namespaces

Because several of the previously mentioned problems are related, it's good to take a look at them collectively. One central issue has to do with tooling, where the requirement of headers describing binary libraries can be solved by bundling this metadata with the code of the library. This is precisely what assemblies do, as shown in Figure 24.3.