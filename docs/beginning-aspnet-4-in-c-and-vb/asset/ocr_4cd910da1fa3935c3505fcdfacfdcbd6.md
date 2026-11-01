Be sure to register the new version of the shared assembly SharedDemo again in the GAC, using gacutil. If the referenced version cannot be found, you will get a System.IO.FileLoadException, because the binding to the correct assembly failed.

With a successful run, you can see the full name of the referenced assembly:

```
```
SharedDemo, Version=1.0.0.0, Culture=neutral, PublicKeyToken= f946433fdae2512d
```
```

This client program can now be used to test different configurations of this shared component.

# Binding to Assembly Versions

With a configuration file, you can specify that the binding should happen to a different version of a shared assembly. Assume that you create a new version of the shared assembly SharedDemo with major and minor versions 1.1. Maybe you don't want to rebuild the client but just want the new version of the assembly to be used with the existing client instead. This is useful in cases where either a bug is fixed with the shared assembly or you just want to get rid of the old version because the new version is compatible.

By running gacutil.exe, you can see that the versions 1.0.0.0 and 1.0.3300.0 are installed for the SharedDemo assembly:

```
```
> gacutil -l SharedDemo

Microsoft (R) .NET Global Assembly Cache Utility. Version 4.0.21006.1
Copyright (c) Microsoft Corporation. All rights reserved.

The Global Assembly Cache contains the following assemblies:
SharedDemo, Version=1.0.0.0, Culture=neutral, PublicKeyToken=f946433fdae2512d,
processorArchitecture=x86
SharedDemo, Version=1.0.3300.0, Culture=neutral, PublicKeyToken=f946433fdae2512d, processorArchitecture=x86

Number of items = 2
```
```

Figure 18-14 shows the manifest of the client application where the client references version 1.0.0.0 of the assembly SharedDemo.

Now, again, an application configuration file is needed. As before, the assembly that is redirected needs to be specified with the <assemblyIdentity> element. This element identifies the assembly using the name, culture, and public key token. For a redirect to a different version, the <bindingRedirect> element is used. The oldVersion attribute specifies what version of the assembly should be redirected to a new version. With oldVersion you can specify a range like the one shown that all assemblies from version 1.0.0.0 to 1.0.3300.0 should be redirected. The new version is specified with the newVersion attribute.

![](bbox=[0.5, 0.68, 0.92, 0.88])

FIGURE 18-14

```
```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <runtime>
    <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
      <dependentAssembly>
        <assemblyIdentity name="SharedDemo" culture="neutral" publicKeyToken="f946433fdae2512d" />
        <bindingRedirect oldVersion="1.0.0.0-1.0.3300.0" newVersion="1.0.3300.0" />
      </dependentAssembly>
    </assemblyBinding>
  </runtime>
</configuration>
```
```