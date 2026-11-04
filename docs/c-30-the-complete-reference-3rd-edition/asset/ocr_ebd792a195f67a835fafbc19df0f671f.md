Here is a simple example that illustrates boxing and unboxing:

```
~~~csharp
// A simple boxing/unboxing example.

using System;

class BoxingDemo {
    static void Main() {
        int x;
        object obj;

        x = 10;
        obj = x; // box x into an object

        int y = (int)obj; // unbox obj into an int
        Console.WriteLine(y);
    }
}
~~~
```

This program displays the value 10. Notice that the value in x is boxed simply by assigning it to **obj**, which is an **object** reference. The integer value in **obj** is retrieved by casting **obj** to **int**.

Here is another, more interesting example of boxing. In this case, an **int** is passed as an argument to the **Sqr()** method, which uses an **object** parameter.

```
~~~csharp
// Boxing also occurs when passing values.

using System;

class BoxingDemo {
    static void Main() {
        int x;

        x = 10;
        Console.WriteLine("Here is x: " + x);

        // x is automatically boxed when passed to Sqr().
        x = BoxingDemo.Sqr(x);
        Console.WriteLine("Here is x squared: " + x);
    }

    static int Sqr(object o) {
        return (int)o * (int)o;
    }
}
~~~
```

The output from the program is shown here:

```
~~~
Here is x: 10
Here is x squared: 100
~~~
```

Here, the value of **x** is automatically boxed when it is passed to **Sqr()**.

Boxing and unboxing allow **C#**'s type system to be fully unified. All types derive from **object**. A reference to any type can be assigned to a variable of type **object**. Boxing and