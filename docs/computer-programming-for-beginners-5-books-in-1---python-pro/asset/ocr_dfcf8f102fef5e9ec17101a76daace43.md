```
```csharp
return (width * length);
}
}
class Object1Tester {
    static void Main(string[] args) {
        Object1 obj = new Object1(8, 6);
        double x = obj.area();
        Console.WriteLine("The area is: {0}",x);
        Console.ReadKey();
    }
}
}
```
```

The code will print the following result:

![](bbox=[0.036, 0.38, 0.944, 0.549])

After defining a function in a class that you want to implement in an inherited class, you should use a *virtual* function.

To implement dynamic polymorphism, we use *abstract classes* and *virtual functions*. Let us demonstrate this using an example:

```
```csharp
using System;
namespace PolymorphismApp {
    class Object {
        protected int width, height;
        public Object( int x = 0, int y = 0) {
            width = x;
            height = y;
        }
        public virtual int area() {
```
```