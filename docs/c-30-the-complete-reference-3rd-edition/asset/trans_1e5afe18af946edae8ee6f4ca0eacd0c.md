
```csharp
public void SetStart(int x) {
    start = x;
    val = start;
}

class SeriesDemo2 {
    static void Main() {
        ByTwos twoOb = new ByTwos();
        Primes primeOb = new Primes();
        ISeries ob;

        for(int i=0; i < 5; i++) {
            ob = twoOb;
            Console.WriteLine("Next ByTwos value is " +
                              ob.GetNext());

            ob = primeOb;
            Console.WriteLine("Next prime number is " +
                              ob.GetNext());
        }
    }
}
```

The output from the program is shown here:

```text
Next ByTwos value is 2
Next prime number is 3
Next ByTwos value is 4
Next prime number is 5
Next ByTwos value is 6
Next prime number is 7
Next ByTwos value is 8
Next prime number is 11
Next ByTwos value is 10
Next prime number is 13
```

在 **Main()** 中，**ob** 被声明为对 **ISeries** 接口的引用。这意味着它可用于存储实现 **ISeries** 的任何对象的引用。在本例中，它用于引用 **twoOb** 和 **primeOb**，它们分别是 **ByTwos** 和 **Primes** 类型的对象，两者都实现了 **ISeries**。

另一点：接口引用变量仅知道其 **interface declaration** 声明的方法。因此，接口引用无法用于访问对象可能支持的任何其他变量或方法。

## 接口属性

像方法一样，属性在接口中也是不带主体指定的。下面是属性指定的一般形式：

```csharp
// interface property
type name {
    get;
    set;
}
```

当然，对于只读或只写属性，分别只会出现 get 或 set。虽然接口中属性的声明看起来与类中自动实现属性的声明相似，但两者并不相同。接口声明不会导致属性被自动实现。它仅指定属性的名称和类型。实现留给每个实现类。此外，在接口中声明属性时，访问器上不允许使用访问修饰符。因此，例如，set 访问器在接口中不能指定为 private。下面是使用名为 Next 的属性来获取和设置序列中下一个元素的 ISeries 接口和 ByTwos 类的重写：

```csharp
// Use a property in an interface.
using System;

public interface ISeries {
    // An interface property.
    int Next {
        get; // return the next number in series
        set; // set next number
    }
}

// Implement ISeries.
class ByTwos : ISeries {
    int val;

    public ByTwos() {
        val = 0;
    }

    // Get or set value.
    public int Next {
        get {
            val += 2;
            return val;
        }
        set {
            val = value;
        }
    }
}

// Demonstrate an interface property.
class SeriesDemo3 {
    static void Main() {
        ByTwos ob = new ByTwos();

        // Access series through a property.
        for(int i=0; i < 5; i++) {
            Console.WriteLine("Next value is " + ob.Next);
        }

        Console.WriteLine("\nStarting at 21");
        ob.Next = 21;

        for(int i=0; i < 5; i++)
            Console.WriteLine("Next value is " + ob.Next);
    }
}
```

程序的输出如下所示：

```text
Next value is 2
Next value is 4
Next value is 6
Next value is 8
Next value is 10

Starting at 21
Next value is 23
Next value is 25
Next value is 27
Next value is 29
Next value is 31
```

## 接口索引器

接口可以指定索引器。在接口中声明的一维索引器的一般形式如下：

```csharp
// interface indexer
element-type this[int index] {
    get;
    set;
}
```

如前所述，对于只读或只写索引器，分别只会出现 **get** 或 **set**。此外，在 **interface** 中声明索引器时，访问器上也不允许使用访问修饰符。

下面是 **ISeries** 的另一个版本，它添加了一个只读索引器，返回序列中的第 *i* 个元素。

```csharp
// Add an indexer in an interface.

using System;

public interface ISeries {
    // An interface property.
    int Next {
        get; // return the next number in series
        set; // set next number
    }

    // An interface indexer.
    int this[int index] {
        get; // return the specified number in series
    }
}
```

程序的输出如下所示：

```text
Next value is 2
Next value is 4
Next value is 6
Next value is 8
Next value is 10

Starting at 21
Next value is 23
Next value is 25
Next value is 27
Next value is 29
Next value is 31

Resetting to 0
Next value is 0
Next value is 2
Next value is 4
Next value is 6
Next value is 8
```

## 接口可以被继承

一个接口可以继承另一个接口。语法与继承类相同。当一个类实现了一个继承了另一个接口的接口时，它必须为接口继承链中定义的所有成员提供实现。下面是一个示例：

```csharp
// One interface can inherit another.

using System;

public interface IA {
    void Meth1();
    void Meth2();
}

// B now includes Meth1() and Meth2() -- it adds Meth3().
public interface IB : IA {
    void Meth3();
}

// This class must implement all of IA and IB.
class MyClass : IB {
    public void Meth1() {
        Console.WriteLine("Implement Meth1().");
    }

    public void Meth2() {
        Console.WriteLine("Implement Meth2().");
    }

    public void Meth3() {
        Console.WriteLine("Implement Meth3().");
    }
}

class IFExtend {
    static void Main() {
        MyClass ob = new MyClass();

        ob.Meth1();
        ob.Meth2();
        ob.Meth3();
    }
}
```

作为实验，你可以尝试删除 MyClass 中 Meth1() 的实现。这将导致编译时错误。如前所述，任何实现接口的类都必须实现该接口定义的所有方法，包括从其他接口继承的方法。

## 接口继承中的名称隐藏

当一个接口继承另一个接口时，可以在派生接口中声明一个成员来隐藏基接口中定义的一个成员。当派生接口中的成员与基接口中的成员具有相同的声明时，就会发生这种情况。在这种情况下，基接口名称会被隐藏。除非使用 new 指定派生接口成员，否则会产生警告信息。

## 显式实现

在实现接口的成员时，可以用其接口名称完全限定其名称。这样会创建显式接口成员实现，简称为显式实现。例如，给定

```csharp
interface IMyIF {
    int MyMeth(int x);
}
```

那么按如下所示实现 IMyIF 是合法的：

```csharp
class MyClass : IMyIF {
    int IMyIF.MyMeth(int x) {
        return x / 3;
    }
}
```

正如你所见，当实现 IMyIF 的 MyMeth() 成员时，其完整名称（包括接口名称）被指定。

你可能需要创建接口方法的显式实现有两个原因。首先，当你使用完全限定名称实现接口方法时，你提供的是无法通过类的对象访问的实现。相反，它必须通过接口引用访问。因此，显式实现提供了一种实现接口方法的方式，使其不是提供实现类的公共成员。其次，一个类可以实现两个接口，这两个接口都声明了同名且类型签名相同的方法。用接口限定名称可以消除这种情况下的歧义。让我们分别看一个示例。

下面的程序包含一个名为 IEven 的接口，它定义了两个方法 IsEven() 和 IsOdd()，用于判断一个数是偶数还是奇数。MyClass 然后实现 IEven。在实现时，它显式地实现了 IsOdd()。

```csharp
// Explicitly implement an interface member.

using System;

interface IEven {
    bool IsOdd(int x);
    bool IsEven(int x);
}

class MyClass : IEven {
    // Explicit implementation. Notice that this member is private
    // by default.
    bool IEven.IsOdd(int x) {
        if((x%2) != 0) return true;
        else return false;
    }

    // Normal implementation.
    public bool IsEven(int x) {
        IEven o = this; // Interface reference to the invoking object.
        return !o.IsOdd(x);
    }
}

class Demo {
    static void Main() {
        MyClass ob = new MyClass();
        bool result;
        result = ob.IsEven(4);
        if(result) Console.WriteLine("4 is even.");

        // result = ob.IsOdd(4); // Error, IsOdd not exposed.

        // But, this is OK. It creates an IEven reference to a MyClass object
        // and then calls IsOdd() through that reference.
        IEven iRef = (IEven) ob;
        result = iRef.IsOdd(3);
        if(result) Console.WriteLine("3 is odd.");
    }
}
```
