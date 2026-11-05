
-   如果 F 的主体是一个块，并且 D 具有 void 返回类型，或者 F 是 async 且 D 的返回类型为 Task，则在为 F 的每个参数赋予 D 中对应参数的类型时，F 的主体是一个有效块（w.r.t §12.3），其中没有任何 return 语句指定表达式。
-   如果 F 的主体是一个表达式，并且 F 是非 async 且 D 具有非 void 返回类型 T，或者 F 是 async 且 D 的返回类型为 Task<T>，则在为 F 的每个参数赋予 D 中对应参数的类型时，F 的主体是一个有效表达式（w.r.t §11），该表达式可隐式转换为 T。
-   如果 F 的主体是一个块，并且 F 是非 async 且 D 具有非 void 返回类型 T，或者 F 是 async 且 D 的返回类型为 Task<T>，则在为 F 的每个参数赋予 D 中对应参数的类型时，F 的主体是一个有效块（w.r.t §12.3），其末端不可达，并且其中每个 return 语句指定的表达式可隐式转换为 T。

示例：以下示例说明了这些规则：

```
delegate void D(int x);
D d1 = delegate() { };                     // Ok
D d2 = delegate() { };                     // Error, signature mismatch
D d3 = delegate(long x) { };               // Error, signature mismatch
D d4 = delegate(int x) { };                // Ok
D d5 = delegate(int x) { return; };        // Ok
D d6 = delegate(int x) { return x; };      // Error, return type mismatch

delegate void E(out int x);
E e1 = delegate() { };                     // Error, E has an out parameter
E e2 = delegate(out int x) { x = 1; };     // Ok
E e3 = delegate(ref int x) { x = 1; };     // Error, signature mismatch

delegate int P(params int[] a);
P p1 = delegate() { };                     // Error, end of block reachable
P p2 = delegate { return; };               // Error, return type mismatch
P p3 = delegate { return 1; };             // Ok
P p4 = delegate { return "Hello"; };      // Error, return type mismatch
P p5 = delegate(int[] a)                   // Ok
{
    return a[0];
};
P p6 = delegate(params int[] a)            // Error, params modifier
{
    return a[0];
};
P p7 = delegate(int[] a)                   // Error, return type mismatch
{
    if (a.Length > 0) return a[0];
    return "Hello";
};

delegate object Q(params int[] a);
Q q1 = delegate(int[] a)                   // Ok
{
    if (a.Length > 0) return a[0];
    return "Hello";
};
```

示例结束

示例：以下示例使用泛型委托类型 Func<A,R>，它表示一个接受类型为 A 的参数并返回类型为 R 的值的函数：

```
delegate R Func<A,R>(A arg);
```

在以下赋值中

```
Func<int,int> f1 = x => x + 1; // Ok
Func<int,double> f2 = x => x + 1; // Ok
Func<double,int> f3 = x => x + 1; // Error
Func<int, Task<int>> f4 = async x => x + 1; // Ok
```

每个匿名函数的参数和返回类型都是从匿名函数被赋值的变量的类型中确定的。

第一个赋值成功地将匿名函数转换为委托类型 Func<int,int>，因为当 x 被赋予 int 类型时，x + 1 是一个有效表达式，可隐式转换为 int 类型。

同样，第二个赋值成功地将匿名函数转换为委托类型 Func<int,double>，因为 x + 1 的结果（类型为 int）可隐式转换为 double 类型。

然而，第三个赋值是编译时错误，因为当 x 被赋予 double 类型时，x + 1 的结果（类型为 double）不可隐式转换为 int 类型。

第四个赋值成功地将匿名 async 函数转换为委托类型 Func<int, Task<int>>，因为 x + 1 的结果（类型为 int）可隐式转换为 async lambda 的有效返回类型 int，而该 lambda 的返回类型为 Task<int>。

示例结束

lambda 表达式 F 与表达式树类型 Expression<D> 兼容的条件是 F 与委托类型 D 兼容。这不适用于匿名方法，仅适用于 lambda 表达式。

匿名函数可能会影响重载解析，并参与类型推断。有关更多详细信息，请参阅 §11.6。

## 10.7.2 匿名函数转换为委托类型的求值

将匿名函数转换为委托类型会生成一个委托实例，该实例引用匿名函数以及在求值时处于活动状态的（可能为空的）捕获外部变量集合。当委托被调用时，匿名函数的主体会被执行。主体中的代码使用委托引用的捕获外部变量集合执行。delegate_creation_expression（§11.7.15.6）可作为将匿名方法转换为委托类型的替代语法。

从匿名函数生成的委托的调用列表包含单个条目。委托的确切目标对象和目标方法未指定。特别是，委托的目标对象是 null、封闭函数成员的 this 值还是其他对象，均未指定。

将语义相同的匿名函数（具有相同的（可能为空的）捕获外部变量实例集合）转换为相同的委托类型时，允许（但不要求）返回相同的委托实例。此处语义相同是指在所有情况下，给定相同的参数，匿名函数的执行将产生相同的效果。该规则允许对如下代码进行优化。

```
delegate double Function(double x);

class Test
{
    static double[] Apply(double[] a, Function f)
    {
        double[] result = new double[a.Length];
        for (int i = 0; i < a.Length; i++)
        {
            result[i] = f(a[i]);
        }
        return result;
    }

    static void F(double[] a, double[] b)
    {
        a = Apply(a, (double x) => Math.Sin(x));
        b = Apply(b, (double y) => Math.Sin(y));
        ...
    }
}
```

由于这两个匿名函数委托具有相同的（空）捕获外部变量集合，并且由于匿名函数语义相同，因此编译器允许委托引用相同的目标方法。事实上，编译器允许从两个匿名函数表达式返回完全相同的委托实例。

## 10.7.3 lambda 表达式转换为表达式树类型的求值

将 lambda 表达式转换为表达式树类型会生成一个表达式树（§8.6）。更精确地说，lambda 表达式转换的求值会生成一个对象结构，该结构表示 lambda 表达式本身的结构。

并非每个 lambda 表达式都可以转换为表达式树类型。向兼容的委托类型的转换始终存在，但在实现特定的原因下可能在编译时失败。

注意：lambda 表达式无法转换为表达式树类型的常见原因包括：

-   它具有块主体
-   它具有 async 修饰符
-   它包含赋值运算符
-   它包含 out 或 ref 参数
-   它包含动态绑定表达式

注释结束

## 10.8 方法组转换

从方法组（§11.2）到兼容的委托类型（§19.4）存在隐式转换。如果 D 是委托类型，且 E 是被分类为方法组的表达式，则 D 与 E 兼容当且仅当 E 包含至少一个方法，该方法在其常规形式（§11.6.4.2）下适用于任何参数列表（§11.6.2），该参数列表的类型和修饰符与 D 的参数类型和修饰符匹配，如下所述。

从方法组 E 到委托类型 D 的转换的编译时应用如下所述。请注意，从 E 到 D 的隐式转换的存在并不保证转换的编译时应用能够在没有错误的情况下成功。

-   选择单个方法 M，对应于形式为 E(A) 的方法调用（§11.7.8.2），并进行以下修改：
  -   参数列表 A 是一个表达式列表，每个表达式都被分类为变量，并且具有 D 的 formal_parameter_list 中对应参数的类型和修饰符（ref 或 out）——除 dynamic 类型的参数外，对应表达式的类型为 object 而非 dynamic。
  -   考虑的候选方法仅限于在其常规形式下适用且不省略任何可选参数的方法（§11.6.4.2）。因此，如果候选方法仅在其扩展形式下适用，或者其一个或多个可选参数在 D 中没有对应参数，则会被忽略。
-   如果 §11.7.8.2 的算法产生单个最佳方法 M，且其参数数量与 D 相同，则认为转换存在。
-   即使转换存在，如果所选方法 M 与委托类型 D 不兼容（§19.4），则会发生编译时错误。
-   如果所选方法 M 是实例方法，则与 E 关联的实例表达式决定委托的目标对象。
-   如果所选方法 M 是通过实例表达式上的成员访问表示的扩展方法，则该实例表达式决定委托的目标对象。
-   转换的结果是类型为 D 的值，即引用所选方法和目标对象的委托。

*示例：* 以下演示了方法组转换：

```
delegate string D1(object o);
delegate object D2(string s);
delegate object D3();
delegate string D4(object o, params object[] a);
delegate string D5(int i);
class Test
{
    static string F(object o) {...}
    static void G()
    {
        D1 d1 = F;          // Ok
        D2 d2 = F;          // Ok
        D3 d3 = F;          // Error – not applicable
        D4 d4 = F;          // Error – not applicable in normal form
        D5 d5 = F;          // Error – applicable but not compatible
    }
}
```

对 d1 的赋值隐式地将方法组 F 转换为类型为 D1 的值。

对 d2 的赋值展示了如何创建指向具有较少派生（逆变）参数类型和更派生（协变）返回类型的方法的委托。
