
```
```
}
```
```

在此示例中，匿名函数捕获了一个局部变量：

```csharp
class Test
{
    void F()
    {
        int y = 123;
        D d = () => Console.WriteLine(y);
    }
}
```

局部变量的生命周期现在必须至少延长到匿名函数委托的生命周期。这可以通过将局部变量“提升”到编译器生成的类的字段中来实现。局部变量的实例化（§11.16.6.3）随后对应于创建编译器生成的类的实例，而访问局部变量则对应于访问编译器生成类实例中的字段。此外，匿名函数成为编译器生成类的实例方法：

```csharp
class Test
{
    void F()
    {
        __Locals1 __locals1 = new __Locals1();
        __locals1.y = 123;
        D d = new D(__locals1.__Method1);
    }

    class __Locals1
    {
        public int y;

        public void __Method1()
        {
            Console.WriteLine(y);
        }
    }
}
```

最后，下面的匿名函数捕获了 this 以及两个具有不同生命周期的局部变量：

```csharp
class Test
{
    int x;

    void F()
    {
        int y = 123;
        for (int i = 0; i < 10; i++)
        {
            int z = i * 2;
            D d = () => Console.WriteLine(x + y + z);
        }
    }
}
```

在此，为捕获了局部变量的每个块创建了一个编译器生成的类，以便不同块中的局部变量可以具有独立的生命周期。内层块的编译器生成类 __locals2 的一个实例包含局部变量 z 以及一个引用 __locals1 实例的字段。外层块的编译器生成类 __locals1 的一个实例包含局部变量 y 以及一个引用包含函数成员的 this 的字段。借助这些数据结构，可以通过 __locals2 的一个实例访问所有被捕获的外层变量，因此匿名函数的代码可以作为该类的实例方法实现。

class Test
{
    void F()
    {
        __locals1 __locals1 = new __locals1();
        __locals1.__this = this;
        __locals1.y = 123;
        for (int i = 0; i < 10; i++)
        {
            __locals2 __locals2 = new __locals2();
            __locals2.__locals1 = __locals1;
            __locals2.z = i * 2;
            D d = new D(__locals2.__Method1);
        }
    }
    class __locals1
    {
        public Test __this;
        public int y;
    }
    class __locals2
    {
        public __locals1 __locals1;
        public int z;
        public void __Method1()
        {
            Console.WriteLine(__locals1.__this.x + __locals1.y + z);
        }
    }
}
```

此处用于捕获局部变量的相同技术也可以在将匿名函数转换为表达式树时使用：可以将在表达式树中存储对编译器生成对象的引用，并且对局部变量的访问可以表示为对这些对象的字段访问。这种方法的优点在于它允许“提升”的局部变量在委托和表达式树之间共享。

信息性文本结束。

## 11.17 查询表达式

### 11.17.1 通用

*查询表达式*提供了一种语言集成的查询语法，其类似于 SQL 和 XQuery 等关系和分层查询语言。

query_expression
  : from_clause query_body
  ;

from_clause
  : 'from' type? identifier 'in' expression
  ;

query_body
  : query_body_clauses? select_or_group_clause query_continuation?
  ;

query_body_clauses
  : query_body_clause
  | query_body_clauses query_body_clause
  ;

query_body_clause
  : from_clause
  | let_clause
  | where_clause
  | join_clause
  | join_into_clause
  | orderby_clause
  ;

let_clause
  : 'let' identifier '=' expression
  ;

where_clause
  : 'where' boolean_expression
  ;

join_clause
  : 'join' type? identifier 'in' expression 'on' expression 'equals' expression
  ;

join_into_clause
  : 'join' type? identifier 'in' expression 'on' expression 'equals' expression
  'into' identifier
  ;

orderby_clause
  : 'orderby' orderings
  ;

orderings
: ordering (',' ordering)*
;
ordering
    : expression ordering_direction?
    ;
ordering_direction
    : 'ascending'
    | 'descending'
    ;
select_or_group_clause
    : select_clause
    | group_clause
    ;
select_clause
    : 'select' expression
    ;
group_clause
    : 'group' expression 'by' expression
    ;
query_continuation
    : 'into' identifier query_body
    ;

查询表达式以 from 子句开始，以 select 或 group 子句结束。初始的 from 子句后面可以跟零个或多个 from、let、where、join 或 orderby 子句。每个 from 子句都是一个生成器，引入一个范围变量，该变量遍历序列的元素。每个 let 子句引入一个范围变量，表示通过先前的范围变量计算得到的值。每个 where 子句都是一个过滤器，用于从结果中排除项目。每个 join 子句将源序列的指定键与另一个序列的键进行比较，生成匹配的对。每个 orderby 子句根据指定的条件重新排序项目。最终的 select 或 group 子句根据范围变量指定结果的形状。最后，可以使用 into 子句通过将一个查询的结果作为后续查询中的生成器来“拼接”查询。

### 11.17.2 查询表达式中的歧义

查询表达式使用了一些上下文关键字（§6.4.4）：ascending, by, descending, equals, from, group, into, join, let, on, orderby, select and where。

为了避免因这些标识符既用作关键字又用作简单名称而可能产生的歧义，这些标识符在查询表达式内的任何位置都被视为关键字，除非它们以“@”为前缀（§6.4.4），在这种情况下它们被视为标识符。为此目的，查询表达式是任何以“from identifier”开头，后跟除“；”、“=”或“，”之外的任何标记的表达式。

### 11.17.3 查询表达式转换

#### 11.17.3.1 通用

C# 语言未指定查询表达式的执行语义。相反，查询表达式被转换为遵循查询表达式模式（§11.17.4）的方法的调用。具体来说，查询表达式被转换为名为 Where、Select、SelectMany、Join、GroupJoin、OrderBy、OrderByDescending、ThenBy、ThenByDescending、GroupBy 和 Cast 的方法的调用。这些方法预计具有特定的签名和返回类型，如 §11.17.4 中所述。这些方法可以是被查询对象的实例方法，也可以是对象外部的扩展方法。这些方法实现了查询的实际执行。

从查询表达式到方法调用的转换是在进行任何类型绑定或重载解析之前发生的语法映射。在转换查询表达式之后， resulting 方法调用作为常规方法调用进行处理，这反过来可能会发现编译时错误。这些错误条件包括但不限于不存在的方法、类型错误的参数以及类型推断失败的泛型方法。

查询表达式通过反复应用以下转换进行处理，直到无法再进行进一步简化为止。转换按应用顺序列出：每个部分假设前一节中的转换已彻底执行，并且一旦耗尽，在同一查询表达式的处理中不会再次 revisiting 该部分。

如果查询表达式包含对范围变量的赋值，或将范围变量用作 ref 或 out 参数的参数，则为编译时错误。

某些转换会注入用 * 表示的透明标识符的范围变量。这些在 §11.17.3.8 中进一步描述。

#### 11.17.3.2 带有延续的 select 和 group ... by 子句

使用 y 的属性 Prop 的 group 子句的查询表达式，其查询体 Q 包含如下形式的延续：

```
from «y» in S group «y» by «y».Prop into «x» Q
```

被转换为：

```
from «x» in ( from «y» in S group «y» by «y».Prop ) Q
```

以下各节中的转换假设查询没有 into 延续。

示例：示例：

```
from c in customers
group c by c.Country into g
select new { Country = g.Key, CustCount = g.Count() }
```

被转换为：

```
from g in
    (from c in customers
     group c by c.Country)
select new { Country = g.Key, CustCount = g.Count() }
```

其最终转换是：

```
customers.
GroupBy(c => c.Country).
Select(g => new { Country = g.Key, CustCount = g.Count() })
```

示例结束

#### 11.17.3.3 显式范围变量类型

显式指定范围变量类型的 from 子句

```
from «T» «x» in «e»
```
