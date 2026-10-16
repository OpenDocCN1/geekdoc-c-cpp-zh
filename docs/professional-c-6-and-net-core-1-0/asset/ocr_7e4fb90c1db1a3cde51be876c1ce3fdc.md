from `CSharpSyntaxRewriter`. **Doing rewrites this way is an efficient way to build up new syntax trees based on existing ones by changing nodes.**

The following code snippet is taken for the conversion. The class `Sample` defines full properties `Text` and `X` that should be converted to auto-implemented properties. The other members of the class shouldn’t be changed (code file `SyntaxRewriter/Sample.cs`):

```
namespace SyntaxRewriter
{
    class Sample
    {
        // these properties can be converted to auto-implemented properties
        private int _x;
        public int X
        {
            get { return _x; }
            set { _x = value; }
        }

        private string _text;
        public string Text
        {
            get { return _text; }
            set { _text = value; }
        }

        // this is already a auto-implemented property
        public int Y { get; set; }

        // this shouldn't be converted
        private int _z = 3;
        public int Z
        {
            get { return _z; }
        }
    }
}
```

**To change syntax nodes, the class `AutoPropertyRewriter` derives from the base class `CSharpSyntaxRewriter`. For accessing symbol and binding information within the rewriter, the `SemanticModel` needs to be passed to the constructor of the rewriter (code file `SyntaxRewriter/AutoPropertyRewriter.cs`):**

```
class AutoPropertyRewriter : CSharpSyntaxRewriter
{
    private readonly SemanticModel _semanticModel;

    public AutoPropertyRewriter(SemanticModel semanticModel)
    {
        _semanticModel = semanticModel;
    }
    // etc.
```

The base class `CSharpSyntaxRewriter` defines multiple virtual `VisitXX` methods for different syntax node types. Here, the method `VisitPropertyDeclaration` is overridden. This method is invoked when the rewriter finds a property in the tree. Within such a method you can