
the final translation of which is:

```
customers.
GroupBy(c => c.Country).
Select(g => new { Country = g.Key, CustCount = g.Count() })
```

end example

## 12.20.3.3 Explicit range variable types

A from clause that explicitly specifies a range variable type

```
from «T» «x» in «e»
```

is translated into

```
from «x» in ( «e» ) . Cast < «T» > ( )
```

A join clause that explicitly specifies a range variable type

```
join «T» «x» in «e» on «k1» equals «k2»
```

is translated into

```
join «x» in ( «e» ) . Cast < «T» > ( ) on «k1» equals «k2»
```

The translations in the following sections assume that queries have no explicit range variable types.

Example: The example

```
from Customer c in customers
where c.City == "London"
select c
```

is translated into

```
from c in (customers).Cast<Customer>()
where c.City == "London"
select c
```

the final translation of which is

```
customers.
Cast<Customer>().
Where(c => c.City == "London")
```

end example

Note: Explicit range variable types are useful for querying collections that implement the non-generic IEnumerable interface, but not the generic IEnumerable<T> interface. In the example above, this would be the case if customers were of type ArrayList. end note

## 12.20.3.4 Degenerate query expressions

A query expression of the form

```
from «x» in «e» select «x»
```

is translated into

```
( «e» ) . Select ( «x» => «x» )
```

Example: The example

```
from c in customers
select c
```

is translated into

```
(customers).Select(c => c)
```

end example

A degenerate query expression is one that trivially selects the elements of the source.

> Note: Later phases of the translation (§12.20.3.6 and §12.20.3.7) remove degenerate queries introduced by other translation steps by replacing them with their source. It is important, however, to ensure that the result of a query expression is never the source object itself. Otherwise, returning the result of such a query might inadvertently expose private data (e.g., an element array) to a caller. Therefore this step protects degenerate queries written directly in source code by explicitly calling Select on the source. It is then up to the implementers of Select and other query operators to ensure that these methods never return the source object itself. end note

## 12.20.3.5 From, let, where, join and orderby clauses

A query expression with a second from clause followed by a select clause

```
from «x1» in «e1»
from «x2» in «e2»
select «v»
```

is translated into

```
( «e1» ) . SelectMany( «x1» => «e2» , ( «x1» , «x2» ) => «v» )
```

Example: The example

```
from c in customers
from o in c.Orders
select new { c.Name, o.OrderID, o.Total }
```

is translated into

```
(customers).
SelectMany(c => c.Orders,
(c,o) => new { c.Name, o.OrderID, o.Total }
)
```

end example

A query expression with a second from clause followed by a query body Q containing a non-empty set of query body clauses:

```
from «x1» in «e1»
from «x2» in «e2»
Q
```

is translated into

```
from * in («e1») . SelectMany( «x1» => «e2» , ( «x1» , «x2» ) => new { «x1» , «x2» } )
Q
```

Example: The example

```
from c in customers
from o in c.Orders
orderby o.Total descending
select new { c.Name, o.OrderID, o.Total }
```

is translated into

```
from * in (customers).
    SelectMany(c => c.Orders, (c,o) => new { c, o })
    orderby o.Total descending
    select new { c.Name, o.OrderID, o.Total }
```

the final translation of which is

```
customers.
SelectMany(c => c.Orders, (c,o) => new { c, o }).
OrderByDescending(x => x.o.Total).
Select(x => new { x.c.Name, x.o.OrderID, x.o.Total })
```

where x is a compiler generated identifier that is otherwise invisible and inaccessible.

end example

A let expression along with its preceding from clause:

```
from «x» in «e»
let «y» = «f»
...
```

is translated into

```
from * in ( «e» ) . Select ( «x» => new { «x» , «y» = «f» } )
...
```

Example: The example

```
from o in orders
let t = o.Details.Sum(d => d.UnitPrice * d.Quantity)
where t >= 1000
select new { o.OrderID, Total = t }
```

is translated into

```
from * in (orders).Select(
    o => new { o, t = o.Details.Sum(d => d.UnitPrice * d.Quantity) })
where t >= 1000
select new { o.OrderID, Total = t }
```

the final translation of which is

```
orders
.Select(o => new { o, t = o.Details.Sum(d => d.UnitPrice * d.Quantity) })
.Where(x => x.t >= 1000)
.Select(x => new { x.o.OrderID, Total = x.t })
```

where x is a compiler generated identifier that is otherwise invisible and inaccessible.

end example

A where expression along with its preceding from clause:

```
from «x» in «e»
where «f»
...
```

is translated into

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

is translated into

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

the final translation of which is

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

where x and y are compiler generated identifiers that are otherwise invisible and inaccessible.

*end example*

An orderby clause and its preceding from clause:

```
    from «x» in «e»
    orderby «k1» , «k2» , ... , «kn»
    ...
```

is translated into

```
    from «x» in ( «e» ) .
        OrderBy ( «x» => «k1» ) .
        ThenBy ( «x» => «k2» ) .
        ...
        ThenBy ( «x» => «kn» )
        ...
```

If an ordering clause specifies a descending direction indicator, an invocation of OrderByDescending or ThenByDescending is produced instead.

*Example: The example*

```
    from o in orders
    orderby o.Customer.Name, o.Total descending
    select o
```

has the final translation

```
(orders)
.OrderBy(o => o.Customer.Name)
.ThenByDescending(o => o.Total)
end example
```

The following translations assume that there are no let, where, join or orderby clauses, and no more than the one initial from clause in each query expression.

## 12.20.3.6 Select clauses

A query expression of the form

```
from «x» in «e» select «v»
```

is translated into

```
( «e» ) . Select ( «x» => «v» )
```

except when «v» is the identifier «x», the translation is simply

```
( «e» )
```

Example: The example

```
from c in customers.Where(c => c.City == "London")
select c
```

is simply translated into

```
(customers).Where(c => c.City == "London")
```

end example

## 12.20.3.7 Group clauses

A group clause

```
from «x» in «e» group «v» by «k»
```

is translated into

```
( «e» ) . GroupBy ( «x» => «k» , «x» => «v» )
```

except when «v» is the identifier «x», the translation is

```
( «e» ) . GroupBy ( «x» => «k» )
```

Example: The example

```
from c in customers
group c.Name by c.Country
```

is translated into

```
(customers).GroupBy(c => c.Country, c => c.Name)
```

## 12.20.3.8 Transparent identifiers

Certain translations inject range variables with transparent identifiers denoted by *. Transparent identifiers exist only as an intermediate step in the query-expression translation process.

When a query translation injects a transparent identifier, further translation steps propagate the transparent identifier into anonymous functions and anonymous object initializers. In those contexts, transparent identifiers have the following behavior:

- When a transparent identifier occurs as a parameter in an anonymous function, the members of the associated anonymous type are automatically in scope in the body of the anonymous function.
- When a member with a transparent identifier is in scope, the members of that member are in scope as well.
- When a transparent identifier occurs as a member declarator in an anonymous object initializer, it introduces a member with a transparent identifier.

In the translation steps described above, transparent identifiers are always introduced together with anonymous types, with the intent of capturing multiple range variables as members of a single object. An implementation of C# is permitted to use a different mechanism than anonymous types to group together multiple range variables. The following translation examples assume that anonymous types are used, and shows one possible translation of transparent identifiers.

Example: The example

```
```
from c in customers
from o in c.Orders
orderby o.Total descending
select new { c.Name, o.Total }
```
```

is translated into

```
```
from * in (customers).SelectMany(c => c.Orders, (c,o) => new { c, o })
orderby o.Total descending
select new { c.Name, o.Total }
```
```

which is further translated into

```
```
customers
    .SelectMany(c => c.Orders, (c,o) => new { c, o })
    .OrderByDescending(* => o.Total)
    .Select(* => new { c.Name, o.Total })
```
```

which, when transparent identifiers are erased, is equivalent to

```
```
customers
    .SelectMany(c => c.Orders, (c,o) => new { c, o })
    .OrderByDescending(x => x.o.Total)
    .Select(x => new { x.c.Name, x.o.Total })
```
```

where x is a compiler generated identifier that is otherwise invisible and inaccessible.

The example

```
```
from c in customers
join o in orders on c.CustomerID equals o.CustomerID
join d in details on o.OrderID equals d.OrderID
join p in products on d.ProductID equals p.ProductID
select new { c.Name, o.OrderDate, p.ProductName }
```
```

is translated into

```
```
from * in (customers).Join(
    orders,
    c => c.CustomerID,
```
