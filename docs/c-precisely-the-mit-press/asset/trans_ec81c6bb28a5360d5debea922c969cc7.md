

88 表达式

## 12.20 类型转换表达式

类型转换表达式用于执行将值从一种类型显式转换为另一种类型（第 5.3 节）。当 e 是一个表达式而 t 是一个类型时，将 e 转换为 t 的转换通过使用表达式完成：

`(t)e`

该表达式在合法的情况下，类型为 t。它通过将 e 求值为值 v 来进行计算。如果 e 是简单类型且 t 是简单类型，则按照第 5.3.1 节中描述进行转换。

如果 e 是引用类型且存在从类型 e 到 t 的标准转换，那么如果 v 为 null，或者对对象或数组的引用可以隐式转换为 t，则转换成功且结果为 v；否则，将抛出 `InvalidCastException` 异常。

如果 e 是结构体类型且存在从类型 e 到 t 的标准转换（t 必须是接口、Object 或 ValueType），则转换成功，结果为 v 的装箱拷贝（boxed copy）。

如果 e 是类类型，且该类型或类型 t 声明了到类型 t 的转换，则使用该转换来获取结果。

如果 e 是简单类型且类型 e 声明了从类型 e 到类型 t 的转换，则使用该转换来获取结果。

当在编译时可以确定运行时不可能成功时，该类型转换是非法的并在编译时被拒绝；例如，当 e 的类型为 String 而 t 是 Array 时。当其中或两者都是接口时，无法在编译时确定。

如果第 12.13 节描述的实例测试 `e is t` 返回 true，则类型转换 `(t)` 将成功且不会抛出异常。反之则不成立。例如，转换 `(t)e` 可能在 e 求值为 null 的情况下仍然成功；它考虑了用户定义的转换，并考虑了简单类型的隐式转换，而实例测试 `e is` 正是这样做。

## 12.21 typeof 运算符

任何类型在运行时都可以由 System 命名空间下预定义类 `Type` 的对象表示。这对于伪类型 `void` 以及由泛型构造的类型（第 26.2 节）也是如此。对于任何给定的类型，都有唯一的 Type 对象。

表达式 `typeof(t)` 求值为代表类型 t 的 Type，而 `typeof(void)` 求值为代表 void 的类型对象。`typeof` 运算符可以应用于所有类型，甚至是涉及类型参数的类型（第 26.6 节）。

注意，虽然 `typeof(t)` 返回的是给定类型 t 的 Type 对象，但方法 `e.GetType()` 返回的是给定值 e 的运行时类型的 Type 对象。`GetType` 方法声明在 `Object` 类中，因此所有类型的值（匿名方法外）均可用；参见第 5.2 节和示例 8）。

## 表达式 89

## 示例 107 类型转换

尽管 `i` 为 false，但转换 `(long)i` 仍然成功。在像 `(C)s` 这样涉及用户定义转换的情况下，s 的类型必须与转换操作符声明的参数类型完全匹配。

```csharp
class B {
  class C : B {
    private String s;
    public C(String s) { this.s = s; }
    public static explicit operator C(String s) { return new C(s + s); }
  }
}

int i = 471;
long ll = (byte)i + (long)i; // 简单类型转换
String s = "ole";
B b1 = new C(""), b2 = new B();
C1 = (C)b1; // 成功，b1 是类 C
C2 = (C)b2; // 失败，b2 是类 B
C3 = (C)s; // 用户定义转换 String->C
Object o = (Object)s; // 总是成功
C4 = (C)(String)o; // 成功，Object-->String-->C
C5 = (o); // 失败，没有 Object-->C 转换
Array arr = (Array)s; // 编译时拒绝
```

## 示例 108 typeof 运算符

```csharp
interface I {
  class B : I {
    delegate void D(int i);
  }
  struct S : I {}
  class G { public static void WriteType<T>() { Console.WriteLine(typeof(T)); } }
}

Console.WriteLine(typeof(String)); // System.String
Console.WriteLine(typeof(int)); // System.Int32 (int)
Console.WriteLine(typeof(double)); // System.Double (double)
Console.WriteLine(typeof(int[])); // System.Int32[]
Console.WriteLine(typeof(int[][])); // System.Int32[][]
Console.WriteLine(typeof(int[][])); // System.Int32[][][]
Console.WriteLine(typeof(void)); // System.Void
Console.WriteLine(typeof(B)); // B
Console.WriteLine(typeof(C)); // C
Console.WriteLine(typeof(I)); // I
Console.WriteLine(typeof(D)); // D
Console.WriteLine(typeof(S)); // S
Console.WriteLine(typeof(int)); // System.Int32
Console.WriteLine(typeof(G<String>)); // G[System.String]
G<int>.WriteType(); // System.Int32
Console.WriteLine(typeof(int)==typeof(Int32)); // True
```

## 匿名方法表达式

匿名方法表达式是一个求值为委托（delegate）或无名方法的表达式。这类似于 Lisp 和 Scheme (lambda)、Standard ML (fn) 以及其他函数式语言中常见的无名函数。匿名方法对于向库传递行为（例如比较器 (15)）非常方便；这种目的可以通过匿名内部类来实现。匿名方法表达式具有以下形式之一：

- delegate-语句
- delegate(形式参数列表) 块-语句

形式参数列表（formal-list）与方法（第 10.7 节）相似，但它不能包含参数数组 (`params`) 或可选参数 (10)。块语句（block-statement）是匿名方法的体。没有 `goto` 或 `continue` 语句可以离开块语句。

匿名方法可以使用闭包函数中绑定的局部变量和参数。在非静态代码中，类中的匿名方法表达式不能使用当前的当前实例 `this`（第 14.2 节）。

匿名方法可以隐式转换为委托类型（17）。第一种匿名方法与任何形式参数列表不包含 `out` 参数的委托 D 兼容。第二种匿名方法如果其形式参数列表具有相同的参数以及 `ref/out` 修饰符，则与委托 D 兼容；此外，该委托类型具有参数数组 (`params`)，且在匿名方法中没有匹配项。在这两种情况下，如果 D 的返回类型为 `void`，则块语句中的任何 `return` 语句都不能返回值。相反，如果 D 的返回类型为 `t`，则块语句中的每个 `return` 语句必须有一个可以隐式转换为 `t` 的参数，且块语句的结尾必须可达。

匿名方法转换为委托后，可以像委托一样调用（第 17 节）。委托调用的参数将被求值。在匿名方法的种形式中，参数值将被忽略；在第二种形式中，它们将绑定到匿名方法的的形式参数上。匿名方法将求值，如果它执行了 `return` 语句，则匿名方法将终止。

