```
static class Util
{
    public static int Negate(this int i)
    {
        return -i;
    }
}
```

The syntax looks a little odd, but it is the this keyword prefixing the parameter to Negate that identifies it as an extension method, and the fact that the parameter that this prefixes is an int means that you are extending the int type.

To use the extension method, bring the Util class into scope. (If necessary, add a using statement that specifies the namespace to which the Util class belongs, or a using static statement that specifies the Util class directly.) Then you can simply use dot notation (.) to reference the method, like this:

Click here to view code image

```
int x = 591;
Console.WriteLine($"x.Negate {x.Negate()}");
```

Notice that you do not need to reference the Util class anywhere in the statement that calls the Negate method. The C# compiler automatically detects all extension methods for a given type from all the static classes that are in scope. You can also invoke the Util.Negate method by passing an int as the parameter, using the regular syntax you have seen before, although this use obviates the purpose of defining the method as an extension method:

Click here to view code image

```
int x = 591;
Console.WriteLine($"x.Negate {Util.Negate(x)}");
```

In the following exercise, you will add an extension method to the int type. With this extension method, you can convert the value in an int variable from base 10 to a representation of that value in a different number base.

# Create an extension method

+   1. In Visual Studio 2015, open the ExtensionMethod project, which is located in the \Microsoft Press\VCSBS\Chapter 12\ExtensionMethod folder in your Documents folder.
+   2. Display the Util.cs file in the Code and Text Editor window.
+      This file contains a static class named Util in a namespace named Extensions. Remember that you must define extension methods inside a static class. The class is empty apart from the // TODO: comment.
+   3. Delete the comment and declare a public static method in the Util class, named ConvertToBase. The method should take two parameters: an int parameter named i, prefixed with the this keyword to indicate that the