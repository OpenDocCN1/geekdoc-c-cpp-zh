# Compilation

To get semantic information, you need to compile the code. You can create a compilation that invokes the static Create method of the CSharpCompilation class. This method returns a CSharpCompilation instance that represents compiled code. A parameter that is required is the name of the assembly that is generated. Optional parameters are syntax trees, assembly references, and compiler options. You can also add this information by invoking methods. The sample code adds an assembly reference by invoking the AddReferences method and the syntax tree by invoking the method AddSyntaxTrees. You could configure compiler options by invoking the method WithOptions by passing an object of type CompilationOptions, but here only the default options are used (code file SemanticsCompilation/Program.cs):

```
```csharp
var compilation = CSharpCompilation.Create("HelloWorld")
.AddReferences(
    MetadataReference.CreateFromFile(
        typeof(object).Assembly.Location
    )
)
.AddSyntaxTrees(tree);
```
```

There’s a difference between the actual compiler and the compiler building that was taught in universities not many years ago: It’s that a program isn’t compiled only once before it is executed; the compilation needs to take place multiple times. By adding some characters in the code editor, compilation needs to show squiggles under the incorrect code if compilation goes wrong. This behavior occurs because of the new compilation process. Using the CSharpCompilation object, small changes could be done where the cache information from the previous compilation can be used. The compiler is built for this process in mind to be high performing with this functionality.

You can add syntax trees and references using AddReferences and AddSyntaxTrees; you remove them using RemoveReferences and RemoveSyntaxTrees. To produce a compilation binary, you can invoke the Emit method:

```
```csharp
EmitResult result = compilation.Emit("HelloWorld.exe");
```
```

Using the compilation, diagnostic information of the compilation process can be retrieved. The compilation object also gives some information about symbols. For example, the symbol for the method Hello can be retrieved:

```
```csharp
ISymbol helloVariableSymbol =
    compilation.GetSymbolsWithName(name => name
    =="Hello").FirstOrDefault();
```
```

# Semantic Model

For making an analysis of the program and accessing symbols with binding to nodes from the tree, you can create a SemanticModel object to invoke the GetSemanticModel method from the CSharpCompilation object (code file SemanticsCompilation/Program.cs):