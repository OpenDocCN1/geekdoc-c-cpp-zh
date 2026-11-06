```
```csharp
}
class Caller {
    public void CallArea(Object obj) {
        int x;
        x = obj.area();
        Console.WriteLine("The Area is: {0}", x);
    }
}
class TesterClass {
    static void Main(string[] args) {
        Caller c = new Caller();
        Object1 ob1 = new Object1(10, 7);
        Object2 ob2 = new Object2(10, 5);
        c.CallArea(ob1);
        c.CallArea(ob2);
        Console.ReadKey();
    }
}
}
```
```

The code returns the following output:

```
```text
The area of Object1 class is:
The Area is: 70
The Area of Object2 class is:
The Area is: 25
```
```