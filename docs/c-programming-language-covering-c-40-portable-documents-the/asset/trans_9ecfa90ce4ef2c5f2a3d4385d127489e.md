
查询表达式是通过反复应用以下转换进行处理的，直到无法再进行进一步的简化为止。转换按应用顺序列出：每个部分都假设前一节中的转换已彻底执行；一旦耗尽，该部分在同一查询表达式的处理中将不会被再次访问。

赋值给范围变量在查询表达式中是不允许的。然而，C# 实现被允许并不总是强制执行此限制，因为使用本文介绍的语法转换方案有时可能无法实现。

某些转换会注入用 * 表示的透明标识符的范围变量。透明标识符的特殊属性在 §7.16.2.7 中进一步讨论。

> > **CHRIS SELLS** 尽管我很喜欢 C# 3.0 查询语法，有时很难记住这些转换。如果偶尔觉得需要使用方法调用语法来写出查询，请不要感到不好意思。此外，你自己实现的任何查询方法都不会有语言结构，因此有时你别无选择，只能使用方法调用语法。
> >
> > 此外，如果你的同事写查询像这样，完全没问题：
> >
> > ```
> > var duluthians = from c in Customers
> >                   where c.City == "Duluth" select c;
> > ```
> >
> > 而你写查询像这样：
> >
> > ```
> > var duluthians = Customers.Where(c => c.City == "Duluth");
> > ```
> >
> > 第二种语法不需要心理转换，并且适用于所有扩展方法，而不仅仅是被翻译成关键字的那些。例如：
> >
> > ```
> > var tenDuluthites = Customers.Where(c => c.City == "Duluth").Take(10);
> > ```
> >
> > 与之相比
> >
> > ```
> > var tenDuluthites = (from c in Customers where c.City ==
> >                     "Duluth" select c).Take(10);
> > ```
> >
> > 我是个简单的人，所以我更喜欢总是有效的语法风格，而不是现在酷孩子们正在做的。

> JON SKEET 虽然不太可能在查询表达式中支持 IEnumerable<T> 上的额外查询方法，但其定义中涉及的中立性是其美妙之处之一：规范中没有任何内容规定类型应该是什么。这使得其他框架（如 Reactive Extensions 和 Parallel Extensions）能够针对新类型编写查询方法，同时仍然利用查询表达式语法。

## 7.16.2.1 select 和 GroupBy 子句中的延续

带有一个延续的查询表达式

```
from ... into x ...
```

被翻译成

```
from x in ( from ... ) ...
```

以下各节中的转换假设查询中没有 into 延续。

示例

```
from c in customers
group c by c.Country into g
select new { Country = g.Key, CustCount = g.Count() }
```

被翻译成

```
from g in
    from c in customers
    group c by c.Country into g
    select new { Country = g.Key, CustCount = g.Count() }
```

其最终转换是

```
customers.
GroupBy(c => c.Country).
Select(g => new { Country = g.Key, CustCount = g.Count() })
```

> JOSEPH ALBAHARI 查询延续的目的是允许在 select 或 group 子句之后继续使用其他子句（否则查询会终止）。在查询延续之后，前一个范围变量以及通过 join 或 let 子句引入的任何变量都超出作用域。相比之下，let 子句的行为类似于非破坏性 select：它保留前一个范围变量和其他查询变量的作用域。查询延续引入的标识符可以与前一个范围变量相同。

## 7.16.2.2 显式范围变量类型

显式指定范围变量类型的 from 子句

```
from T x in e
```

被翻译成

```
from x in ( e ) . Cast < T > ( )
```

显式指定范围变量类型的 join 子句

```
join T x in e on k₁ equals k₂
```

被翻译成

```
join x in ( e ) . Cast < T > ( ) on k₁ equals k₂
```

以下各节中的转换假设查询中没有显式的范围变量类型。

示例

```
from Customer c in customers
where c.City == "London"
select c
```

被翻译成

```
from c in customers.Cast<Customer>()
where c.City == "London"
select c
```

其最终转换是

```
customers.
Cast<Customer>().
Where(c => c.City == "London")
```

显式范围变量类型对于查询实现非泛型 IEnumerable 接口但未实现泛型 IEnumerable<T> 接口的集合非常有用。在上面的示例中，如果 customers 的类型为 ArrayList，则会是这种情况。

## 7.16.2.3 退化查询表达式

形式为的查询表达式

```
from x in e select x
```

被翻译成

```
( e ) . Select ( x => x )
```

示例

```
from c in customers
select c
```

被翻译成

```
customers.Select(c => c)
```

退化查询表达式是指仅平凡地选择源元素的表达式。转换的后续阶段通过将其替换为其源来删除由其他转换步骤引入的退化查询。然而，必须确保查询表达式的结果永远不是源对象本身，因为这会向查询的客户端揭示源的类型和标识。因此，此步骤通过显式在源上调用 Select 来保护直接在源代码中编写的退化查询。然后，Select 和其他查询运算符的实现者有责任确保这些方法永远不会返回源对象本身。

## 7.16.2.4 from、let、where、join 和 orderby 子句

> JOSEPH ALBAHARI 本节中看起来繁琐的转换正是使查询语法非常有用的原因：它们消除了手工编写繁琐查询的需要。鉴于 lambda 表达式和扩展方法的功能，如果没有这个问题，可能很难为 C# 3.0 引入查询表达式语法提供正当理由。
> 
> 更复杂转换中的共同主题是将数据投影到临时匿名类型中，以便在 let、from 或 join 子句之后保持前一个范围变量的作用域。

带有一个第二个 from 子句后跟 select 子句的查询表达式

```
from x1 in e1
from x2 in e2
select o
```

被翻译成

```
from * in ( e₁ ) . SelectMany( x₁ => e₂ , ( x₁ , x₂ ) => new { x₁ , x₂ } )
```

### 带有一个 let 子句的查询表达式

```
from x in e
let y = f
...
```

被翻译成

```
from * in ( e ) . Select ( x => new { x , y = f } )
...
```

### 带有一个 where 子句的查询表达式

```
from x in e
where f
...
```

被翻译成

```
from x in ( e ) . Where ( x => f )
...
```

### 带有一个没有 into 的 join 子句后跟 select 子句的查询表达式

```
from x₁ in e₁
join x₂ in e₂ on k₁ equals k₂
select v
```

被翻译成

```
( e₁ ) . Join( e₂ , x₁ => k₁ , x₂ => k₂ , ( x₁ , x₂ ) => v )
```

### 带有一个没有 into 的 join 子句后跟除 select 子句之外的其他内容的查询表达式

```
from x₁ in e₁
join x₂ in e₂ on k₁ equals k₂
...
```

被翻译成

```
from * in ( e₁ ) . Join( e₂ , x₁ => k₁ , x₂ => k₂ , ( x₁ , x₂ ) => new { x₁ , x₂ } )
...
```

带有一个 into 的 join 子句后跟 select 子句的查询表达式

```
from x1 in e1
join x2 in e2 on k1 equals k2 into g
select v
```

被翻译成

```
( e1 ) . GroupJoin( e2 , x1 => k1 , x2 => k2 , ( x1 , g ) => v )
```

带有一个 into 的 join 子句后跟除 select 子句之外的其他内容的查询表达式

```
from x1 in e1
join x2 in e2 on k1 equals k2 into g
...
```

被翻译成

```
from * in ( e1 ) . GroupJoin( e2 , x1 => k1 , x2 => k2 , ( x1 , g ) => new { x1 , g } )
```

带有一个 orderby 子句的查询表达式

```
from x in e
orderby k1 , k2 , ... , kn
...
```

被翻译成

```
from x in ( e ) .
OrderBy ( x => k1 ) .
ThenBy ( x => k2 ) .
...
ThenBy ( x => kn )
...
```

如果排序子句指定了降序方向指示符，则会生成 OrderByDescending 或 ThenByDescending 的调用。

以下转换假设没有 let、where、join 或 orderby 子句，并且每个查询表达式中最多只有一个初始 from 子句。

示例

```
from c in customers
from o in c.Orders
select new { c.Name, o.OrderID, o.Total }
```

被翻译成

```
customers.
SelectMany(c => c.Orders, (c,o) => new { c.Name, o.OrderID, o.Total })
```
