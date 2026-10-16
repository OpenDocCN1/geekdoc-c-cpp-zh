The Assets settings define what files should be included with the VSIX project. In case you’re adding images and readme files with the description of the add-in, you need to add these files to the Assets. One file that needs to be added to the Assets in any case is the binary created from the other project (see Figure 18.8). With the code refactoring provider building, you need to set the type to a Microsoft.VisualStudio.MefComponent. The last settings of the designer define Dependencies that are required to be installed on the target system before the add-in can be installed—for example, .NET Framework 4.6.

![](bbox=[0.105, 0.25, 0.895, 0.498])

Figure 18.8

# Code Refactoring Provider

Now that you’ve configured the VSIX package, let’s get into the source code. The generated class PropertyCodeRefactoringProvider makes use of the attribute ExportCodeRefactoringProvider. This is an attribute to define a MEF part that can be included with Visual Studio. The base class CodeRefactoringProvider is a class defined by the Workspace API in the assembly Microsoft.CodeAnalysis.Workspaces (code file PropertyCodeRefactoring/CodeRefactoringProvider.cs):

```
[ExportCodeRefactoringProvider(LanguageNames.CSharp,
    Name = nameof(PropertyCodeRefactoringProvider)), Shared]
internal class PropertyCodeRefactoringProvider:
CodeRefactoringProvider
{
    // etc.
}
```

The base class CodeRefactoringProvider defines the method ComputeRefactoringsAsync that is invoked when the user of the code editor starts Quick Actions in the context menu. Based on the selection of the user, with the implementation of this method, it needs to be decided whether the add-in should offer one of the options to allow code changes. The parameter CodeRefactoringContext makes it possible