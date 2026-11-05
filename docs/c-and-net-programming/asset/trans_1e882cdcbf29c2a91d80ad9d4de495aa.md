
## 5.1 使用方法的优点

- 1. 减少代码重复。
- 2. 将复杂问题分解为更简单的部分，从而为程序带来模块化。
- 3. 提高代码的清晰度。
- 4. 代码复用。
- 5. 信息隐藏。
- 6. 代码隔离，有助于轻松追踪错误和调试。

## 5.2 静态方法

### 概念

- 1. 静态方法直接从类级别调用，无需创建对象。静态方法在调用时不需要对象实例。

### 解释

- 2. 静态方法没有实例。它们通过类型名调用，而不是通过标识符调用。它们可以是 public 或 private。要调用静态方法，请使用类名和点运算符。
- 3. 静态方法只能使用静态成员变量。
- 4. 静态方法常用于表示不随对象状态变化的数据或计算。一个例子是数学库，其中包含用于各种计算的静态方法。
- 5. 关键字 'static' 用于声明静态方法。当不存在 static 修饰符时，该方法称为实例方法。
- 6. 不能在静态方法中使用 this 关键字。它只能在实例方法中使用。
- 8. Main() 方法是 C# 控制台和 GUI 应用程序的入口点。在 C# 中，Main() 方法必须是静态的。在应用程序启动之前，尚未创建任何对象。
- 9. 要调用非静态方法，需要有一个对象实例。静态方法在类实例化之前就存在，因此 static 被应用于主入口点。

### 示例

```csharp
//Illustration of keyword static
/* Note
A static method can only work with static variables.
Show() is static method. It works with a static member n.
Basic.Show(); //To invoke a static method, there is no need of object instance. Method is called by using the name of the class and the dot operator.
*/

using System;

public class StaticDemo
{
    static int n = 657;

    public static void Show()
    {
        Console.WriteLine("The number is: {0}", n);
    }
}

public class StaticMethod
{
    static void Main()
    {
        StaticDemo.Show();
    }
}
```

输入：无

### 输出

该数字是 657。

## 5.3 实例方法

### 概念

- 1. 类中的实例方法使用属于该类的 public、private 或 static 数据。

### 解释

- 2. 用户可以使用类的对象访问方法。在声明中，将方法名放在点运算符之前。

### 示例

```csharp
// Illustration of Instance methods.
class InstanceDemo
{
    void method1()
    {
        Console.WriteLine("First Instance method.");
    }
    void method2()
    {
        Console.WriteLine("Second Instance method.");
    }
    static void Main(string[] args)
    {
        InstanceDemo obj = new InstanceDemo();
        obj.method1();
        obj.method2();
        Console.Read();
    }
}
```

输入：无

### 输出

| 输出 |
|---|
| 第一个实例方法。 |
| 第二个实例方法。 |

## 5.4 匿名方法

### 概念

- 1. 匿名方法是内联方法，没有名称。
- 2. 匿名方法通过消除创建单独方法的需要来减少编码开销。
- 3. 如果没有匿名方法，开发人员常常不得不创建类的实例，仅仅为了调用一个方法。

### 解释

### 示例

```csharp
//Illustration of anonymous method
using System;
using System.Timers;

public class AnonymousMethod
{
    static void Main()
    {
        Timer objtimer = new Timer();

        /*A Timer class generates recurring events in an application.*/
        objtimer.Elapsed += new ElapsedEventHandler(
            delegate(object source, ElapsedEventArgs e)
            {
                Console.WriteLine("Event triggered at {0}", e.SignalTime);
            }
        );
        objtimer.Interval = 2000;// timer object is created every 2 seconds
        objtimer.Enabled = true;

        Console.ReadLine();
    }
}
```

输入：无

### 输出

事件在 (?????) 触发 [实际输出将取决于系统时间。]

## 5.5 方法重载

这个概念将在第 8 章学习。参见 8.2 节。

## 5.6 隐藏方法、重写方法和密封方法

这些概念将在第 8 章和第 9 章学习。

密封方法参见 8.1 节。

重写参见 9.3 节。

方法隐藏参见 9.4 节。

AU: May-19

## 5.7 不安全方法或不安全块

- 1. 不安全代码是已进行指针操作的代码。
- 2. **C# 中不安全代码的优点**
  - 1. 性能和灵活性得到增强，因为使用指针可以以尽可能高效的方式访问和操作数据。
  - 2. 兼容性是使用指针的主要原因，因为旧的 Windows API 广泛使用指针。许多第三方 DLL 可能通过指针参数提供其功能。（尽管在 DLL 使用中可以通过编写 DllImport 声明来避免指针。）
  - 3. 如果需要访问内存地址，那么不使用指针就无法知道某些数据的内存地址。
- 3. **C# 中不安全代码的缺点**
  - 1. 指针的语法复杂。
  - 2. 从逻辑上讲，指针更难使用。如果使用方式或步骤不当，可能会导致糟糕的情况，例如：
    - 覆盖其他变量。
    - 栈溢出。
    - 访问那些并不包含任何数据的内存区域，却把它们当作包含数据来访问。
    - 覆盖 .NET 运行时所用代码的某些信息，这必然会导致应用程序崩溃。
  - 3. 包含指针的代码很难调试，因为它可能突然崩溃。
  - 4. .NET 支持类型安全，而使用指针会破坏类型安全。这也可能导致代码无法执行。
- 4. **不安全代码的特征**
  - 1. 方法、类型和代码块可以定义为不安全。
  - 2. 在某些情况下，不安全代码可以通过移除数组边界检查来提高应用程序的性能。
  - 3. 当调用需要指针的本机函数时，必须使用不安全代码。
  - 4. 要让 C# 编译不安全代码，应用程序必须使用 /unsafe 进行编译。

### 示例

```csharp
//illustration of unsafe method
using System;

class Book {
    public static void Main() {
        findBook();
    }
}

public static unsafe void testFun() {
    int bkID = 25;
    int* ptrbkID = &bkID;
    Console.WriteLine("Book is " + bkID);
    Console.WriteLine("Book Memory Address is " + (int) ptrbkID );
}
```

```csharp
//illustration of unsafe block
using System;

class Number {
    public static void Main() {
        ChangeVal Obj = new ChangeVal();
        unsafe {
            int no1 = 125;
            int no2 = 235;
            Console.WriteLine("Before swap = number1" + no1 + " number2= " + no2);
            Obj.swapVal(&no1, &no2);
            Console.WriteLine("After swap = number1" + no1 + " number2= " + no2);
        }
    }
}
class ChangeVal {
    public unsafe void swapVal(int* ptr1, int* ptr2) {
        int tmp = *ptr1;
        *ptr1 = *ptr2;
        *ptr2 = tmp;
    }
}
```

## 两分题及答案

**Q.1 public、static 和 void 有什么区别？**

**答：** 用 public 声明的变量或方法可在应用程序中的任何位置访问。用 static 声明的变量或方法无需创建类的实例即可全局访问。静态成员默认并非全局可访问；这取决于所使用的访问修饰符类型。编译器将该方法的地址存储为入口点，并在创建任何对象之前使用此信息开始执行。而 void 是一种类型修饰符，表示该方法或变量不返回任何值。

**Q.2 什么是内联函数？**

**答：** 内联函数是编译器使用的一种技术，它指示将函数的完整主体插入到程序源代码中使用该函数的每个位置。

**Q.3 重载和重写的主要区别是什么？**

**答：** 重载是静态绑定，而重写是动态绑定。重载不过是同一方法使用不同参数，并且在同一个类中它可能返回也可能不返回相同的值。
