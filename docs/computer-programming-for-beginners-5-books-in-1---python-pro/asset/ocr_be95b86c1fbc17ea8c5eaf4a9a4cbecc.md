```
```csharp
Console.WriteLine("The area of the parent class is :");
return 0;
}
}
class Object1: Object {
    public Object1( int x = 0, int y = 0): base(x, y) {

    }
    public override int area () {
        Console.WriteLine("The area of Object1 class is:");
        return (width * height);
    }
}
class Object2: Object {
    public Object2(int x = 0, int y = 0): base(x, y) {
    }
    public override int area() {
        Console.WriteLine("The area of Object2 class is:");
        return (width * height / 2);
    }
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
```