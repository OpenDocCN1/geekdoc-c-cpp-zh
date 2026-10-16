![](bbox=[0.1, 0.06, 0.9, 0.39])

# Figure 26.1

Here’s the full picture of how parts are loaded. As mentioned, parts are found with exports. Exports can be defined using attributes, or with a fluent API from C# code. Multiple export providers can be connected in chains for customizing exports—for example, with a custom export provider to only allow parts for specific users or roles. The container uses export providers to connect imports to exports and is itself an export provider.

Microsoft Composition consists of the NuGet packages shown in Figure 26.2. This figure also shows the dependencies of the libraries.

![](bbox=[0.1, 0.6, 0.9, 0.73])

# Figure 26.2

The following table explains the content of these NuGet packages.