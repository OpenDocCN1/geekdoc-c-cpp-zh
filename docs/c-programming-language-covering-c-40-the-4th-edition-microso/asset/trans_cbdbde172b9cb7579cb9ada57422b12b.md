
在上面的示例中，构造类型 D<int> 具有一个非继承成员 public int G(string s)，它是通过用类型实参 int 替换类型参数 T 得到的。D<int> 还具有一个来自类声明 B 的继承成员。该继承成员的确定方式是：首先通过在基类规范 B<T[]> 中将 T 替换为 int，确定 D<int> 的基类类型 B<int[]>。然后，作为 B 的类型实参，将 int[] 替换 public U F(long index) 中的 U，从而得到继承成员 public int[] F(long index)。

## 10.3.4 new 修饰符

类成员声明允许声明与继承成员具有相同名称或签名的成员。发生这种情况时，称派生类成员隐藏了基类成员。隐藏继承成员不被视为错误，但确实会导致编译器发出警告。若要抑制该警告，派生类成员的声明可以包含 new 修饰符，以指示该派生成员意图隐藏基成员。本主题在 §3.7.1.2 中进一步讨论。

如果声明中包含 new 修饰符，但并未隐藏继承成员，则会发出相应警告。通过移除 new 修饰符可抑制该警告。

## 10.3.5 访问修饰符

类成员声明可以具有五种可能的声明可访问性之一（§3.5.1）：public、protected internal、protected、internal 或 private。除 protected internal 组合外，指定多个访问修饰符是编译时错误。当类成员声明不包含任何访问修饰符时，假定为 private。

## 10.3.6 组成类型

成员声明中使用的类型称为该成员的组成类型。可能的组成类型包括：常量、字段、属性、事件或索引器的类型；方法或运算符的返回类型；以及方法、索引器、运算符或实例构造函数的参数类型。成员的组成类型必须至少与该成员本身一样可访问（§3.5.4）。

## 10.3.7 静态成员和实例成员

类成员要么是静态成员，要么是实例成员。一般来说，将静态成员视为属于类类型、实例成员视为属于对象（类类型的实例）是有用的。

当字段、方法、属性、事件、运算符或构造函数声明包含 static 修饰符时，它声明静态成员。此外，常量或类型声明隐式声明静态成员。静态成员具有以下特征：

- 当在形式为 E.M 的成员访问（§7.6.4）中引用静态成员 M 时，E 必须表示包含 M 的类型。E 表示实例是编译时错误。
- 静态字段标识一个存储位置，由给定封闭类类型的所有实例共享。无论创建给定封闭类类型的多少个实例，静态字段始终只有一个副本。
- 静态函数成员（方法、属性、事件、运算符或构造函数）不对特定实例进行操作，在此类函数成员中引用 this 是编译时错误。

当字段、方法、属性、事件、索引器、构造函数或析构函数声明不包含 static 修饰符时，它声明实例成员。（实例成员有时称为非静态成员。）实例成员具有以下特征：

- 当在形式为 E.M 的成员访问（§7.6.4）中引用实例成员 M 时，E 必须表示包含 M 的类型的实例。E 表示类型是绑定期错误。
- 类的每个实例都包含该类所有实例字段的一组单独副本。
- 实例函数成员（方法、属性、索引器、实例构造函数或析构函数）对类的给定实例进行操作，并且可以通过 this（§7.6.7）访问该实例。

以下示例说明访问静态成员和实例成员的规则：

```
class Test
{
    int x;
    static int y;

    void F() {
        x = 1;        // Okay: same as this.x = 1
        y = 1;        // Okay: same as Test.y = 1
    }

    static void G() {
        x = 1;        // Error: cannot access this.x
        y = 1;        // Okay: same as Test.y = 1
    }
}
```

```
    static void Main() {
        Test t = new Test();       // Okay
        t.x = 1;                   // Error: cannot access static
        t.y = 1;                   //        member through instance
        Test.x = 1;                // Error: cannot access instance member
                                   //        through type
        Test.y = 1;                // Okay
    }
```

F 方法表明，在实例函数成员中，可以使用*简单名称*（§7.6.2）访问实例成员和静态成员。G 方法表明，在静态函数成员中，通过*简单名称*访问实例成员是编译时错误。Main 方法表明，在*成员访问*（§7.6.4）中，实例成员必须通过实例访问，静态成员必须通过类型访问。

## 10.3.8 嵌套类型

在类或结构体声明中声明的类型称为*嵌套类型*。在编译单元或命名空间中声明的类型称为*非嵌套类型*。

> > **乔恩·斯基特** 我听到“顶级类型”这个说法比“非嵌套类型”更常用——而且我毫不怀疑我自己也传播过这个非标准术语。考虑到绝大多数类型都是非嵌套的，感觉描述性术语应该是正面的，而不只是表示没有嵌套。不管怎样，这就是我的借口，其他人也欢迎借用。

在示例

```
    using System;
    class A
    {
        class B
        {
            static void F() {
                Console.WriteLine("A.B.F");
            }
        }
    }
```

中，类 B 是嵌套类型，因为它声明在类 A 中；类 A 是非嵌套类型，因为它声明在编译单元中。

> > **布拉德·艾布拉姆斯** 我并不太喜欢可重用库中的公开可访问嵌套类型。嵌套类型的可发现性并不好。更重要的是，我们已经有一种分组机制——命名空间——应该用它来表示相关类型。

### 10.3.8.1 完全限定名

嵌套类型的完全限定名（§3.8.1）为 S.N，其中 S 是声明类型 N 的类型的完全限定名。

### 10.3.8.2 声明可访问性

非嵌套类型可以具有 public 或 internal 声明可访问性，默认具有 internal 声明可访问性。嵌套类型也可以具有这些形式的声明可访问性，另外还可以具有一种或多种其他形式的声明可访问性，具体取决于包含类型是类还是结构体：

- 在类中声明的嵌套类型可以具有五种声明可访问性中的任意一种（public、protected internal、protected、internal 或 private），并且与其他类成员一样，默认具有 private 声明可访问性。
- 在结构体中声明的嵌套类型可以具有三种声明可访问性中的任意一种（public、internal 或 private），并且与其他结构体成员一样，默认具有 private 声明可访问性。

示例

```
```csharp
public class List
{
    // Private data structure
    private class Node
    {
        public object Data;
        public Node Next;

        public Node(object data, Node next) {
            this.Data = data;
            this.Next = next;
        }
    }

    private Node first = null;
    private Node last = null;

    // Public interface
    public void AddToFront(object o) {...}
```
```

```
~~~csharp
        public void AddToBack(object o) {...}
        public object RemoveFromFront() {...}
        public object RemoveFromBack() {...}
        public int Count { get {...} }
        }
~~~
```

声明了一个私有嵌套类 Node。

### 10.3.8.3 *隐藏*

嵌套类型可以隐藏（§7.3.1）基成员。嵌套类型声明上允许使用 *new* 修饰符，以便可以显式表达隐藏。示例

```
~~~csharp
class Base
{
    public static void M() {
        Console.WriteLine("Base.M");
    }
}
class Derived: Base
{
    new public class M
    {
        public static void F() {
            Console.WriteLine("Derived.M.F");
        }
    }
}
class Test
{
    static void Main() {
        Derived.M.F();
    }
}
~~~
```

展示了一个嵌套类 M，它隐藏了 Base 中定义的方法 M。

### 10.3.8.4 *this* 访问

嵌套类型与其包含类型在 *this 访问*（§7.6.7）方面没有特殊关系。具体而言，嵌套类型中的 *this* 不能用于引用包含类型的实例成员。在嵌套类型需要访问其包含类型的实例成员的情况下，可以通过提供来提供访问
