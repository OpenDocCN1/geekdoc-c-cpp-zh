
static variable. A static variable is initialized before its class is used. If no explicit initializer is specified, it is initialized to zero for numeric types, null in the case of reference types, or false for variables of type bool. Thus, a static variable always has a value.

The difference between a static method and a normal method is that the static method can be called through its class name, without any instance of that class being created. You have seen an example of this already: the `Sqrt()` method, which is a static method within C#'s `System.Math` class.

Here is an example that declares a static variable and a static method:

```
// Use static.
using System;
class StaticDemo {
    // A static variable.
    public static int Val = 100;
    // A static method.
    public static int ValDiv2() {
        return Val/2;
    }
}
class SDemo {
    static void Main() {
        Console.WriteLine("Initial value of StaticDemo.Val is "
            + StaticDemo.Val);
        StaticDemo.Val = 8;
        Console.WriteLine("StaticDemo.Val is " + StaticDemo.Val);
        Console.WriteLine("StaticDemo.ValDiv2(): " +
            StaticDemo.ValDiv2());
    }
}
```

The output is shown here:

```
Initial value of StaticDemo.Val is 100
StaticDemo.Val is 8
StaticDemo.ValDiv2(): 4
```

As the output shows, a static variable is initialized before any object of its class is created.

There are several restrictions that apply to static methods:

- A static method does not have a `this` reference. This is because a static method does not execute relative to any object.
- A static method can directly call only other static methods of its class. It cannot directly call an instance method of its class. The reason is that instance methods operate on specific objects, but a static method is not called on an object. Thus, on what object would the static method operate?
- A similar restriction applies to static data. A static method can directly access only other static data defined by its class. It cannot operate on an instance variable of its class because there is no object to operate on.

For example, in the following class, the static method `ValDivDenom()` is illegal:

```
class StaticError {
    public int Denom = 3; // a normal instance variable
    public static int Val = 1024; // a static variable

    /* Error! Can't directly access a non-static variable
       from within a static method. */
    static int ValDivDenom() {
        return Val/Denom; // won't compile!
    }
}
```

Here, `Denom` is a normal instance variable that cannot be accessed within a static method. However, the use of `Val` is okay since it is a static variable.

The same problem occurs when trying to call a non-static method from within a static method of the same class. For example:

```
using System;

class AnotherStaticError {
    // A non-static method.
    void NonStaticMeth() {
        Console.WriteLine("Inside NonStaticMeth().");
    }

    /* Error! Can't directly call a non-static method
       from within a static method. */
    static void staticMeth() {
        NonStaticMeth(); // won't compile
    }
}
```

In this case, the attempt to call a non-static (that is, instance method) from a static method causes a compile-time error.

It is important to understand that a static method can call instance methods and access instance variables of its class if it does so through an object of that class. It is just that it cannot use an instance variable or method without an object qualification. For example, this fragment is perfectly valid:

```
class MyClass {
    // A non-static method.
    void NonStaticMeth() {
        Console.WriteLine("Inside NonStaticMeth().");
    }

    /* Can call a non-static method through an
       object reference from within a static method. */
    public static void staticMeth(MyClass ob) {
        ob.NonStaticMeth(); // this is OK
}
```

Here, `NonStaticMeth()` is called by `staticMeth()` through `ob`, which is an object of type `MyClass`.

Because static fields are independent of any specific object, they are useful when you need to maintain information that is applicable to an entire class. Here is an example of such a situation. It uses a static field to maintain a count of the number of objects that are in existence.

```
// Use a static field to count instances.

using System;

class CountInst {
    static int count = 0;
    // Increment count when object is created.
    public CountInst() {
        count++;
    }
    // Decrement count when object is destroyed.
    ~CountInst() {
        count--;
    }
    public static int GetCount() {
        return count;
    }
}

class CountDemo {
    static void Main() {
        CountInst ob;
        for(int i=0; i < 10; i++) {
            ob = new CountInst();
            Console.WriteLine("Current count: " + CountInst.GetCount());
        }
    }
}
```

The output is shown here:

```
Current count: 1
Current count: 2
Current count: 3
Current count: 4
Current count: 5
Current count: 6
Current count: 7
Current count: 8
Current count: 9
Current count: 10
```

Each time that an object of type `CountInst` is created, the static field `count` is incremented. Each time an object is recycled, `count` is decremented. Thus, `count` always contains a count of the number of objects currently in existence. This is possible only through the use of a static field. There is no way for an instance variable to maintain the count because the count relates to the class as a whole, not to a specific instance.

Here is one more example that uses static. Earlier in this chapter, you saw how a class factory could be used to create objects. In that example, the class factory was a non-static method, which meant that it could be called only through an object reference. This meant that a default object of the class needed to be created so that the factory method could be called. However, a better way to implement a class factory is as a static method, which allows the class factory to be called without creating an unnecessary object. Here is the class factory example rewritten to reflect this improvement:

```
// Use a static class factory.

using System;

class MyClass {
    int a, b;

    // Create a class factory for MyClass.
    static public MyClass Factory(int i, int j) {
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
        int i, j;

        // Generate objects using the factory.
        for(i=0, j=10; i < 10; i++, j--) {
            MyClass ob = MyClass.Factory(i, j); // get an object
            ob.Show();
        }

        Console.WriteLine();
    }
}
```

In this version, `Factory()` is invoked through its class name in this line of code:

```
MyClass ob = MyClass.Factory(i, j); // get an object
```

There is no need to create a `MyClass` object prior to using the factory.

## Static Constructors

A constructor can also be specified as static. A static constructor is typically used to initialize features that apply to a class rather than an instance. Thus, it is used to initialize aspects of a class before any objects of the class are created. Here is a simple example:

```
// Use a static constructor.
using System;
class Cons {
  public static int alpha;
  public int beta;
  // A static constructor.
  static Cons() {
    alpha = 99;
    Console.WriteLine("Inside static constructor.");
  }
  // An instance constructor.
  public Cons() {
    beta = 100;
    Console.WriteLine("Inside instance constructor.");
  }
}
class ConsDemo {
  static void Main() {
    Cons ob = new Cons();
    Console.WriteLine("Cons.alpha: " + Cons.alpha);
    Console.WriteLine("ob.beta: " + ob.beta);
  }
}
```

Here is the output:

```
Inside static constructor.
Inside instance constructor.
Cons.alpha: 99
ob.beta: 100
```

Notice that the static constructor is called automatically (when the class is first loaded) and before the instance constructor. This can be generalized. In all cases, the static constructor will be executed before any instance constructor. Furthermore, static constructors cannot have access modifiers (thus, they use default access) and cannot be called by your program.
