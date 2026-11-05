
```
static D[] F() {
    D[] result = new D[3];
    for (int i = 0; i < 3; i++) {
        result[i] = () => { Console.WriteLine(i); };
    }
    return result;
}
```

只捕获了迭代变量的一个实例，这会产生以下输出：

3
3
3

> ERIC LIPPERT 这种行为——匿名函数捕获的是循环变量，而不是该变量的当前值——是我们收到的“我认为我在编译器中发现了一个 bug”这类错误报告中最常见的原因。对于本规范的未来版本，我们正在考虑将 foreach 循环变量的形式定义移至循环内部，这样循环内的匿名函数每次循环都会捕获一个新的变量。这在技术上会是一个破坏性变更，但它会使语言与大多数人认为其行为应该一致的情况保持一致。很难想象有一种情况，你希望将循环变量作为变量捕获，而不是作为值捕获。

匿名函数委托可以共享某些捕获的变量，同时对其他变量有各自的实例。例如，如果将 F 改为

```
D[] result = new D[3];
int x = 0;
for (int i = 0; i < 3; i++) {
    int y = 0;
    result[i] = () => { Console.WriteLine("{0} {1}", ++x, ++y); };
}
return result;
```

这三个委托捕获的是 x 的同一个实例，但 y 的各自实例，并且输出为

1 1
2 1
3 1

单独的匿名函数可以捕获外部变量的同一个实例。在下面的示例中

```
using System;
delegate void Setter(int value);
delegate int Getter();
class Test
{
    static void Main() {
        int x = 0;
        Setter s = (int value) => { x = value; };
        Getter g = () => { return x; };
        s(5);
        Console.WriteLine(g());
        s(10);
        Console.WriteLine(g());
    }
}
```

这两个匿名函数捕获了局部变量 x 的同一个实例，并且可以通过该变量进行“通信”。示例的输出为

5
10

## 7.15.6 匿名函数表达式的求值

匿名函数 F 必须始终转换为委托类型 D 或表达式树类型 E，要么直接转换，要么通过执行委托创建表达式 new D(F)。此转换决定了匿名函数的结果，如 §6.5 中所述。

## 7.16 查询表达式

查询表达式提供了一种语言集成的查询语法，其类似于 SQL 和 XQuery 等关系型和层次型查询语言。

```
query-expression:
    from-clause query-body

from-clause:
    from type_opt identifier in expression

query-body:
    query-body-clauses_opt select-or-group-clause query-continuation_opt

query-body-clauses:
    query-body-clause
    query-body-clauses query-body-clause
```

```
query-body-clause:
  from-clause
  let-clause
  where-clause
  join-clause
  join-into-clause
  orderby-clause

let-clause:
  let identifier = expression

where-clause:
  where boolean-expression

join-clause:
  join type_opt identifier in expression on expression equals expression

join-into-clause:
  join type_opt identifier in expression on expression equals expression into identifier

orderby-clause:
  orderby orderings

orderings:
  ordering
  orderings , ordering

ordering:
  expression ordering-direction_opt

ordering-direction:
  ascending
  descending

select-or-group-clause:
  select-clause
  group-clause

select-clause:
  select expression
```

```
group-clause:
    group expression by expression
```

```
query-continuation:
    into identifier query-body
```

查询表达式以 from 子句开始，以 select 或 group 子句结束。初始的 from 子句可以跟随零个或多个 from、let、where、join 或 orderby 子句。每个 from 子句都是一个生成器，引入一个范围变量，该变量遍历序列的元素。每个 let 子句引入一个范围变量，表示通过先前的范围变量计算得到的值。每个 where 子句都是一个过滤器，排除结果中的项。每个 join 子句将源序列的指定键与另一个序列的键进行比较，产生匹配的对。每个 orderby 子句根据指定的标准重新排序项。最后的 select 或 group 子句根据范围变量指定结果的形状。最后，可以使用 into 子句来“拼接”查询，将一个查询的结果作为后续查询中的生成器来处理。

> > **ERIC LIPPERT** 为什么 C# 中的查询语法是 "from...where...select"，而不是 SQL 开发者更熟悉的顺序："select...from...where"？虽然 SQL 的顺序对 SQL 开发者来说很熟悉，对英语使用者也很自然，但它给语言和 IDE 设计者带来了许多问题，而这些问题在 C# 的顺序中并不存在。
> >
> > 首先，由于作用域规则，使用 SQL 顺序的 IntelliSense 很困难。想象你在为“select 优先”语法设计 IDE。用户刚刚输入了 "select"。接下来呢？你不知道用户是从哪个数据源进行投影，因此无法提供合理的帮助选项列表。同样也无法为 "where" 提供任何帮助。在 C# 系统中，"from" 在 "select" 之前；因此，当用户输入 "where" 或 "select" 时，IDE 已知道数据源的类型信息。
> >
> > 其次，C# 的顺序是代码实际执行操作的顺序：首先确定一个集合，然后对集合运行过滤器，然后对过滤器的结果进行投影。此顺序有助于让人了解数据如何在系统中流动。

> > **CHRIS SELLS** 现在我见过 SQL 中的 "select-from" 顺序和 LINQ 中的 "from-select" 顺序后，LINQ 对我来说更有意义了，我很沮丧 SQL 不允许 "from-select" 风格。

### 7.16.1 查询表达式中的歧义

查询表达式包含许多“上下文关键字”——即在给定上下文中具有特殊含义的标识符。具体来说，这些是 from、where、join、on、equals、into、let、orderby、ascending、descending、select、group 和 by。为了避免因这些标识符作为关键字或简单名称的混合使用而在查询表达式中产生的歧义，这些标识符在查询表达式内的任何位置出现时都被视为关键字。

为此目的，查询表达式是任何以“from identifier”开头，后跟除“;”、“}”或“,”之外的任何标记的表达式。

要在查询表达式中使用这些词作为标识符，可以在前面加上“@”（§2.4.2）。

### 7.16.2 查询表达式翻译

C# 语言并未指定查询表达式的执行语义。相反，查询表达式被翻译成遵循查询表达式模式（§7.16.3）的方法的调用。具体来说，查询表达式被翻译成名为 where、Select、SelectMany、Join、GroupJoin、OrderBy、OrderByDescending、ThenBy、ThenByDescending、GroupBy 和 Cast 的方法的调用。这些方法预计具有特定的签名和结果类型，如 §7.16.3 中所述。这些方法可以是被查询对象的实例方法，也可以是对象外部的扩展方法，并且它们实现了查询的实际执行。

从查询表达式到方法调用的翻译是在进行任何类型绑定或重载解析之前发生的语法映射。翻译保证在语法上是正确的，但不保证产生语义上正确的 C# 代码。在查询表达式翻译之后，得到的方法调用作为常规方法调用进行处理，这可能会进一步发现错误——例如，如果方法不存在，如果参数类型错误，或者如果方法为泛型且类型推断失败。

> **BILL WAGNER** 本节是理解查询表达式如何被翻译成方法调用以及可能的扩展方法调用的绝佳方式。

> **JON SKEET** 查询表达式能够以如此小的规范增量引入到 C# 中，对我来说是令人惊叹的。相比之下，像泛型这样的一些特性影响了语言的几乎每个方面，而查询表达式却出奇地自成一体——尤其是考虑到它们提供的表达能力。
