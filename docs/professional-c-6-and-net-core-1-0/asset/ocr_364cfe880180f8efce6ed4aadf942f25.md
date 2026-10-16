In the user interface, the TreeView control binds to the Nodes property. The HierarchicalDataTemplate defines the look of the items in the tree view. With this data template, the value of the TypeName property is shown in a TextBlock. For showing all the child nodes, the ItemsSource property of the HierarchicalDataTemplate is bound to the Children property (code file WPFSyntaxTree/MainWindow.xaml):

```
<TreeView x:Name="treeView" ItemsSource="{Binding Nodes, Mode=OneTime}" SelectedItemChanged="OnSelectSyntaxNode" Grid.Row="1" Grid.Column="0">
    <TreeView.ItemTemplate>
        <HierarchicalDataTemplate ItemsSource="{Binding Children}">
            <StackPanel>
                <TextBlock Text="{Binding TypeName}" />
            </StackPanel>
        </HierarchicalDataTemplate>
    </TreeView.ItemTemplate>
</TreeView>
```

The code file that is opened with the sample application is a simple Hello, World! code file that also includes some comments:

```
using static System.Console;

namespace SyntaxTreeSample
{
    // Hello World! Sample Program
    public class Program
    {
        // Hello World! Sample Method
        public void Hello()
        {
            WriteLine("Hello, World!");
        }
    }
}
```

When you run the application, you can see a tree of the syntax node types shown in the following table. A SyntaxNode enables you to walk through the hierarchy and also access the parent node, ancestors, and descendants. When you use the Span property, which returns a TextSpan struct, the position information within the source code is returned. The following table shows the hierarchy level in the first column (2 is a child node of 1; 3 is a child node of 2); the second column gives the type of the node class; the third column lists the content of the node (if the content is longer, an ellipsis is shown); and the fourth column gives the Start and End positions of the Span property. With this tree, you can see the CompilationUnitSyntax that spans the complete source code. Child nodes of this node are the UsingDirectiveSyntax and the NamespaceDeclarationSyntax. The UsingDirectiveSyntax consists of the using declaration to import the static System.Console class. The child node of the UsingDirectiveSyntax is the QualifiedNameSyntax that itself contains two IdentifierNameSyntax nodes: