As shown in Figure 4-18, the New Project dialog displays three types of project template hierarchy nodes:

+   * Project type root nodes — These are related to languages, or, more precisely, language service packages such as Visual C# or Visual Basic. Figure 4-18 shows examples for Visual C#.
* Pseudo nodes — These are parent folders for a project root nodes. Other Languages and Other Project Types provide good examples in Figure 4-18.
* Template folder nodes — These are the children of project root nodes, and they are mapped to physical folders having template files under them. In Figure 4-18, the Windows, Web, and Silverlight nodes under Visual C# are examples of them.

![](bbox=[0.147, 0.335, 0.796, 0.755])

**Figure 4-18:** Project template node types

The whole procedure of creating the template node hierarchy is a bit complex, so this discussion does not include all the details. Instead, here are a few points to help you understand the basics:

+   * To produce the project template hierarchy, Visual Studio uses the .vtemplate files within the .zip archive, registry keys, and values stored in the NewProjectTemplates key with the help of mentioned earlier, resources in the language packages (determined with the help of registry values), template folder structure, and .vstdir files.