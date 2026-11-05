```
public static void TestRef(ref int aValue)
{
    aValue = 333;
    Console.WriteLine("Inside TestRef -"
                      + "Value: "
                      + "{0}", aValue);
}

public static void TestDefault(int aValue)
{
    aValue = 111;
    Console.WriteLine("In TestDefault -"
                      + "Value: "
                      + "{0}", aValue);
}

public static void TestOut(out int aValue)
{
    aValue = 222;
    Console.WriteLine("In TestOut - "
                      + "Value: "
                      + " {0}", aValue);
}
}
```

The output shown in Figure 3-8 illustrates how value parameters remain unchanged. They retain their original value in the calling method. This is because a copy is actually made of the original value. On return to the calling method, the original retained values are visible.

Arguments sent using `ref` and `out` are changed when control is returned to the calling method. The `out` parameter does not have to be initialized before the call; however, the `out` parameter must be assigned a value before the method returns. C# does not allow the use of uninitialized variables.