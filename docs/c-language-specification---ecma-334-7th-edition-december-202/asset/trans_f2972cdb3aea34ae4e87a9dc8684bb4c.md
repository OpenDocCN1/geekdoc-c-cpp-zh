
其最终翻译为：

```
customers.
GroupBy(c => c.Country).
Select(g => new { Country = g.Key, CustCount = g.Count() })
```

示例结束

## 12.20.3.3 显式范围变量类型

一个显式指定范围变量类型的 from 子句

```
from «T» «x» in «e»
```

翻译为

```
from «x» in ( «e» ) . Cast < «T» > ( )
```

一个显式指定范围变量类型的 join 子句

```
join «T» «x» in «e» on «k1» equals «k2»
```

翻译为

```
join «x» in ( «e» ) . Cast < «T» > ( ) on «k1» equals «k2»
```

以下各节中的翻译假定查询没有显式范围变量类型。

示例：示例

```
from Customer c in customers
where c.City == "London"
select c
```

翻译为

```
from c in (customers).Cast<Customer>()
where c.City == "London"
select c
```

其最终翻译为

```
customers.
Cast<Customer>().
Where(c => c.City == "London")
```

示例结束

注意：显式范围变量类型对于查询实现非泛型 IEnumerable 接口但未实现泛型 IEnumerable<T> 接口的集合很有用。在上面的示例中，如果 customers 的类型为 ArrayList，就会是这种情况。 注意结束

## 12.20.3.4 退化查询表达式

形式为的查询表达式

```
from «x» in «e» select «x»
```

翻译为

```
( «e» ) . Select ( «x» => «x» )
```

示例：示例

```
from c in customers
select c
```

翻译为

```
(customers).Select(c => c)
```

示例结束

退化查询表达式是指对源元素进行平凡选择的表达式。

> 注意：翻译的后期阶段（§12.20.3.6 和 §12.20.3.7）通过将其替换为其源来删除由其他翻译步骤引入的退化查询。然而，重要的是要确保查询表达式的结果永远不是源对象本身。否则，返回此类查询的结果可能会无意中向调用方公开私有数据（例如元素数组）。因此，此步骤通过显式地在源上调用 Select 来保护直接在源代码中编写的退化查询。然后，Select 和其他查询运算符的实现者有责任确保这些方法永远不会返回源对象本身。 注意结束

## 12.20.3.5 From、let、where、join 和 orderby 子句

带有第二个 from 子句后跟 select 子句的查询表达式

```
from «x1» in «e1»
from «x2» in «e2»
select «v»
```

翻译为

```
( «e1» ) . SelectMany( «x1» => «e2» , ( «x1» , «x2» ) => «v» )
```

示例：示例

```
from c in customers
from o in c.Orders
select new { c.Name, o.OrderID, o.Total }
```

翻译为

```
(customers).
SelectMany(c => c.Orders,
(c,o) => new { c.Name, o.OrderID, o.Total }
)
```

示例结束

带有第二个 from 子句后跟包含非空查询主体子句集的查询主体 Q 的查询表达式：

```
from «x1» in «e1»
from «x2» in «e2»
Q
```

翻译为

```
from * in («e1») . SelectMany( «x1» => «e2» , ( «x1» , «x2» ) => new { «x1» , «x2» } )
Q
```

示例：示例

```
from c in customers
from o in c.Orders
orderby o.Total descending
select new { c.Name, o.OrderID, o.Total }
```

翻译为

```
from * in (customers).
    SelectMany(c => c.Orders, (c,o) => new { c, o })
    orderby o.Total descending
    select new { c.Name, o.OrderID, o.Total }
```

其最终翻译为

```
customers.
SelectMany(c => c.Orders, (c,o) => new { c, o }).
OrderByDescending(x => x.o.Total).
Select(x => new { x.c.Name, x.o.OrderID, x.o.Total })
```

其中 x 是一个编译器生成的标识符，否则不可见且无法访问。

示例结束

一个 let 表达式连同其前面的 from 子句：

```
from «x» in «e»
let «y» = «f»
...
```

翻译为

```
from * in ( «e» ) . Select ( «x» => new { «x» , «y» = «f» } )
...
```

示例：示例

```
from o in orders
let t = o.Details.Sum(d => d.UnitPrice * d.Quantity)
where t >= 1000
select new { o.OrderID, Total = t }
```

翻译为

```
from * in (orders).Select(
    o => new { o, t = o.Details.Sum(d => d.UnitPrice * d.Quantity) })
where t >= 1000
select new { o.OrderID, Total = t }
```

其最终翻译为

```
orders
.Select(o => new { o, t = o.Details.Sum(d => d.UnitPrice * d.Quantity) })
.Where(x => x.t >= 1000)
.Select(x => new { x.o.OrderID, Total = x.t })
```

其中 x 是一个编译器生成的标识符，否则不可见且无法访问。

示例结束

一个 where 表达式连同其前面的 from 子句：

```
from «x» in «e»
where «f»
...
```

翻译为

```
from «x» in ( «e» ) . Where ( «x» => «f» )
...
```

```
    from c in customers
    join o in orders on c.CustomerID equals o.CustomerID into co
    let n = co.Count()
    where n >= 10
    select new { c.Name, OrderCount = n }
```

翻译为

```
    from * in (customers).GroupJoin(
        orders,
        c => c.CustomerID,
        o => o.CustomerID,
        (c, co) => new { c, co })
    let n = co.Count()
    where n >= 10
    select new { c.Name, OrderCount = n }
```

其最终翻译为

```
    customers
        .GroupJoin(
            orders,
            c => c.CustomerID,
            o => o.CustomerID,
            (c, co) => new { c, co })
        .Select(x => new { x, n = x.co.Count() })
        .Where(y => y.n >= 10)
        .Select(y => new { y.x.c.Name, OrderCount = y.n })
```

其中 x 和 y 是编译器生成的标识符，否则不可见且无法访问。

*示例结束*

一个 orderby 子句及其前面的 from 子句：

```
    from «x» in «e»
    orderby «k1» , «k2» , ... , «kn»
    ...
```

翻译为

```
    from «x» in ( «e» ) .
        OrderBy ( «x» => «k1» ) .
        ThenBy ( «x» => «k2» ) .
        ...
        ThenBy ( «x» => «kn» )
        ...
```

如果排序子句指定了降序方向指示符，则会生成 OrderByDescending 或 ThenByDescending 的调用。

*示例：示例*

```
    from o in orders
    orderby o.Customer.Name, o.Total descending
    select o
```

的最终翻译为

```
(orders)
.OrderBy(o => o.Customer.Name)
.ThenByDescending(o => o.Total)
end example
```

示例结束

以下翻译假定没有 let、where、join 或 orderby 子句，并且每个查询表达式中最多只有一个初始 from 子句。

## 12.20.3.6 Select 子句

形式为的查询表达式

```
from «x» in «e» select «v»
```

翻译为

```
( «e» ) . Select ( «x» => «v» )
```

除非 «v» 是标识符 «x»，翻译仅为

```
( «e» )
```

示例：示例

```
from c in customers.Where(c => c.City == "London")
select c
```

仅翻译为

```
(customers).Where(c => c.City == "London")
```

示例结束

## 12.20.3.7 Group 子句

一个 group 子句

```
from «x» in «e» group «v» by «k»
```

翻译为

```
( «e» ) . GroupBy ( «x» => «k» , «x» => «v» )
```

除非 «v» 是标识符 «x»，翻译为

```
( «e» ) . GroupBy ( «x» => «k» )
```

示例：示例

```
from c in customers
group c.Name by c.Country
```

翻译为

```
(customers).GroupBy(c => c.Country, c => c.Name)
```

## 12.20.3.8 透明标识符

某些翻译会注入用 * 表示的透明标识符的范围变量。透明标识符仅作为查询表达式翻译过程中的中间步骤存在。

当查询翻译注入透明标识符时，后续的翻译步骤会将透明标识符传播到匿名函数和匿名对象初始化器中。在这些上下文中，透明标识符具有以下行为：

- 当透明标识符作为匿名函数的参数出现时，与之关联的匿名类型的成员会在匿名函数体中自动进入作用域。
- 当具有透明标识符的成员在作用域内时，该成员的成员也在作用域内。
- 当透明标识符作为匿名对象初始化器中的成员声明符出现时，它会引入一个具有透明标识符的成员。

在上述描述的翻译步骤中，透明标识符始终与匿名类型一起引入，其目的是将多个范围变量作为单个对象的成员捕获。C# 的实现可以使用不同于匿名类型的机制来组合多个范围变量。以下翻译示例假定使用匿名类型，并展示了透明标识符的一种可能翻译。

示例：示例

```
```
from c in customers
from o in c.Orders
orderby o.Total descending
select new { c.Name, o.Total }
```
```

翻译为

```
```
from * in (customers).SelectMany(c => c.Orders, (c,o) => new { c, o })
orderby o.Total descending
select new { c.Name, o.Total }
```
```

进一步翻译为

```
```
customers
    .SelectMany(c => c.Orders, (c,o) => new { c, o })
    .OrderByDescending(* => o.Total)
    .Select(* => new { c.Name, o.Total })
```
```

当透明标识符被擦除时，等价于

```
```
customers
    .SelectMany(c => c.Orders, (c,o) => new { c, o })
    .OrderByDescending(x => x.o.Total)
    .Select(x => new { x.c.Name, x.o.Total })
```
```

其中 x 是一个编译器生成的标识符，否则不可见且无法访问。

示例

```
```
from c in customers
join o in orders on c.CustomerID equals o.CustomerID
join d in details on o.OrderID equals d.OrderID
join p in products on d.ProductID equals p.ProductID
select new { c.Name, o.OrderDate, p.ProductName }
```
```

翻译为

```
```
from * in (customers).Join(
    orders,
    c => c.CustomerID,
```
