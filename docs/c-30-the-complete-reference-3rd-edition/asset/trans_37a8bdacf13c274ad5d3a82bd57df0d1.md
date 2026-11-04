
静态变量。静态变量在其类被使用之前初始化。如果没有指定显式初始化器，则对于数值类型初始化为零，对于引用类型初始化为 null，对于 bool 类型的变量初始化为 false。因此，静态变量始终具有值。

静态方法与普通方法的区别在于，静态方法可以通过其类名调用，而无需创建该类的任何实例。你已经见过一个这样的例子：`Sqrt()` 方法，它是 C# 的 `System.Math` 类中的一个静态方法。

下面是一个声明静态变量和静态方法的示例：

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

输出如下所示：

```
Initial value of StaticDemo.Val is 100
StaticDemo.Val is 8
StaticDemo.ValDiv2(): 4
```

如输出所示，静态变量在创建其类的任何对象之前就已初始化。

静态方法有若干限制：

- 静态方法没有 `this` 引用。这是因为静态方法不是相对于任何对象执行的。
- 静态方法只能直接调用其类的其他静态方法。它不能直接调用其类的实例方法。原因在于实例方法操作特定的对象，而静态方法不是在对象上调用的。那么静态方法将在哪个对象上操作？
- 类似的限制也适用于静态数据。静态方法只能直接访问其类定义的其它静态数据。它不能操作其类的实例变量，因为没有对象可供操作。

例如，在下面的类中，静态方法 `ValDivDenom()` 是非法的：

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

这里，`Denom` 是一个普通的实例变量，不能在静态方法内访问。然而，`Val` 的使用是可以的，因为它是一个静态变量。

当尝试从同一类的静态方法内部调用非静态方法时也会出现相同的问题。例如：

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

在这种情况下，从静态方法调用非静态（即实例方法）的尝试会导致编译时错误。

必须理解，静态方法可以通过该类的对象来调用实例方法并访问实例变量。只是它不能在没有对象限定符的情况下使用实例变量或方法。例如，这段代码完全有效：

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

这里，`NonStaticMeth()` 是由 `staticMeth()` 通过 `ob` 调用的，而 `ob` 是类型为 `MyClass` 的对象。

由于静态字段独立于任何特定对象，因此在需要维护适用于整个类的信息时非常有用。下面是一个这样的例子。它使用静态字段来维护当前存在对象的数量。

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

输出如下所示：

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

每次创建类型为 `CountInst` 的对象时，静态字段 `count` 都会递增。每次对象被回收时，`count` 都会递减。因此，`count` 始终包含当前存在对象的数量。只有通过使用静态字段才可能实现这一点。实例变量无法维护计数，因为计数与整个类相关，而非特定实例。

这里还有一个使用 static 的例子。本章前面你已经看到如何使用类工厂来创建对象。在那个例子中，类工厂是一个非静态方法，这意味着它只能通过对象引用调用。这意味着需要先创建一个类的默认对象，以便调用工厂方法。然而，更好的实现类工厂的方式是作为静态方法，这样可以在不创建不必要的对象的情况下调用类工厂。下面是重写后的类工厂示例，以体现这一改进：

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

在这个版本中，`Factory()` 是通过其类名在此行代码中调用的：

```
MyClass ob = MyClass.Factory(i, j); // get an object
```

使用工厂之前无需创建 `MyClass` 对象。

## 静态构造函数

构造函数也可以指定为静态。静态构造函数通常用于初始化适用于类而不是实例的功能。因此，它用于在创建类的任何对象之前初始化类的各个方面。下面是一个简单示例：

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

输出如下：

```
Inside static constructor.
Inside instance constructor.
Cons.alpha: 99
ob.beta: 100
```

请注意，静态构造函数会在类首次加载时自动调用，并且在实例构造函数之前调用。这可以推广。在所有情况下，静态构造函数都将在任何实例构造函数之前执行。此外，静态构造函数不能有访问修饰符（因此使用默认访问），并且不能由你的程序调用。
