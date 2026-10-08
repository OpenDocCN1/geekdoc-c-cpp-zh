There is a significant issue with this solution — it's static. This approach explicitly enumerates the parts composing the application. It uses types that should be known at compile time, and lacks dynamic discovery of parts.

Instead, the `MefGreetings` sample builds up the composition container utilizing a catalog:

```
var catalog = new AssemblyCatalog(Assembly.GetExecutingAssembly());
var container = new CompositionContainer(catalog);
container.Compose(this);
```

A catalog in MEF is an abstraction of an inventory that contains parts. The great thing about a catalog is that it has dynamic behavior. Its content is established at run-time, and so it can be used for dynamic discovery. For example, the AssemblyCatalog used in the code snippet is inventory for all composable parts contained in a concrete physical assembly.

MEF is shipped with a number of catalogs out-of-the-box. Table 10-9

# 10-9: MEF Catalogs

| TYPE NAME | DESCRIPTION |
|---|---|n| TypeCatalog | This catalog is a container for types. During the discovery, all exports are collected that are exploited by the types in the catalog. You can use this when you know exactly the types providing exports — for example, when you create unit tests. |
| AssemblyCatalog | This catalog discovers all exports in a specified assembly. You can use this catalog when you know which assemblies contains parts. With AssemblyCatalog, you can put dynamism into your application. You can separate the static (not affected by changes) and dynamic (subject to changes) partitions of the application into different assemblies. Creating an AssemblyCatalog on the dynamic partition allows better change management. |
| DirectoryCatalog | This catalog discovers all the exports in all the assemblies in a directory. You can use an absolute or relative path when creating a DirectoryCatalog. If you specify a relative path, it is relative to the base directory of the current AppDomain. With this catalog, you can add flexibility to application! Just drop an assembly into the folder of the catalog, restart your application, and it can immediately use the exports in the newly dropped assembly. |
| AggregateCatalog | As the name of this type suggests, it combines multiple catalogs into a single catalog. A common pattern is that you aggregate several DirectoryCatalog instances to aggregate all folders where you/ expect extension assemblies into a combined catalog. (Visual Studio 2010 internally uses this.) |