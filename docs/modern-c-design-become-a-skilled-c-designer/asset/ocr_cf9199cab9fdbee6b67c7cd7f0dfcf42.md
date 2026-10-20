PlatformFactory a singleton and thereby “hide” the PlatformFactory’s factory function in the Instance() function.

The abstract factory pattern might still not make a lot of sense, so let’s look at some sample code, viewing the abstraction in a top-down fashion. Ultimately, the abstract factory pattern enables us to write the following platform-independent, high-level code in pdCalc:

```
```cpp
// PlatformFactory Instance returns either a PosixFactory or a // WindowsFactory instance (based on the platform), which in turn // creates the correct derived DynamicLoader
auto loader = PlatformFactory::Instance().createDynamicLoa
```
```

```
```cpp
// The correctly instantiated loader provides platform speci fic // dynamic loading functionality polymorphically through a platform // independent interface
auto plugin = loader->allocatePlugin(pName);
```
```