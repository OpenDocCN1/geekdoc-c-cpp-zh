
## 7.16 查询表达式

*查询表达式*为查询提供了一种语言集成语法，类似于 SQL 和 XQuery 等关系型和层次型查询语言。

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
query-continuation:
    into identifier query-body
```

查询表达式以 from 子句开始，以 select 或 group 子句结束。初始 from 子句之后可以跟零个或多个 from、let、where、join 或 orderby 子句。每个 from 子句都是一个生成器，引入一个范围变量，该范围变量在序列的元素上迭代。每个 let 子句引入一个范围变量，表示通过前面的范围变量计算得到的值。每个 where 子句都是一个筛选器，从结果中排除项。每个 join 子句将源序列的指定键与另一个序列的键进行比较，生成匹配对。每个 orderby 子句根据指定条件对项重新排序。最后的 select 或 group 子句根据范围变量指定结果的形状。最后，into 子句可用于“拼接”查询，方法是将一个查询的结果视为后续查询中的生成器。

### 7.16.1 查询表达式中的歧义

查询表达式包含若干“上下文关键字”，即，在给定上下文中具有特殊含义的标识符。具体而言，这些标识符是 from、where、join、on、equals、into、let、orderby、ascending、descending、select、group 和 by。为了避免因将这些标识符混合用作关键字或简单名称而导致查询表达式中的歧义，当这些标识符出现在查询表达式中的任何位置时，它们都被视为关键字。

为此，查询表达式是指以“from identifier”开头、后跟除“;”、“=”或“,”之外的任意标记的任何表达式。

为了在查询表达式内将这些词用作标识符，可以在它们前面加上“@”（§2.4.2）。

### 7.16.2 查询表达式转换

C# 语言不规定查询表达式的执行语义。相反，查询表达式会被转换为对遵循查询表达式模式（§7.16.3）的方法的调用。具体而言，查询表达式会被转换为对名为 where、Select、SelectMany、Join、GroupJoin、OrderBy、OrderByDescending、ThenBy、ThenByDescending、GroupBy 和 Cast 的方法的调用。这些方法应具有特定的签名和结果类型，如 §7.16.3 所述。这些方法可以是被查询对象的实例方法，也可以是该对象外部的扩展方法，它们实现查询的实际执行。

从查询表达式到方法调用的转换是一种语法映射，发生在执行任何类型绑定或重载决策之前。该转换保证语法正确，但不保证生成语义正确的 C# 代码。在查询表达式转换之后，生成的方法调用会作为常规方法调用进行处理，这反过来可能会发现错误，例如方法不存在、参数类型错误，或者方法是泛型方法而类型推断失败。

查询表达式通过反复应用以下转换来处理，直到无法再进行任何归约。这些转换按应用顺序列出：每一节都假定前面各节中的转换已被完全执行；一旦执行完毕，在处理同一查询表达式时，后面不会再回到该节。

查询表达式中不允许对范围变量赋值。但是，允许 C# 实现不总是强制实施此限制，因为对于此处给出的语法转换方案，有时可能无法做到这一点。

某些转换会注入带有由 * 表示的透明标识符的范围变量。透明标识符的特殊属性将在 §7.16.2.7 中进一步讨论。

### 7.16.2.1 带延续的 Select 和 groupby 子句

带延续的查询表达式

```
from ... into x ...
```

被转换为

```
from x in ( from ... ) ...
```

以下各节中的转换假定查询没有 into 延续。

示例

```
from c in customers
group c by c.Country into g
select new { Country = g.Key, CustCount = g.Count() }
```

被转换为

```
from g in
    from c in customers
    group c by c.Country
select new { Country = g.Key, CustCount = g.Count() }
```

其最终转换为

```
customers.
GroupBy(c => c.Country).
Select(g => new { Country = g.Key, CustCount = g.Count() })
```

### 7.16.2.2 显式范围变量类型

显式指定范围变量类型的 from 子句

```
from T x in e
```

被转换为

```
from x in ( e ) . Cast < T > ( )
```

显式指定范围变量类型的 join 子句

```
join T x in e on k1 equals k2
```

被转换为

```
join x in ( e ) . Cast < T > ( ) on k1 equals k2
```

以下各节中的转换假定查询没有显式范围变量类型。

示例

```
from Customer c in customers
where c.City == "London"
select c
```

被转换为

```
from c in customers.Cast<Customer>()
where c.City == "London"
select c
```

其最终转换为

```
customers.
Cast<Customer>().
where(c => c.City == "London")
```

显式范围变量类型对于查询实现非泛型 IEnumerable 接口但不实现泛型 IEnumerable<T> 接口的集合很有用。在上面的示例中，如果 customers 的类型为 ArrayList，就会出现这种情况。

### 7.16.2.3 退化查询表达式

形式为

```
from x in e select x
```

的查询表达式

被转换为

```
( e ) . Select ( x => x )
```

示例

```
from c in customers
select c
```

被转换为

```
customers.Select(c => c)
```

退化查询表达式是指简单地选择源元素的一种查询表达式。转换的后续阶段会移除由其他转换步骤引入的退化查询，方法是将其替换为它们的源。然而，重要的是确保查询表达式的结果永远不会是源对象本身，因为这会向查询客户端泄露源的类型和标识。因此，此步骤通过在源上显式调用 Select 来保护直接在源代码中编写的退化查询。然后，Select 和其他查询运算符的实现者需要确保这些方法永远不会返回源对象本身。

### 7.16.2.4 From、let、where、join 和 orderby 子句

带第二个 from 子句且后跟 select 子句的查询表达式

```
from x1 in e1
from x2 in e2
select v
```

被转换为

```
( e1 ) . SelectMany( x1 => e2 , ( x1 , x2 ) => v )
```

**带 where 子句的查询表达式**

```
from x in e
where f
...
```

被转换为

```
from x in ( e ) . Where ( x => f )
...
```

**带不带 into 的 join 子句且后跟 select 子句的查询表达式**

```
from x1 in e1
join x2 in e2 on k1 equals k2
select v
```

被转换为

```
( e1 ) . Join( e2 , x1 => k1 , x2 => k2 , ( x1 , x2 ) => v )
```

**带不带 into 的 join 子句且后跟 select 子句以外内容的查询表达式**

```
from x1 in e1
join x2 in e2 on k1 equals k2
...
```

被转换为

```
from * in ( e1 ) . Join(
    e2 , x1 => k1 , x2 => k2 , ( x1 , x2 ) => new { x1 , x2 })
...
```

**带 into 的 join 子句且后跟 select 子句的查询表达式**

```
from x1 in e1
join x2 in e2 on k1 equals k2 into g
select v
```

被转换为

```
( e1 ) . GroupJoin( e2 , x1 => k1 , x2 => k2 , ( x1 , g ) => v )
```

**带 into 的 join 子句且后跟 select 子句以外内容的查询表达式**

```
from x1 in e1
join x2 in e2 on k1 equals k2 into g
```

被转换为

```
from * in ( e1 ) . GroupJoin(
    e2 , x1 => k1 , x2 => k2 , ( x1 , g ) => new { x1 , g })
...
```

**带 orderby 子句的查询表达式**

```
from x in e
orderby k1 , k2 , ... , kn
...
```

被转换为
