Given this simple implementation, we already have a useful (admittedly simple) calculator, as shown in Figure 21.6.

![](bbox=[0.12, 0.2, 0.55, 0.55])

FIGURE 21.6 Our extensible calculator without any extensions loaded.

# Discovery and Loading of Extensions

Besides the built-in extensions, we also want to be able to load all the extensions provided by third-party vendors. There are two contractual aspects to this: first, the requirement to implement our ICalculation interface, and second, the need to put extension assemblies in a place where the host application can find them (referred to as the “repository” in Figure 21.4). We’ll assume extensions live in an Extensions folder alongside the application executable.

Using reflection, we can now discover extension types in assemblies. There are two sides to this: We first need to find all the assemblies and load them. After we’ve done this, we then need to scan the assemblies for types implementing ICalculation and create an instance of those. We’ll assume a default constructor is required for extensions.

# DISCOVERY, SAFER AND SIMPLIFIED

This discovery process is of interest to us in the scope of this example because of its use of reflection for various operations. However, a few limitations and drawbacks apply when it’s implemented in the way shown here. For one thing, looking for assemblies simply by searching .dll files and trying to load them through the reflection APIs is a gross simplification of things. We might want to discover types not only based on a directory containing assemblies, but look elsewhere, too.

Second, loading those assemblies can fail for a variety of reasons. Maybe the .dll file is not an assembly but a native DLL or another kind of file that got disguised with a .dll extensions for some reason.

Finally, assemblies cannot be unloaded unless the containing application domain gets unloaded as a whole. Misbehaving assemblies or assemblies without any useful extension types will be loaded into the program’s memory.

Frameworks like System.Addins and the MEF help to avoid such issues.