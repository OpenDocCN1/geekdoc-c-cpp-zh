There are different ways to resolve this conflict, the most obvious of which is to refer to the intended type by its full name. This can be done in a case-by-case manner, only for those types that are subject to a conflict. In other words, there’s no need to back out a namespace import because of a single issue:

```
var point = new System.Drawing.Point(3, 4);
```

Again, the Visual Studio feature to resolve names can help here. Other unambiguous names can stay abbreviated. For example

```
// Only in the System.Windows namespace (defined in the WindowsBase assembly).
var vector = new Vector(3, 4);
```

Use of those long type names can hinder code readability, though, especially if several such conflicts occur. To mitigate this issue, C# supports a way to define aliases for namespace imports.

# Using Aliases

The using directive can be extended with the definition of a named alias, acting as an abbreviation for the namespace or type name on the right side. An example of this is shown in Chapter 22, “Dynamic Programming,” when dealing with the Word and Excel automation APIs. In this context, the Application type exists in both namespaces used for Word and Excel interop. Use of an alias allowed us to abbreviate references to them:

```
using Word = Microsoft.Office.Interop.Word;
using Excel = Microsoft.Office.Interop.Excel;
```

Now we can write the following two lines of code, disambiguating a reference to the Application interface:

```
var excel = new Excel.Application();
var word = new Word.Application();
```

Defined aliases are scoped within the containing compilation unit or the immediately enclosing declaration of a namespace.

Aliases can also be used to refer to types, including generic ones as long as they’re closed constructed types; that is, no generic parameters are omitted or remain unbound:

```
using WpfPoint = System.Windows.Point;
using IntList = System.Collections.Generic.List<int>;
```

This feature tends to be used to a lesser extent. Some C++ savvy readers may draw a parallel with typedefs in some native languages. This analogy only holds to a limited degree. For example, it’s not possible to have an alias defined in an assembly such that every user