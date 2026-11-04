
```csharp
// Access to alpha and beta is allowed only through methods.
ob.SetAlpha(-99);
ob.SetBeta(15);
Console.WriteLine("ob.alpha is " + ob.GetAlpha());
Console.WriteLine("ob.beta is " + ob.GetBeta());

// You cannot access alpha or beta like this:
// ob.alpha = 10; // Wrong! alpha is private!
// ob.beta = 9;   // Wrong! beta is private!

// It is OK to directly access gamma because it is public.
ob.gamma = 99;
}
```

正如你所见，在 MyClass 类内部，alpha 被指定为 private，beta 默认是 private，而 gamma 被指定为 public。因为 alpha 和 beta 是私有的，所以它们不能被类外部的代码访问。因此，在 AccessDemo 类内部，两者都不能直接使用。每个都必须通过公共方法访问，例如 SetAlpha() 和 GetAlpha()。例如，如果你将以下行的开头注释符号去掉

```csharp
// ob.alpha = 10; // Wrong! alpha is private!
```

你将无法编译此程序，因为会出现访问违规。虽然 MyClass 外部代码不允许访问 alpha，但 MyClass 内部定义的方法可以自由访问它，正如 SetAlpha() 和 GetAlpha() 方法所示。beta 也是如此。

关键点是：私有成员可以被其所在类的其他成员自由使用，但不能被类外部的代码访问。

## 应用公共与私有访问

正确使用 public 和 private 访问是成功面向对象编程的关键组成部分。虽然没有硬性规定，这里有一些作为指导的一般原则：

-   类中仅在类内部使用的成员应设为 private。
-   必须在特定范围内的数据应设为 private，并通过能够执行范围检查的公共方法提供访问。
-   如果更改某个成员会产生超出该成员本身的影响（即影响对象的其他方面），则该成员应设为 private，并且对其访问应受控制。
-   当使用不当会损害对象时，成员应设为 private。对这些成员的访问应通过防止不当使用的公共方法进行。
-   获取和设置私有数据值的方法必须是 public。
-   当没有理由将它们设为 private 时，公共实例变量是可以允许的。

当然，以上规则未涵盖的细微差别有很多，特殊情况会导致一条或多条规则被违反。但总的来说，如果你遵循这些规则，你将创建出不易被误用的健壮对象。

## 控制访问：案例研究

为了更好地理解访问控制背后的“如何”与“为何”，案例研究很有用。面向对象编程的典型示例之一是实现栈的类。正如你可能知道的，栈是一种实现后进先出列表的数据结构。它的名称来源于桌上盘子堆的类比。放在桌上的第一块盘子是最后才被使用的那一个。

栈是面向对象编程的经典示例，因为它将信息的存储与访问该信息的方法结合在一起。因此，栈是一种强制执行后进先出使用的引擎。这种组合非常适合于一个类，其中提供栈存储的成员是私有的，而公共方法提供访问。通过封装底层存储，使用栈的代码无法按顺序访问元素。

栈定义了两个基本操作：push 和 pop。push 将值放到栈顶。pop 从栈顶移除值。因此，pop 是消耗性的；一旦值从栈中弹出，它就被移除了，无法再次访问。

这里所示的示例创建了一个名为 Stack 的类来实现栈。栈的底层存储由一个私有数组提供。push 和 pop 操作可通过 Stack 类的公共方法使用。因此，公共方法强制执行后进先出机制。如图所示，Stack 类存储字符，但同样的机制也可用于存储任何类型的数据：

```csharp
// A stack class for characters.

using System;

class Stack {
    // These members are private.
    char[] stck; // holds the stack
    int tos;     // index of the top of the stack

    // Construct an empty Stack given its size.
    public Stack(int size) {
        stck = new char[size]; // allocate memory for stack
        tos = 0;
    }

    // Push characters onto the stack.
    public void Push(char ch) {
        if(tos==stck.Length) {
            Console.WriteLine(" -- Stack is full.");
            return;
        }

        stck[tos] = ch;
        tos++;
    }

    // Pop a character from the stack.
    public char Pop() {
        if(tos==0) {
            Console.WriteLine(" -- Stack is empty.");
            return (char) 0;
        }
        tos--;
        return stck[tos];
    }

    // Return true if the stack is full.
    public bool IsFull() {
        return tos==stck.Length;
    }

    // Return true if the stack is empty.
    public bool IsEmpty() {
        return tos==0;
    }

    // Return total capacity of the stack.
    public int Capacity() {
        return stck.Length;
    }

    // Return number of objects currently on the stack.
    public int GetNum() {
        return tos;
    }
}
```

让我们仔细检查这个类。Stack 类首先声明这两个实例变量：

```csharp
// These members are private.
char[] stck; // holds the stack
int tos;    // index of the top of the stack
```

stck 数组提供了栈的底层存储，在此情况下它保存字符。请注意，没有分配数组。实际数组的分配由 Stack 构造函数处理。tos 成员保存栈顶的索引。

tos 和 stck 成员都是私有的。这强制执行后进先出的栈机制。如果允许对 stck 进行公共访问，那么栈上的元素可能会被乱序访问。此外，由于 tos 保存栈中顶元素的索引，必须防止 Stack 类外部的代码操作 tos，以避免栈被破坏。对 stck 和 tos 的访问可通过稍后描述的各种公共方法间接提供给 Stack 的使用者。

栈构造函数如下所示：

```csharp
// Construct an empty Stack given its size.
public Stack(int size) {
    stck = new char[size]; // allocate memory for stack
    tos = 0;
}
```

构造函数接收期望的栈大小。它分配底层数组并将 tos 设置为零。因此，tos 的零值表示栈为空。

公共 Push() 方法将元素放到栈上。如下所示：

```csharp
// Push characters onto the stack.
public void Push(char ch) {
    if(tos==stck.Length) {
        Console.WriteLine(" -- Stack is full.");
        return;
    }

    stck[tos] = ch;
    tos++;
}
```

要压入栈的元素通过 ch 传入。在将元素添加到栈之前，会检查底层数组是否仍有空间。这是通过确保 tos 不超过 stck 的长度来完成的。如果仍有空间，元素将被存储在 stck 中由 tos 指定的索引处，然后 tos 自增。因此，tos 始终包含 stck 中下一个空闲元素的索引。

要从栈中移除元素，请调用公共方法 Pop()。如下所示：

```csharp
// Pop a character from the stack.
public char Pop() {
    if(tos==0) {
        Console.WriteLine(" -- Stack is empty.");
        return (char) 0;
    }

    tos--;
    return stck[tos];
}
```

这里检查 tos 的值。如果为零，则栈为空。否则，tos 递减，并返回该索引处的元素。

尽管 Push() 和 Pop() 是实现栈所需的唯一方法，但还有一些其他方法非常有用，Stack 类还定义了四个方法。它们是 IsFull()、IsEmpty()、Capacity() 和 GetNum()，它们提供有关栈状态的信息。如下所示：

```csharp
// Return true if the stack is full.
public bool IsFull() {
    return tos==stck.Length;
}

// Return true if the stack is empty.
public bool IsEmpty() {
    return tos==0;
}

// Return total capacity of the stack.
```
