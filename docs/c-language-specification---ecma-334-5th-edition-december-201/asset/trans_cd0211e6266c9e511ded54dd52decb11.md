
否则，Tx 是 U 中运算符的目标类型集合中包含范围最广的类型。如果找不到包含范围最广的类型，则转换不明确并会发生编译时错误。

- 查找最具体的转换运算符：
  - 如果 U 恰好包含一个从 Sx 转换到 Tx 的用户定义转换运算符，则此为最具体的转换运算符。
  - 否则，如果 U 恰好包含一个从 Sx 转换到 Tx 的提升转换运算符，则此为最具体的转换运算符。
  - 否则，转换不明确并会发生编译时错误。

- 最后，应用转换：
  - 如果 E 尚不具有类型 Sx，则执行从 E 到 Sx 的标准显式转换。
  - 调用最具体的用户定义转换运算符将 Sx 转换为 Tx。
  - 如果 Tx 不是 T，则执行从 Tx 到 T 的标准显式转换。

如果存在从类型 S 的变量到 T 的用户定义显式转换，则存在从类型 S 到类型 T 的用户定义显式转换。

## 11.6 涉及可空类型的转换

### 11.6.1 可空转换

可空转换允许对非可空值类型操作的预定义转换也适用于这些类型的可空形式。对于从非可空值类型 S 到非可空值类型 T 的每种预定义隐式或显式转换（§11.2.2、§11.2.3、§11.2.4、§11.2.10、§11.3.2 和 §11.3.3），存在以下可空转换：

- 从 S? 到 T? 的隐式或显式转换
- 从 S 到 T? 的隐式或显式转换
- 从 S? 到 T 的显式转换

可空转换本身被归类为隐式或显式转换。某些可空转换被归类为标准转换，并且可以在用户定义转换的一部分中出现。具体来说，所有隐式可空转换都被归类为标准隐式转换（§11.4.2），而满足 §11.4.3 要求的那些显式可空转换被归类为标准显式转换。基于从 S 到 T 的底层转换对可空转换的求值如下进行：

- 如果可空转换是从 S? 到 T?：
  - 如果源值为 null（HasValue 属性为 false），结果为类型 T? 的 null 值。
  - 否则，转换被求值为空包从 S? 到 S，随后是 S 到 T 的底层转换，随后是从 T 到 T? 的包装。
- 如果可空转换是从 S 到 T?，则转换被求值为空底层转换从 S 到 T，随后是从 T 到 T? 的包装。
- 如果可空转换是从 S? 到 T，则转换被求值为空包从 S? 到 S，随后是 S 到 T 的底层转换。

### 11.6.2 提升转换

给定一个从非可空值类型 S 到非可空值类型 T 的用户定义转换运算符，存在一个从 S? 到 T? 的提升转换运算符。此提升转换运算符执行从 S? 到 S 的解包，随后是 S 到 T 的用户定义转换，随后是从 T 到 T? 的包装，除了 null 值的 S? 直接转换为 null 值的 T?。提升转换运算符具有与其底层用户定义转换运算符相同的隐式或显式分类。

## 11.7 匿名函数转换

### 11.7.1 通用

匿名方法表达式或 lambda 表达式被归类为匿名函数（§12.16）。该表达式没有类型，但可以隐式转换为兼容的委托类型。某些 lambda 表达式也可以隐式转换为兼容的表达式树类型。

为简洁起见，本小节使用任务类型 Task 和 Task<T> 的简写形式（§15.15.1）。

具体来说，匿名函数 F 与委托类型 D 兼容，前提是：

- 如果 F 包含匿名函数签名，则 D 和 F 具有相同数量的参数。
- 如果 F 不包含匿名函数签名，则 D 可以有零个或多个任意类型的参数，只要 D 的参数没有 out 参数修饰符即可。
- 如果 F 具有显式类型的参数列表，则 D 中的每个参数与 F 中对应参数具有相同的类型和修饰符。
- 如果 F 具有隐式类型的参数列表，则 D 没有 ref 或 out 参数。
- 如果 F 的主体是一个表达式，并且 D 具有 void 返回类型或 F 为 async 且 D 具有返回类型 Task，则当 F 的每个参数被赋予 D 中对应参数的类型时，F 的主体是一个有效的表达式（关于 §12），该表达式可作为语句表达式（§13.7）被允许。
- 如果 F 的主体是一个语句块，并且 D 具有 void 返回类型或 F 为 async 且 D 具有返回类型 Task，则当 F 的每个参数被赋予 D 中对应参数的类型时，F 的主体是一个有效的语句块（关于 §13.3），其中没有 return 语句指定表达式。
- 如果 F 的主体是一个表达式，并且 F 为非 async 且 D 具有非 void 返回类型 T，或 F 为 async 且 D 具有返回类型 Task<T>，则当 F 的每个参数被赋予 D 中对应参数的类型时，F 的主体是一个有效的表达式（关于 §12），该表达式可隐式转换为 T。
- 如果 F 的主体是一个语句块，并且 F 为非 async 且 D 具有非 void 返回类型 T，或 F 为 async 且 D 具有返回类型 Task<T>，则当 F 的每个参数被赋予 D 中对应参数的类型时，F 的主体是一个有效的语句块（关于 §13.3），其末端不可达，其中每个 return 语句指定一个可隐式转换为 T 的表达式。

[示例：以下示例说明了这些规则：

```csharp
delegate void D(int x);
D d1 = delegate { }; // Ok
D d2 = delegate() { }; // Error, signature mismatch
D d3 = delegate(long x) { }; // Error, signature mismatch
D d4 = delegate(int x) { }; // Ok
D d5 = delegate(int x) { return; }; // Ok
D d6 = delegate(int x) { return x; }; // Error, return type mismatch
delegate void E(out int x);
E e1 = delegate { }; // Error, E has an out parameter
E e2 = delegate(out int x) { x = 1; }; // Ok
E e3 = delegate(ref int x) { x = 1; }; // Error, signature mismatch
delegate int P(params int[] a);
P p1 = delegate { }; // Error, end of block reachable
P p2 = delegate { return; }; // Error, return type mismatch
P p3 = delegate { return 1; }; // Ok
P p4 = delegate { return "Hello"; }; // Error, return type mismatch
P p5 = delegate(int[] a) { return a[0]; }; // Ok
P p6 = delegate(params int[] a) { return a[0]; }; // Error, params modifier
P p7 = delegate(int[] a) { if (a.Length > 0) return a[0]; return "Hello"; }; // Error, return type mismatch
delegate object Q(params int[] a);
Q q1 = delegate(int[] a) { if (a.Length > 0) return a[0]; return "Hello"; }; // Ok
```

示例结束

[示例：以下示例使用通用委托类型 Func<A,R>，它表示一个接受类型 A 的参数并返回类型 R 的值 的函数：

```csharp
delegate R Func<A,R>(A arg);
```

在赋值中

```csharp
Func<int,int> f1 = x => x + 1; // Ok
Func<int,double> f2 = x => x + 1; // Ok
Func<double,int> f3 = x => x + 1; // Error
Func<int, Task<int>> f4 = async x => x + 1; // Ok
```

每个匿名函数的参数和返回类型都是从匿名函数被赋值的变量的类型确定的。第一个赋值成功地将匿名函数转换为委托类型 Func<int,int>，因为当 x 被赋予类型 int 时，x + 1 是一个有效表达式，可隐式转换为类型 int。同样，第二个赋值成功地将匿名函数转换为委托类型 Func<int,double>，因为 x + 1 的结果（类型为 int）可隐式转换为类型 double。然而，第三个赋值是编译时错误，因为当 x 被赋予类型 double 时，x + 1 的结果（类型为 double）不可隐式转换为类型 int。第四个赋值成功地将匿名 async 函数转换为委托类型 Func<int, Task<int>>，因为 x + 1 的结果（类型为 int）可隐式转换为 async lambda 的有效返回类型 int，而该 lambda 的返回类型为 Task<int>。示例结束

lambda 表达式 F 与表达式树类型 Expression<D> 兼容，如果 F 与委托类型 D 兼容。这不适用于匿名方法，仅适用于 lambda 表达式。

某些 lambda 表达式不能转换为表达式树类型：即使转换存在，它也会在编译时失败。如果 lambda 表达式满足以下情况，则会出现这种情况：

- 具有块主体
- 包含简单或复合赋值运算符
- 包含动态绑定表达式
- 为 async

