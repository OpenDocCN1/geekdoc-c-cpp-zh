
## 12.19 索引器访问表达式

索引 `get` 访问必须具有以下形式之一：

- `o[actual-list]`
- `this[actual-list]`
- `base[actual-list]`

其中 `o` 是引用类型的表达式。在第一种情况下，`o` 的类型必须具有给定参数类型的索引器。在第二种情况下，当前类必须（声明或继承）具有给定参数类型的索引器。在第三种情况下，当前类的基类必须具有给定参数类型的索引器。在每种情况下，表达式的类型都是索引器的声明类型。`get` 访问通过评估 `o`（如果存在），然后评估 `actual-list` 中的表达式以获取参数值，并将其隐式转换为索引器形式参数的类型来实现。

### 88 表达式

## 12.20 类型转换表达式

类型转换表达式用于执行将值从一种类型显式转换为另一种类型（第 5.3 节）。当 `e` 是一个表达式而 `t` 是一个类型时，将 `e` 转换为 `t` 的转换通过使用表达式完成：

`(`t`)`e`

该表达式在合法的情况下，类型为 `t`。它通过将 `e` 求值为值 `v` 来进行计算。如果 `e` 是简单类型且 `t` 是简单类型，则按照第 5.3.1 节中描述进行转换。

如果 `e` 是引用类型且存在从类型 `e` 到 `t` 的标准转换，那么如果 `v` 为 `null`，或者对对象或数组的引用可以隐式转换为 `t`，则转换成功且结果为 `v`；否则，将抛出 `InvalidCastException` 异常。

如果 `e` 是结构体类型且存在从类型 `e` 到 `t` 的标准转换（`t` 必须是接口、`Object` 或 `ValueType`），则转换成功，结果为 `v` 的装箱拷贝（boxed copy）。

如果 `e` 是类类型，且该类型或类型 `t` 声明了到类型 `t` 的转换，则使用该转换来获取结果。

如果 `e` 是简单类型且类型 `e` 声明了从类型 `e` 到类型 `t` 的转换，则使用该转换来获取结果。

当在编译时可以确定运行时不可能成功时，该类型转换是非法的并在编译时被拒绝；例如，当 `e` 的类型为 `String` 而 `t` 是 `Array` 时。当其中或两者都是接口时，无法在编译时确定。

如果第 12.13 节描述的实例测试 `e is t` 返回 `true`，则类型转换 `(`t`)` 将成功且不会抛出异常。反之则不成立。例如，转换 `(`t`)`e` 可能在 `e` 求值为 `null` 的情况下仍然成功；它考虑了用户定义的转换，并考虑了简单类型的隐式转换，而实例测试 `e is` 正是这样做。

## 12.21 typeof 运算符

任何类型在运行时都可以由 `System` 命名空间下预定义类 `Type` 的对象表示。这对于伪类型 `void` 以及由泛型构造的类型（第 26.2 节）也是如此。对于任何给定的类型，都有唯一的 `Type` 对象。

表达式 `typeof(`t`)` 求值为代表类型 `t` 的 `Type`，而 `typeof(void)` 求值为代表 `void` 的类型对象。`typeof` 运算符可以应用于所有类型，甚至是涉及类型参数的类型（第 26.6 节）。

注意，虽然 `typeof(`t`)` 返回的是给定类型 `t` 的 `Type` 对象，但方法 `e.GetType()` 返回的是给定值 `e` 的运行时类型的 `Type` 对象。`GetType` 方法声明在 `Object` 类中，因此所有类型的值（匿名方法外）均可用；参见第 5.2 节和示例 8）。

### 表达式 89

## 示例 107 类型转换

尽管 `i` 为 `false`，但转换 `(`long`)`i` 仍然成功。在像 `(`C`)`s` 这样涉及用户定义转换的情况下，`s` 的类型必须与转换操作符声明的参数类型完全匹配。

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

匿名方法表达式是一个求值为委托（delegate）或无名方法的表达式。这类似于 Lisp 和 Scheme (`lambda`)、Standard ML (`fn`) 以及其他函数式语言中常见的无名函数。匿名方法对于向库传递行为（例如比较器 (15)）非常方便；这种目的可以通过匿名内部类来实现。匿名方法表达式具有以下形式之一：

- `delegate`-语句
- `delegate(`形式参数列表`)` 块-语句

形式参数列表（formal-list）与方法（第 10.7 节）相似，但它不能包含参数数组 (`params`) 或可选参数 (10)。块语句（block-statement）是匿名方法的体。没有 `goto` 或 `continue` 语句可以离开块语句。

匿名方法可以使用闭包函数中绑定的局部变量和参数。在非静态代码中，类中的匿名方法表达式不能使用当前的当前实例 `this`（第 14.2 节）。

匿名方法可以隐式转换为委托类型（17）。第一种匿名方法与任何形式参数列表不包含 `out` 参数的委托 `D` 兼容。第二种匿名方法如果其形式参数列表具有相同的参数以及 `ref/out` 修饰符，则与委托 `D` 兼容；此外，该委托类型具有参数数组 (`params`)，且在匿名方法中没有匹配项。在这两种情况下，如果 `D` 的返回类型为 `void`，则块语句中的任何 `return` 语句都不能返回值。相反，如果 `D` 的返回类型为 `t`，则块语句中的每个 `return` 语句必须有一个可以隐式转换为 `t` 的参数，且块语句的结尾必须可达。

匿名方法转换为委托后，可以像委托一样调用（第 17 节）。委托调用的参数将被求值。在匿名方法的种形式中，参数值将被忽略；在第二种形式中，它们将绑定到匿名方法的的形式参数上。匿名方法将求值，如果它执行了 `return` 语句，则匿名方法将终止。

## 示例 109 匿名方法的兼容性

匿名方法 `d11` 兼容 `D1` 但不兼容 `D2`；匿名方法 `d21` 兼容 `D2` 但不兼容 `D1`；而 `d22` 兼容 `D2` 和 `D3` 但不兼容 `D1`。这些匿名方法均都不兼容 `D4`。`foreach` 循环调用了匿名方法；对 `d21` 的每次调用以及由 `M(4)` 创建的匿名方法的调用都会使 `ref` 参数 `y` 增加 1。

```csharp
delegate D1(int x, ref int y, int z);
delegate D2(int x, ref int y, int z);
delegate D3(int x);
delegate D4(int x, ref int y);
class {
    static D1 d1 = delegate(int x, ref int y, int z) { z = y++; return x + y; };
    static D2 d21 = delegate(int x, ref int y) { y+=2; return x + y; };
    static D2 d22 = delegate { { return 5; };
    public static D2 M(int mx) {
        if (mx < 6)
            return delegate (int x, ref int y) { y+=2; return x + y; };
        else
            return delegate { return mx; }
    }
    public static void Main(String[] args) {
        D2[] ds = { d21, d22, M(4), M(7), delegate { return 8; } };
        int y = 0;
        foreach (D2 d in ds)
            Console.WriteLine(d, y); // Prints 4 5 6 7 8
        Console.WriteLine(y); // Prints 4
    }
}
```

# 示例 110 匿名方法捕获的局部变量

局部变量 `u` 和 `v` 被捕获在循环体内的匿名方法中。由于 `u` 在 `for` 循环外部声明，因此只会创建一个变量实例，且 `udlg` 中的所有匿名方法都引用该实例。由于 `v` 是在内部声明的，循环的每次迭代都会创建一个变量的独立实例，且 `vdlg` 中的每个匿名方法都有自己的实例。因此，单个的 `u` 被增加了五次，而每个 `v` 被增加了一次。

```csharp
public static void Main(String[] args) {
    D[] udlgs = new D[5], vdlg = new D[5];
    int u = 0;
    for (int i=0; i<5; i++) {
        int v = 0;
        udlgs[i] = delegate () { u++; Console.Write(u); };
        vdlg[i] = delegate () { v++; Console.Write(v); };
    }
    foreach (D lg in udlgs) lg(); // Prints 12345
    foreach (D lg in vdlg) lg(); // Prints 11111
}
delegate void D();
```

### 92 表达式

## 12.23 Lambda 表达式 (C# 3.0)

Lambda 表达式类似于匿名方法表达式（第 12.22 节），但语法更紧凑。它的基本形式为：

```
x => e
(xt, ..., xn) => e
(parameter-modifier t1 x1, ..., parameter-modifier tn xn) => e
```

`x` 和 `xi` 是参数，表达式是 Lambda 表达式的体，`ti` 是参数类型，而 `parameter-modifier` 是 `ref` 或 `out`。Lambda 表达式不能接受参数数组（`params`；见第 10.7 节）或可选参数（第 10.10 节）。根据匿名方法的规则（第 12.22 节），`e` 可以引用封闭作用域内的变量和参数。

Lambda `x => e` 的值是一个委托对象，当应用于参数 `x` 时，它将评估表达式并返回结果。类似于匿名方法，Lambda 表达式本身没有类型，但可以转换为与参数类型以及 `e` 的类型（返回类型）一致的委托类型。当 Lambda 表达式的参数类型未指定时，编译器会尝试使用上下文信息来推断它们，例如 Lambda 表达式所赋值的变量或方法的类型（示例 111）。

# 12.24 匿名对象表达式 (C# 3.0)

匿名对象求值为一个具有只读字段的对象：

```
new { xi = ei, ..., xn = en }
```

`xi` 是标识符，`ei` 是从左到右求值的表达式，用于获取 `xi` 的值。当 `ei` 是标识符 `x` 或字段或属性访问 `e.f` 时，可以省略 `xi=`，在这种情况下，标识符 `x` 或标识符 `f` 将被用于 `xi`。

生成的匿名对象具有只读属性，返回创建时给的值。表达式的类型是匿名类型。在同一个程序集内（第 1.1 节），所有具有相同字段且顺序相同的匿名表达式都具有相同的匿名类型。匿名对象的 `Equals` 和 `GetCode` 方法已根据其内部的字段值进行了重写。`ToString` 方法显示对象的字段值。匿名对象表达式用于 LINQ 查询的实现（示例 242）。

# 12.25 隐式类型数组创建表达式 (C# 3.0)

一维数组的隐式类型数组创建的格式如下：

```
new [] { xi = ei, ..., xn = en }
```

与普通数组创建（第 9 节）的区别在于，隐式类型格式没有指定新创建数组的类型；这对于一个用匿名对象表达式初始化的数组来说是不可能的。前面的表达式创建了一个长度为 `n` 的数组，其元素类型是所有 `ei` 类型中的最佳类型。`ei` 从左到右求值。矩形多维数组 `new[] { { ... }, ..., { ... } }` 如第 9.2 节所示创建。

### 示例 111 Lambda 表达式

Lambda 表达式如 `(s => s.Length==3)` 是一个谓词，用于测试 `(String)` 参数长度是否为 3。典型用法是过滤掉可枚举中具有特定属性的项。示例 `f1` 和 `f2` 显示同一个表达式可以用于不同的类型。由于 Lambda 表达式本身没有类型（当指定参数时），它不能赋值给类型不是 `Object` 或 `dynamic` 的 `var` 声明变量。

变量 `f3` 和 `f4` 显示了相同的加 `x` 和 `y` 的函数，但 `f1` 同时接收两个参数，而 `f2` 返回一个接受 `x` 和 `y` 然后返回 `x+y` 的函数。该函数是。

### 示例 112 匿名对象

匿名对象求值为一个具有只读字段的对象：

```csharp
new { xi = ei, ..., xn = en }
```

### 示例 113 隐式类型数组

一维数组的隐式类型数组创建的格式如下：

```
new [] { xi = ei, ..., xn = en }
```

# 语句 95

## 示例 114 语句终止
语句的执行可能会 (1) 正常终止，意味着执行将继续执行下一个语句（如果有的话）；或 (2) 通过抛出异常异常终止；或 (3) 在方法或构造函数内部通过执行 `return` 语句退出；或 (4) 通过执行 `break` 语句退出 switch 或循环；或 (5) 通过执行 `continue` 语句退出循环的当前迭代并开始新迭代；或 (6) 通过执行 `goto` 语句退出；或 (7) 完全不终止，例如通过 `while (true)`。

```c
public static void Statement(int choice) {
    boolean again = true;
    while (again) {
        again = false;
        if (choice == 1) // 正常终止
            Console.WriteLine("Choice 1");
        else if (choice == 2) // 抛出异常
            throw new Exception();
        else if (choice == 3) // 从方法返回
            return;
        else if (choice == 4) // 跳出循环
            break;
        else if (choice == 5) // 继续循环
            continue;
        else if (choice == 6) // 跳出循环 
            goto end;
        else // 无限循环
            while (true) {
                Console.WriteLine("At end of loop");
```
