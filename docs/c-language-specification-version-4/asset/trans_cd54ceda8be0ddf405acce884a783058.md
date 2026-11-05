
## C# 语言规范

```
from x in ( e ) .
OrderBy ( x => k1 ) .
ThenBy ( x => k2 ) .
...
ThenBy ( x => kn )
...
```

如果排序子句指定降序方向指示符，则改为生成对 OrderByDescending 或 ThenByDescending 的调用。

以下转换假设不存在 let、where、join 或 orderby 子句，并且每个查询表达式中至多有一个初始 from 子句。

示例

```
from c in customers
from o in c.Orders
select new { c.Name, o.OrderID, o.Total }
```

转换为

```
customers.
SelectMany(c => c.Orders,
(c,o) => new { c.Name, o.OrderID, o.Total }
)
```

示例

```
from c in customers
from o in c.Orders
orderby o.Total descending
select new { c.Name, o.OrderID, o.Total }
```

转换为

```
from * in customers.
SelectMany(c => c.Orders, (c,o) => new { c, o })
orderby o.Total descending
select new { c.Name, o.OrderID, o.Total }
```

其最终转换为

```
customers.
SelectMany(c => c.Orders, (c,o) => new { c, o }).
OrderByDescending(x => x.o.Total).
Select(x => new { x.c.Name, x.o.OrderID, x.o.Total })
```

其中 x 是编译器生成的标识符，除此之外不可见且不可访问。

示例

```
from o in orders
let t = o.Details.Sum(d => d.UnitPrice * d.Quantity)
where t >= 1000
select new { o.OrderID, Total = t }
```

转换为

```
from * in orders.
Select(o => new { o, t = o.Details.Sum(d => d.UnitPrice * d.Quantity) })
where t >= 1000
select new { o.OrderID, Total = t }
```

其最终转换为

```
orders.
Select(o => new { o, t = o.Details.Sum(d => d.UnitPrice * d.Quantity) }).
Where(x => x.t >= 1000).
Select(x => new { x.o.OrderID, Total = x.t })
```

其中 x 是编译器生成的标识符，除此之外不可见且不可访问。

示例

```
from c in customers
join o in orders on c.CustomerID equals o.CustomerID
select new { c.Name, o.OrderDate, o.Total }
```

转换为

```
customers.Join(orders, c => c.CustomerID, o => o.CustomerID,
(c, o) => new { c.Name, o.OrderDate, o.Total })
```

示例

```
from c in customers
join o in orders on c.CustomerID equals o.CustomerID into co
let n = co.Count()
where n >= 10
select new { c.Name, OrderCount = n }
```

转换为

```
from * in customers.
GroupJoin(orders, c => c.CustomerID, o => o.CustomerID,
(c, co) => new { c, co })
let n = co.Count()
where n >= 10
select new { c.Name, OrderCount = n }
```

其最终转换为

```
customers.
GroupJoin(orders, c => c.CustomerID, o => o.CustomerID,
(c, co) => new { c, co }).
Select(x => new { x, n = x.co.Count() }).
Where(y => y.n >= 10).
Select(y => new { y.x.c.Name, OrderCount = y.n })
```

其中 x 和 y 是编译器生成的标识符，除此之外不可见且不可访问。

示例

```
from o in orders
orderby o.Customer.Name, o.Total descending
select o
```

最终转换为

```
orders.
OrderBy(o => o.Customer.Name).
ThenByDescending(o => o.Total)
```

## 7.16.2.5 Select 子句

形式为

```
from x in e select v
```

的查询表达式转换为

```
( e ) . Select ( x => v )
```

除非 v 是标识符 x，此时转换就是

```
( e )
```

例如

```
from c in customers.Where(c => c.City == "London")
select c
```

直接转换为

```
customers.Where(c => c.City == "London")
```

## 7.16.2.6 Groupby 子句

形式为

```
from x in e group v by k
```

的查询表达式转换为

```
( e ) . GroupBy ( x => k , x => v )
```

除非 v 是标识符 x，此时转换为

```
( e ) . GroupBy ( x => k )
```

示例

```
from c in customers
group c.Name by c.Country
```

转换为

```
customers.
GroupBy(c => c.Country, c => c.Name)
```

## 7.16.2.7 透明标识符

某些转换会注入带有由 * 表示的透明标识符的范围变量。透明标识符不是正式的语言功能；它们仅作为查询表达式转换过程中的中间步骤存在。

当查询转换注入透明标识符时，后续转换步骤会将透明标识符传播到匿名函数和匿名对象初始值设定项中。在这些上下文中，透明标识符具有以下行为：

- 当透明标识符作为匿名函数中的参数出现时，关联匿名类型的成员会自动位于该匿名函数体内的作用域中。
- 当带有透明标识符的成员位于作用域中时，该成员的成员也位于作用域中。
- 当透明标识符作为匿名对象初始值设定项中的成员声明符出现时，它会引入一个带有透明标识符的成员。

在上述转换步骤中，透明标识符始终与匿名类型一起引入，目的是将多个范围变量捕获为单个对象的成员。C# 实现可以使用不同于匿名类型的机制来将多个范围变量组合在一起。

示例

```
from c in customers
from o in c.Orders
orderby o.Total descending
select new { c.Name, o.Total }
```

转换为

```
from * in customers.
    SelectMany(c => c.Orders, (c,o) => new { c, o })
    orderby o.Total descending
    select new { c.Name, o.Total }
```

其进一步转换为

```
customers.
SelectMany(c => c.Orders, (c,o) => new { c, o }).
OrderByDescending(* => o.Total).
Select(* => new { c.Name, o.Total })
```

其中，当透明标识符被擦除后，等效于

```
customers.
SelectMany(c => c.Orders, (c,o) => new { c, o }).
OrderByDescending(x => x.o.Total).
Select(x => new { x.c.Name, x.o.Total })
```

其中 x 是编译器生成的标识符，除此之外不可见且不可访问。

示例

```
from c in customers
join o in orders on c.CustomerID equals o.CustomerID
join d in details on o.OrderID equals d.OrderID
join p in products on d.ProductID equals p.ProductID
select new { c.Name, o.OrderDate, p.ProductName }
```

转换为

```
from * in customers.
    Join(orders, c => c.CustomerID, o => o.CustomerID,
        (c, o) => new { c, o })
    join d in details on o.OrderID equals d.OrderID
    join p in products on d.ProductID equals p.ProductID
    select new { c.Name, o.OrderDate, p.ProductName }
```

其进一步简化为

```
customers.
Join(orders, c => c.CustomerID, o => o.CustomerID, (c, o) => new { c, o }).
Join(details, * => o.OrderID, d => d.OrderID, (*, d) => new { *, d }).
Join(products, * => d.ProductID, p => p.ProductID, (*, p) => new { *, p }).
Select(* => new { c.Name, o.OrderDate, p.ProductName })
```

其最终转换为

```
customers.
Join(orders, c => c.CustomerID, o => o.CustomerID,
    (c, o) => new { c, o }).
Join(details, x => x.o.OrderID, d => d.OrderID,
    (x, d) => new { x, d }).
Join(products, y => y.d.ProductID, p => p.ProductID,
    (y, p) => new { y, p }).
Select(z => new { z.y.x.c.Name, z.y.x.o.OrderDate, z.p.ProductName })
```

其中 x、y 和 z 是编译器生成的标识符，除此之外不可见且不可访问。

## 7.16.3 查询表达式模式

查询表达式模式建立了一种方法模式，类型可以实现该模式以支持查询表达式。由于查询表达式通过语法映射被转换为方法调用，因此类型在如何实现查询表达式模式方面具有相当大的灵活性。例如，该模式的方法可以实现为实例方法或扩展方法，因为两者具有相同的调用语法；并且这些方法可以要求委托或表达式树，因为匿名函数可转换为两者。

下面展示了支持查询表达式模式的泛型类型 C<T> 的建议形式。使用泛型类型是为了说明参数类型和结果类型之间的正确关系，但也完全可以为非泛型类型实现该模式。

```
delegate R Func<T1,R>(T1 arg1);
delegate R Func<T1,T2,R>(T1 arg1, T2 arg2);
class C
{
    public C<T> Cast<T>();
}
class C<T> : C
{
    public C<T> Where(Func<T,bool> predicate);
    public C<U> Select<U>(Func<T,U> selector);
    public C<V> SelectMany<U,V>(Func<T,C<U>> selector,
        Func<T,U,V> resultsSelector);
    public C<U> Join<U,K,V>(C<U> inner, Func<T,K> outerKeySelector,
        Func<U,K> innerKeySelector, Func<T,U,V> resultSelector);
    public C<V> GroupJoin<U,K,V>(C<U> inner, Func<T,K> outerKeySelector,
        Func<U,K> innerKeySelector, Func<T,C<U>,V> resultSelector);
    public O<T> OrderBy<K>(Func<T,K> keySelector);
    public O<T> OrderByDescending<K>(Func<T,K> keySelector);
    public C<K,T> GroupBy<K>(Func<T,K> keySelector);
    public C<G<K,E>> GroupBy<K,E>(Func<T,K> keySelector,
        Func<T,K,E> elementSelector);
}
class O<T> : C<T>
{
    public O<T> ThenBy<K>(Func<T,K> keySelector);
    public O<T> ThenByDescending<K>(Func<T,K> keySelector);
}
class G<K,T> : C<T>
{
    public K Key { get; }
}
```

上述方法使用泛型委托类型 Func<T1, R> 和 Func<T1, T2, R>，但它们同样可以使用在参数类型和结果类型中具有相同关系的其他委托或表达式树类型。

请注意 C<T> 和 O<T> 之间的建议关系，该关系确保 ThenBy 和 ThenByDescending 方法仅可用于 OrderBy 或 OrderByDescending 的结果。另请注意 GroupBy 结果的建议形式——一个序列的序列，其中每个内部序列都有一个额外的 Key 属性。

System.Linq 命名空间为任何实现 System.Collections.Generic.IEnumerable<T> 接口的类型提供查询运算符模式的实现。

## 7.17 赋值运算符

赋值运算符将新值赋给变量、属性、事件或索引器元素。

```
assignment:
    unary-expression assignment-operator expression
```

