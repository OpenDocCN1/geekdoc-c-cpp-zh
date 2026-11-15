```
Output 11.5:

490
Fireswamp
```

For type inferencing to be successful, the types must match the method signature. However, starting with C# 3.0, the compiler added an enhancement to imply the type parameter as long as the types were implicitly compatible. For example, calling the Max<T>() method using MathEx.Max(7.0, 490) will compile successfully. Even though the parameters are not both the same type (int and double), they will both implicitly convert to double, so the method call compiles. You can resolve the error by either casting explicitly or including the type argument. Also note that you cannot perform type inferencing purely on the return type. Parameters are required for type inferencing to be allowed.

# Specifying Constraints

The generic method also allows constraints to be specified. For example, you can restrict a type parameter to implement IComparable<T>. The constraint is specified immediately following the method header, prior to the curly braces of the method block, as shown in Listing 11.38.

# LISTING 11.38: Specifying Constraints on Generic Methods

```
public class ConsoleTreeControl
{
    // Generic method Show<T>
    public static void Show<T>(BinaryTree<T> tree, int indent)
        where T : IComparable<T>
    {
        Console.WriteLine(new string(' ',
            "* -- ".PadLeft(5*indent) + " ",
            tree.Item.ToString()));
        if (tree.SubItems.First != null)
            Show(tree.SubItems.First, indent+1);
        if (tree.SubItems.Second != null)
            Show(tree.SubItems.Second, indent+1);
    }
}
```