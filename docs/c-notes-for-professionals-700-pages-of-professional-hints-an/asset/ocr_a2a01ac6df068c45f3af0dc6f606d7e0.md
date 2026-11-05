In case default value is needed, you can assign one using null coalescing operator, GetValueOrDefault method or check if nullable int HasValue before assignment.

```
```csharp
int j = i ?? 0;
int j = i.GetValueOrDefault(0);
int j = i.HasValue ? i.Value : 0;
```
```

The following usage is always unsafe. If i is null at runtime, a System.InvalidOperationException will be thrown. At design time, if a value is not set, you'll get a Use of unassigned local variable 'i' error.

```
```csharp
int j = i.Value;
```
```

# Section 38.4: Getting a default value from a nullable

The .GetValueOrDefault() method returns a value even if the .HasValue property is false (unlike the Value property, which throws an exception).

```
```csharp
class Program
{
    static void Main()
    {
        int? nullableExample = null;
        int result = nullableExample.GetValueOrDefault();
        Console.WriteLine(result); // will output the default value for int - 0
        int secondResult = nullableExample.GetValueOrDefault(1);
        Console.WriteLine(secondResult) // will output our specified default - 1
        int thirdResult = nullableExample ?? 1;
        Console.WriteLine(secondResult) // same as the GetValueOrDefault but a bit shorter
    }
}
```
```

Output:

```
```
0
1
```
```

# Section 38.5: Default value of nullable types is null

```
```csharp
public class NullableTypesExample
{
    static int? _testValue;

    public static void Main()
    {
        if(_testValue == null)
            Console.WriteLine("null");
        else
            Console.WriteLine(_testValue.ToString());
    }
}
```
```

Output:

```
```
null
```
```