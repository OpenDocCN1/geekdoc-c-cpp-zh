
```csharp
Console.WriteLine("Source is " + source);
Console.WriteLine();
}

class Y {
    public void Handler<T,V>(T source, V arg) where V : MyEventArgs {
        Console.WriteLine("Event " + arg.EventNum + " received by a Y object.");
        Console.WriteLine("Source is " + source);
        Console.WriteLine();
    }
}

class UseGenericEventDelegate {
    static void Main() {
        X ob1 = new X();
        Y ob2 = new Y();
        MyEvent evt = new MyEvent();
        // Add Handler() to the event list.
        evt.SomeEvent += ob1.Handler;
        evt.SomeEvent += ob2.Handler;
        // Fire the event.
        evt.OnSomeEvent();
        evt.OnSomeEvent();
    }
}
```

输出如下：

```
Event 0 received by an X object.
Source is MyEvent

Event 0 received by a Y object.
Source is MyEvent

Event 1 received by an X object.
Source is MyEvent

Event 1 received by a Y object.
Source is MyEvent
```

## 泛型接口

除了泛型类和方法之外，还可以有泛型接口。泛型接口的指定方式与泛型类相同。下面这个示例重新实现了第 12 章中开发的 ISeries 接口。（回忆一下，ISeries 定义了一个用于生成数字序列的类的接口。）现在，它所操作的数据类型由类型参数指定。

```csharp
class GenIntfDemo {
    // Define plus two for int.
    static int IntPlusTwo(int v) {
        return v + 2;
    }

    // Define plus two for double.
    static double DoublePlusTwo(double v) {
        return v + 2.0;
    }

    // Define plus two for ThreeD.
    static ThreeD ThreeDPlusTwo(ThreeD v) {
        if(v==null) return new ThreeD(0, 0, 0);
        else return new ThreeD(v.x + 2, v.y + 2, v.z + 2);
    }

    static void Main() {

        // Demonstrate int series.
        ByTwos<int> intBT = new ByTwos<int>(IntPlusTwo);

        for(int i=0; i < 5; i++)
            Console.Write(intBT.GetNext() + "  ");

        Console.WriteLine();

        // Demonstrate double series.
        ByTwos<double> dblBT = new ByTwos<double>(DoublePlusTwo);

        dblBT.SetStart(11.4);

        for(int i=0; i < 5; i++)
            Console.Write(dblBT.GetNext() + "  ");

        Console.WriteLine();

        // Demonstrate ThreeD series.
        ByTwos<ThreeD> ThrDBT = new ByTwos<ThreeD>(ThreeDPlusTwo);

        ThreeD coord;
        for(int i=0; i < 5; i++) {
            coord = ThrDBT.GetNext();
            Console.Write(coord.x + "," +
                          coord.y + "," +
                          coord.z + "  ");
        }

        Console.WriteLine();

    }
}
```

if(v.CompareTo(what) == 0) // now OK, uses CompareTo()
    return true;
}
return false;
}
```

注意约束的使用

```
where T : IComparable
```

该约束确保只有实现了 IComparable 的类型才是 IsIn() 的有效类型实参。

下面的程序演示了 IsIn()。它还展示了类可以多么轻松地实现 IComparable：

```
// Demonstrate IComparable.
using System;

class MyClass : IComparable {
    public int Val;
    public MyClass(int x) { Val = x; }
    // Implement IComparable.
    public int CompareTo(object obj) {
        return Val - ((MyClass) obj).Val;
    }
}

class CompareDemo {
    // Require IComparable interface.
    public static bool IsIn<T>(T what, T[] obs) where T : IComparable {
        foreach(T v in obs)
            if(v.CompareTo(what) == 0) // now OK, uses CompareTo()
                return true;
        return false;
    }
    // Demonstrate comparisons.
    static void Main() {
        // Use IsIn() with int.
        int[] nums = { 1, 2, 3, 4, 5 };
        if(IsIn(2, nums))
            Console.WriteLine("2 is found.");
        if(IsIn(99, nums))
            Console.WriteLine("This won't display.");
        // Use IsIn() with string.
```

```
string[] strs = { "one", "two", "Three" };
if(IsIn("two", strs))
    Console.WriteLine("two is found.");
if(IsIn("five", strs))
    Console.WriteLine("This won't display.");

// Use IsIn with MyClass.
MyClass[] mcs = { new MyClass(1), new MyClass(2),
    new MyClass(3), new MyClass(4) };

if(IsIn(new MyClass(3), mcs))
    Console.WriteLine("MyClass(3) is found.");
if(IsIn(new MyClass(99), mcs))
    Console.WriteLine("This won't display.");
}
```

输出如下：

```
2 is found.
two is found.
MyClass(3) is found.
```

尽管前面的程序是正确的，但仍然存在一个潜在的问题点。

注意 MyClass 是如何实现 CompareTo() 的：

```
public int CompareTo(object obj) {
    return Val - ((MyClass) obj).Val;
}
```

因为 CompareTo() 的参数必须是 object 类型，所以为了访问 Val，必须将 obj 显式强制转换为 MyClass。然而，泛型正是为了消除这类情况而设计的！

为了解决这个问题，C# 提供了 IComparable 的泛型版本，其声明如下：

```
public interface IComparable<T>
```

在这个版本中，被比较的数据类型作为类型实参传递给 T。这导致 CompareTo() 的声明发生变化，如下所示：

```
int CompareTo(T obj)
```

现在，CompareTo() 的参数可以指定为合适的类型，并且不需要从 object 进行强制转换。所有内置类型也都实现了 IComparable<T>。

下面是实现了 IComparable<T> 的 MyClass 的改进版本：

```
// This version of MyClass implements IComparable<T>
class MyClass : IComparable<MyClass> {
    public int Val;
```

```
return ob;
}
}
// A class derived from Gen.
class Gen2<T> : Gen<T> {
    public Gen2(T o) : base(o) {
        // ...
    }
}

class GenHierDemo {
    static void Main() {
        Gen2<string> g2 = new Gen2<string>("Hello");
        Console.WriteLine(g2.GetOb());
    }
}
```

在这个层次结构中，Gen2 继承泛型类 Gen。注意 Gen2 是如何通过下面这行声明的：

```
class Gen2<T> : Gen<T> {
```

类型参数 T 由 Gen2 指定，同时也会传递给 Gen。这意味着，无论什么类型传递给 Gen2，也会同样传递给 Gen。例如，下面的声明

```
Gen2<string> g2 = new Gen2<string>("Hello");
```

将 string 作为类型参数传递给 Gen。因此，Gen2 中 Gen 部分内部的 ob 将是 string 类型。

还要注意，Gen2 除了将类型参数 T 传递给 Gen 基类之外，并不使用它。因此，即使某个派生类在其他情况下不需要是泛型的，它仍然必须指定其泛型基类所要求的类型参数。

当然，派生类可以根据需要自由添加自己的类型参数。例如，下面是前面层次结构的一个变体，其中 Gen2 添加了自己的类型参数：

```
// A derived class can add its own type parameters.
using System;

// A generic base class.
class Gen<T> {
    T ob; // declare a variable of type T

    // Pass the constructor a reference of type T.
    public Gen(T o) {
        ob = o;
    }

    // Return ob.
    public T GetOb() {
        return ob;
    }
```

```
// A derived class of Gen that defines a second
// type parameter, called V.
class Gen2<T, V> : Gen<T> {
    V ob2;
    public Gen2(T o, V o2) : base(o) {
        ob2 = o2;
    }
    public V GetObj2() {
        return ob2;
    }
}

// Create an object of type Gen2.
class GenHierDemo2 {
    static void Main() {
        // Create a Gen2 object for string and int.
        Gen2<string, int> x =
            new Gen2<string, int>("Value is: ", 99);
        Console.Write(x.GetOb());
        Console.WriteLine(x.GetObj2());
    }
}
```

注意这个版本的 Gen2 的声明，如下所示：

```
class Gen2<T, V> : Gen<T> {
```

这里，T 是传递给 Gen 的类型，而 V 是 Gen2 特有的类型。V 用于声明名为 ob2 的对象，并作为方法 GetObj2() 的返回类型。在 Main() 中创建了一个 Gen2 对象，其中类型参数 T 为 string，类型参数 V 为 int。程序会显示如下预期结果：

Value is: 99

## 泛型派生类

非泛型类完全可以作为泛型派生类的基类。例如，考虑下面这个程序：

```
// A non-generic class can be the base class of a generic derived class.
using System;
// A non-generic class.
class NonGen {
    int num;
    public NonGen(int i) {

