

# 示例 109 匿名方法的兼容性

匿名方法 d11 兼容 D1 但不兼容 D2；匿名方法 d21 兼容 D2 但不兼容 D1；而 d22 兼容 D2 和 D3 但不兼容 D1。这些匿名方法均都不兼容 D4。foreach 循环调用了匿名方法；对 d21 的每次调用以及由 M(4) 创建的匿名方法的调用都会使 ref 参数 y 增加 1。

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

局部变量 u 和 v 被捕获在循环体内的匿名方法中。由于 u 在 for 循环外部声明，因此只会创建一个变量实例，且 udlg 中的所有匿名方法都引用该实例。由于 v 是在内部声明的，循环的每次迭代都会创建一个变量的独立实例，且 vdlg 中的每个匿名方法都有自己的实例。因此，单个的 u 被增加了五次，而每个 v 被增加了一次。

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

92 表达式

# 12.23 Lambda 表达式 (C# 3.0)

Lambda 表达式类似于匿名方法表达式（第 12.22 节），但语法更紧凑。它的基本形式为：

```
x => e

(xt, ..., xn) => e

(parameter-modifier t1 x1, ..., parameter-modifier tn xn) => e
```

x 和 xi 是参数，表达式是 Lambda 表达式的体，ti 是参数类型，而 parameter-modifier 是 ref 或 out。Lambda 表达式不能接受参数数组（params；见第 10.7 节）或可选参数（第 10.10 节）。根据匿名方法的规则（第 12.22 节），e 可以引用封闭作用域内的变量和参数。

Lambda x => e 的值是一个委托对象，当应用于参数 x 时，它将评估表达式并返回结果。类似于匿名方法，Lambda 表达式本身没有类型，但可以转换为与参数类型以及 e 的类型（返回类型）一致的委托类型。当 Lambda 表达式的参数类型未指定时，编译器会尝试使用上下文信息来推断它们，例如 Lambda 表达式所赋值的变量或方法的类型（示例 111）。

# 12.24 匿名对象表达式 (C# 3.0)

匿名对象求值为一个具有只读字段的对象：

```
new { xi = ei, ..., xn = en }
```

xi 是标识符，ei 是从左到右求值的表达式，用于获取 xi 的值。当 ei 是标识符 x 或字段或属性访问 e.f 时，可以省略 xi=，在这种情况下，标识符 x 或标识符 f 将被用于 xi。

生成的匿名对象具有只读属性，返回创建时给的值。表达式的类型是匿名类型。在同一个程序集内（第 1.1 节），所有具有相同字段且顺序相同的匿名表达式都具有相同的匿名类型。匿名对象的 Equals 和 GetCode 方法已根据其内部的字段值进行了重写。ToString 方法显示对象的字段值。匿名对象表达式用于 LINQ 查询的实现（示例 242）。

# 12.25 隐式类型数组创建表达式 (C# 3.0)

一维数组的隐式类型数组创建的格式如下：

```
new [] { xi = ei, ..., xn = en }
```

与普通数组创建（第 9 节）的区别在于，隐式类型格式没有指定新创建数组的类型；这对于一个用匿名对象表达式初始化的数组来说是不可能的。前面的表达式创建了一个长度为 n 的数组，其元素类型是所有 ei 类型中的最佳类型。ei 从左到右求值。矩形多维数组 `new[] { { ... }, ..., { ... } }` 如第 9.2 节所示创建。

# 示例 111 Lambda 表达式

Lambda 表达式如 (s => s.Length==3) 是一个谓词，用于测试 (String) 参数长度是否为 3。典型用法是过滤掉可枚举中具有特定属性的项。示例 f1 和 f2 显示同一个表达式可以用于不同的类型。由于 Lambda 表达式本身没有类型（当指定参数时），它不能赋值给类型不是 Object 或 dynamic 的 var 声明变量。

变量 f3 和 f4 显示了相同的加 x 和 y 的函数，但 f1 同时接收两个参数，而 f2 返回一个接受 x 和 y 然后返回 x+y 的函数。该函数是。

# 示例 112 匿名对象

匿名对象求值为一个具有只读字段的对象：

```csharp
new { xi = ei, ..., xn = en }
```

# 示例 113 隐式类型数组

一维数组的隐式类型数组创建的格式如下：

```
new [] { xi = ei, ..., xn = en }
```

