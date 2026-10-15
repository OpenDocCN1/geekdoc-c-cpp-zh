flag it with underlining, similar to the Microsoft Word spelling or grammar error underlines. When you click the underlined text, the compiler will tell you which other assemblies need to be referenced in the project in order to use the class in question.

# Common Namespaces

The generated list of references shown in the Solution Explorer for the newly created Namespace_Sampler project includes most, but not all, of the namespaces that are part of your Windows Forms Application project. For example, one namespace not displayed as a reference is Microsoft.VisualBasic, and the accompanying Microsoft.VisualBasic.dll. Every Visual Basic 2010 project includes the namespace Microsoft.VisualBasic. This namespace is part of the Visual Studio project templates for Visual Basic 2010 and is, in short, what makes Visual Basic 2010 different from C# or any other .NET language. The implicit inclusion of this namespace is the reason why you can call IsDBNull and other methods of Visual Basic 2010 directly. The only difference in the default namespaces included with Visual Basic 2010 and C# Windows Forms Application projects is that the former use Microsoft.VisualBasic and the latter use Microsoft.CSharp.

To see all of the namespaces that are imported automatically, such as the Microsoft.VisualBasic namespace, right-click the project name in the Solution Explorer and select Properties from the context menu. This opens the project’s Properties window in Visual Studio. Select the References tab from the left pane and you will see the reference Microsoft.VisualBasic at the top of the list (see Figure 4-11).

![](bbox=[0.09, 0.4, 0.62, 0.67])

FIGURE 4-11

When looking at the project’s global list of imports in the text area at the bottom of the page, you can see that in addition to the Microsoft.VisualBasic namespace, the System.Collections and System.Diagnostics namespaces are also imported into the project. This is signified by the check marks next to the namespace. Unlike the other namespaces in the list, these namespaces are not listed as references in the text area directly above this. That’s because implementation of the System.Collections and System.Diagnostics namespaces is part of the referenced System.dll. Similarly to Microsoft.VisualBasic, importing these namespaces allows references to the associated classes, such that a fully qualified path is not