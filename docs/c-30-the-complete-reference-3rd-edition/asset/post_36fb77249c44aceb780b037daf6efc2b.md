
Here are some integers: 1 2 3 4 5
Here are two more: 17 20

In cases where a method has regular parameters and a params parameter, the params parameter must be the last one in the parameter list. Furthermore, in all situations, there must be only one params parameter.

## Return Objects

A method can return any type of data, including class types. For example, the following version of the **Rect** class includes a method called **Enlarge()** that creates a rectangle that is proportionally the same as the invoking rectangle, but larger by a specified factor:

```csharp
// Return an object.

using System;

class Rect {
    int width;
    int height;

    public Rect(int w, int h) {
        width = w;
        height = h;
    }

    public int Area() {
        return width * height;
    }

    public void Show() {
        Console.WriteLine(width + " " + height);
    }

    /* Return a rectangle that is a specified
       factor larger than the invoking rectangle. */
    public Rect Enlarge(int factor) {
        return new Rect(width * factor, height * factor);
    }
}

class RetObj {
    static void Main() {
        Rect r1 = new Rect(4, 5);

        Console.WriteLine("Dimensions of r1: ");
        r1.Show();
        Console.WriteLine("Area of r1: " + r1.Area());

        Console.WriteLine();

        // Create a rectangle that is twice as big as r1.
        Rect r2 = r1.Enlarge(2);

        Console.Write("Dimensions of r2: ");
        r2.Show();
        Console.WriteLine("Area of r2: " + r2.Area());
    }
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

```csharp
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
MyClass anotherOb = ob.Factory(i, j); // make an object
anotherOb.Show();
}

Console.WriteLine();
}
}
```

The output is shown here:

```
a and b: 0 10
a and b: 1 9
a and b: 2 8
a and b: 3 7
a and b: 4 6
a and b: 5 5
a and b: 6 4
a and b: 7 3
a and b: 8 2
a and b: 9 1
```

Let's look closely at this example. MyClass does not define a constructor, so only the default constructor is available. Thus, it is not possible to set the values of a and b using a constructor. However, the class factory Factory() can create objects in which a and b are given values. Moreover, since a and b are private, using Factory() is the only way to set these values.

In Main(), a MyClass object is instantiated, and its factory method is used inside the for loop to create ten other objects. The line of code that creates objects is shown here:

```
MyClass anotherOb = ob.Factory(i, j); // get an object
```

With each iteration, an object reference called anotherOb is created, and it is assigned a reference to the object constructed by the factory. At the end of each iteration of the loop, anotherOb goes out of scope, and the object to which it refers is recycled.

## Return an Array

Since in C# arrays are implemented as objects, a method can also return an array. (This differs from C++ in which arrays are not valid as return types.) For example, in the following program, the method FindFactors() returns an array that holds the factors of the argument that it is passed:

```csharp
// Return an array.

using System;

class Factor {
    /* Return an array containing the factors of num.
    On return, numfactors will contain the number of
    factors found. */
    public int[] FindFactors(int num, out int numfactors) {
        int[] facts = new int[80]; // size of 80 is arbitrary
        int i, j;

        // Find factors and put them in the facts array.
        for(i=2, j=0; i < num/2 + 1; i++)
if( num%i ==0 ) {
    facts[j] = i;
    j++;
}
numfactors = j;
return facts;
}
}

class FindFactors {
    static void Main() {
        Factor f = new Factor();
        int numfactors;
        int[] factors;

        factors = f.FindFactors(1000, out numfactors);

        Console.WriteLine("Factors for 1000 are: ");
        for(int i=0; i < numfactors; i++)
            Console.Write(factors[i] + " ");

        Console.WriteLine();
    }
}
```

The output is shown here:

```
Factors for 1000 are:
2 4 5 8 10 20 25 40 50 100 125 200 250 500
```

In Factor, FindFactors() is declared like this:

```
public int[] FindFactors(int num, out int numfactors) {
```

Notice how the int array return type is specified. This syntax can be generalized. Whenever a method returns an array, specify it in a similar fashion, adjusting the type and dimensions as needed. For example, the following declares a method called someMeth() that returns a two-dimensional array of double:

```
public double[,] someMeth() { // ...
```

## Method Overloading

In C#, two or more methods within the same class can share the same name, as long as their parameter declarations are different. When this is the case, the methods are said to be overloaded, and the process is referred to as method overloading. Method overloading is one of the ways that C# implements polymorphism.

In general, to overload a method, simply declare different versions of it. The compiler takes care of the rest. You must observe one important restriction: The type and/or number of the parameters of each overloaded method must differ. It is not sufficient for two methods to differ only in their return types. They must differ in the types or number of their parameters.

(Return types do not provide sufficient information in all cases for C# to decide which method to use.) Of course, overloaded methods may differ in their return types, too. When an overloaded method is called, the version of the method executed is the one whose parameters match the arguments.

Here is a simple example that illustrates method overloading:

```csharp
// Demonstrate method overloading.

using System;

class Overload {
    public void OvlDemo() {
        Console.WriteLine("No parameters");
    }

    // Overload OvlDemo for one integer parameter.
    public void OvlDemo(int a) {
        Console.WriteLine("One parameter: " + a);
    }

    // Overload OvlDemo for two integer parameters.
    public int OvlDemo(int a, int b) {
        Console.WriteLine("Two parameters: " + a + " " + b);
        return a + b;
    }

    // Overload OvlDemo for two double parameters.
    public double OvlDemo(double a, double b) {
        Console.WriteLine("Two double parameters: " + 
            a + " " + b);
        return a + b;
    }
}

class OverloadDemo {
    static void Main() {
        Overload ob = new Overload();
        int resI;
        double resD;

        // Call all versions of OvlDemo().
        ob.OvlDemo();
        Console.WriteLine();

        ob.OvlDemo(2);
        Console.WriteLine();

        resI = ob.OvlDemo(4, 6);
        Console.WriteLine("Result of ob.OvlDemo(4, 6): " + resI);
        Console.WriteLine();

        resD = ob.OvlDemo(1.1, 2.32);
        Console.WriteLine("Result of ob.OvlDemo(1.1, 2.32): " + resD);
    }
}
```
