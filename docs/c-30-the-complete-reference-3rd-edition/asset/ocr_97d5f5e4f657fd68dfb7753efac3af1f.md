```
Console.Write("Dimensions of r2: ");
r2.Show();
Console.WriteLine("Area of r2: " + r2.Area());
}
```

The output is shown here:

```
Dimensions of r1: 4 5
Area of r1: 20

Dimensions of r2: 8 10
Area of r2: 80
```

When an object is returned by a method, it remains in existence until there are no more references to it. At that point, it is subject to garbage collection. Thus, an object won't be destroyed just because the method that created it terminates.

One application of object return types is the class factory. A class factory is a method that is used to construct objects of its class. In some situations, you may not want to give users of a class access to the class' constructor because of security concerns or because object construction depends upon certain external factors. In such cases, a class factory is used to construct objects. Here is a simple example:

```
// Use a class factory.

using System;

class MyClass {
    int a, b; // private

    // Create a class factory for MyClass.
    public MyClass Factory(int i, int j) {
        MyClass t = new MyClass();
        t.a = i;
        t.b = j;
        return t; // return an object
    }

    public void Show() {
        Console.WriteLine("a and b: " + a + " " + b);
    }
}

class MakeObjects {
    static void Main() {
        MyClass ob = new MyClass();
        int i, j;

        // Generate objects using the factory.
        for(i=0, j=10; i < 10; i++, j--) {
```