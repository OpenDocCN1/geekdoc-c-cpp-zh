
```
delegate void D(int x);
class C
{
    public static void M1(int i) {
        Console.WriteLine("C.M1: " + i);
    }
    public static void M2(int i) {
        Console.WriteLine("C.M2: " + i);
    }

    public void M3(int i) {
        Console.WriteLine("C.M3: " + i);
    }
}
class Test
{
    static void Main() {
        D cd1 = new D(C.M1);
        cd1(-1);    // call M1

        D cd2 = new D(C.M2);
        cd2(-2);    // call M2

        D cd3 = cd1 + cd2;
        cd3(10);    // call M1 then M2

        cd3 += cd1;
        cd3(20);    // call M1, M2, then M1

        C c = new C();
        D cd4 = new D(c.M3);
        cd3 += cd4;
        cd3(30);    // call M1, M2, M1, then M3

        cd3 -= cd1; // remove last M1
        cd3(40);    // call M1, M2, then M3

        cd3 -= cd4;
        cd3(50);    // call M1 then M2

        cd3 -= cd2;
        cd3(60);    // call M1
        cd3 -= cd2; // impossible removal is benign
        cd3(60);    // call M1

        cd3 -= cd1; // invocation list is empty so cd3 is null
        // cd3(70);  // System.NullReferenceException thrown
        cd3 -= cd1; // impossible removal is benign
    }
}
```

如语句 cd3 += cd1; 所示，一个委托可以在调用列表中出现多次。在这种情况下，它会按出现次数各调用一次。在此类调用列表中，当该委托被移除时，实际被移除的是调用列表中最后一次出现的位置。

在最后一条语句 cd3 -= cd1; 执行之前，委托 cd3 引用的是一个空的调用列表。尝试从空列表中移除一个委托（或从非空列表中移除一个不存在的委托）不会导致错误。

The output produced is:

```
C.M1: -1
C.M2: -2

C.M1: 10
C.M2: 10

C.M1: 20
C.M2: 20
C.M1: 20

C.M1: 30
C.M2: 30
C.M1: 30
C.M3: 30

C.M1: 40
C.M2: 40
C.M3: 40

C.M1: 50
C.M2: 50

C.M1: 60
C.M1: 60
```

end example]

## 21. 异常

### 21.1 通用

C# 中的异常提供了一种结构化、统一且类型安全的方式来处理系统级和应用级的错误条件。

### 21.2 异常的原因

异常可以通过两种不同的方式抛出。

- throw 语句 (§13.10.6) 会立即且无条件地抛出异常。控制流永远不会到达 throw 之后的下一条语句。
- 在处理 C# 语句和表达式期间出现的某些异常条件会在操作无法正常完成时在某些情况下导致异常抛出。[示例：整数除法操作 (§12.9.3) 如果分母为零则会抛出 System.DivideByZeroException。end example] 请参阅 §21.5 以了解以这种方式可能发生的各种异常的列表。

### 21.3 System.Exception 类

System.Exception 类是所有异常的基础类型。该类具有一些所有异常共有的显著属性：

- Message 是类型为 string 的只读属性，包含异常原因的可读描述。
- InnerException 是类型为 Exception 的只读属性。如果其值非 null，则引用导致当前异常的异常。（即，当前异常是在处理 InnerException 的 catch 块中引发的。）否则，其值为 null，表示此异常不是由另一个异常引起的。以这种方式链接在一起的异常对象的数量可以是任意的。

这些属性的值可以在对 System.Exception 的实例构造函数调用中指定。

### 21.4 异常如何被处理

异常由 try 语句 (§13.11) 处理。

当异常发生时，系统会根据异常的运行时类型搜索最近的可以处理该异常的 catch 子句。首先在当前方法中搜索词法上包围的 try 语句，并按顺序考虑该 try 语句关联的 catch 子句。如果失败，则在调用当前方法的方法中搜索词法上包围的 try 语句。此搜索会一直继续，直到找到可以处理当前异常的 catch 子句为止，该子句通过命名与被抛出的异常的运行时类型相同或为其基类的异常类来处理。未命名异常类的 catch 子句可以处理任何异常。

一旦找到匹配的 catch 子句，系统就会准备将控制权转移到该 catch 子句的第一条语句。在 catch 子句执行开始之前，系统首先按顺序执行与比捕获异常的 try 语句嵌套更深的 try 语句关联的任何 finally 子句。

如果没有找到匹配的 catch 子句：

- 如果搜索匹配的 catch 子句到达静态构造函数 (§15.12) 或静态字段初始化器，则会在触发静态构造函数调用的位置抛出 System.TypeInitializationException。System.TypeInitializationException 的内部异常包含最初抛出的异常。
- 否则，如果在终结器执行期间发生异常且该异常未被捕获，则行为未指定。
- 否则，如果搜索匹配的 catch 子句到达最初启动线程的代码，则线程的执行将被终止。此类终止的影响由实现定义。

### 21.5 常见异常类

以下异常由某些 C# 操作抛出。

| 异常 | 描述 |
|---|---|
| System.ArithmeticException | 用于在算术运算期间发生的异常的基类，例如 System.DivideByZeroException 和 System.OverflowException。 |
| System.ArrayTypeMismatchException | 当向数组存储失败，因为存储元素的类型与数组的类型不兼容时抛出。 |
| System.DivideByZeroException | 当尝试将整数值除以零时抛出。 |
| System.IndexOutOfRangeException | 当尝试通过小于零或超出数组边界的索引来索引数组时抛出。 |
| System.InvalidCastException | 当从基类型或接口到派生类型的显式转换在运行时失败时抛出。 |
| System.NullReferenceException | 当空引用以需要引用对象的方式使用时抛出。 |
| System.OutOfMemoryException | 当尝试分配内存（通过 new）失败时抛出。 |
| System.OverflowException | 当在检查上下文中的算术运算溢出时抛出。 |
| System.StackOverflowException | 当执行栈因挂起的调用过多而耗尽时抛出；通常表示递归非常深或无界。 |
| System.TypeInitializationException | 当静态构造函数或静态字段初始化器抛出异常且不存在 catch 子句来捕获它时抛出。 |

## 22. 属性

### 22.1 通用

C# 语言的大部分功能使程序员能够指定程序中定义的实体的声明性信息。例如，类中方法的访问性是通过用方法修饰符 public、protected、internal 和 private 对其进行装饰来指定的。

C# 使程序员能够发明新的声明性信息类型，称为属性。然后程序员可以将属性附加到各种程序实体，并在运行时环境中检索属性信息。[注意：例如，一个框架可能会定义一个 HelpAttribute 属性，该属性可以放置在某些程序元素（如类和方法）上，以提供这些程序元素与其文档之间的映射。end note]

属性是通过属性类的声明来定义的 (§22.2)，属性类可以具有位置参数和命名参数 (§22.2.3)。属性使用属性规范 (§22.3) 附加到 C# 程序中的实体，并且可以在运行时作为属性实例 (§22.4) 检索。

### 22.2 属性类

#### 22.2.1 通用

派生自抽象类 System.Attribute 的类，无论是直接还是间接，都称为属性类。属性类的声明定义了一种可以放置在程序实体上的新属性类型。根据惯例，属性类以 Attribute 为后缀命名。使用属性时可以包含或省略此后缀。

泛型类声明不得将 System.Attribute 用作直接或间接基类。[示例:
```
using System;
public class B : Attribute {}
public class C<T> : B {}  // Error - generic cannot be an attribute
```
end example]

#### 22.2.2 属性用法

属性 AttributeUsage (§22.5.2) 用于描述属性类如何被使用。

AttributeUsage 具有一个位置参数 (§22.2.3)，使属性类能够指定其可以使用的程序实体的种类。[示例：示例
```
using System;
[AttributeUsage(AttributeTargets.Class | AttributeTargets.Interface)]
public class SimpleAttribute: Attribute
{ ... }
```
