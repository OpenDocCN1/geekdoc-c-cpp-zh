```
public class ClashingMethodSignatures
{
    public void MethodA()
    {
    }

    // This would cause a clash with the method above:
    //public void MethodA()
    //{
    //}

    // As would this: return values are not considered
    //public int MethodA()
    //{
    //    return 0;
    //}

    public int MethodB(int x)
    {
        return x;
    }

    // There is no clash here: the parameters differ.
    // This is an overload of the previous MethodB.
    public int MethodB(int x, int y)
    {
        return x + y;
    }
}
```

Properties, because they don’t have parameter lists, are differentiated solely on their name. Thus, two properties’ signatures clash if they possess the same name.

Imagine the class shown in Listing 3-6, which is needed to implement the aforementioned interface, InterfaceOne.

# LISTING 3-6 The interface that this class needs to implement will cause method signature collisions.

Click here to view code image

```
public class ClassWithMethodSignatureClash
{
    public void MethodOne()
```