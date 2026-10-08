# Language-Dependent Features

As mentioned previously, a few snippet features are implemented in different ways, depending on the language context. For example, Visual Basic does not support surrounding-snippets, while the other languages do. In contrast, Visual Basic allows showing and hiding code template placeholders after the code template has been inserted and placeholder editing is terminated.

The following sections examine a few language-specific features that are related to the structure of the snippet file.

# <Imports> and <References>

There are two children of the <Snippet> section that are supported only in Visual Basic. When you insert a code into the code text, even if it is syntactically correct, it may prevent the full source file from compiling for several reasons. One of the most important is that type and member references used in the code cannot be resolved in the context they are used.

You can use the <Imports> element to define namespaces that should be added to the code as soon as the snippet is inserted. For example, if your snippet is about creating and using streams or files, it probably uses the System.IO namespace. Instead of putting the full type names in the code template, you can add the following element to the <Snippet> section:

```
<Imports>
<Import>
  <Namespace>System.IO</Namespace>
</Import>
</Imports>
```

<Imports> is a container holding one or more <Import> element, each of having exactly one <Namespace> element.

Sometimes the inserted code applies types that are in assemblies not referenced by the project where the snippet is used. The <References> element is a container holding one or more <Reference> elements to provide a way to add references to assemblies when the snippet is inserted into the code. The following example shows how to use <References>:

```
<References>
<Reference>
  <Assembly>System.Data.dll</Assembly>
  <Url>http://msdn.microsoft.com/en-us/library/system.data.(vs.100).aspx</Url>
</Reference>
<Reference>
  <Assembly>
    MyCompany.Widgets.dll, Version=1.0, Culture=neutral,
    PublicKeyToken=0123456789abcdef
  </Assembly>
  <Url>http://mycompany.com/widgets/overview.html</Url>
</Reference>
</References>
```