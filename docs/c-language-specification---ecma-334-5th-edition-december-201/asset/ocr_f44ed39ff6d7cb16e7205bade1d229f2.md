```
from x in e
where f
...
```

is translated into

```
from x in ( e ) . where ( x => f )
...
```

A join clause immediately followed by a select clause

```
from x1 in e1
join x2 in e2 on k1 equals k2
select v
```

is translated into

```
( e1 ) . Join( e2 , x1 => k1 , x2 => k2 , ( x1 , x2 ) => v )
```

[Example: The example

```
from c in customers
join o in orders on c.CustomerID equals o.CustomerID
select new { c.Name, o.OrderDate, o.Total }
```

is translated into

```
(customers).Join(orders, c => c.CustomerID, o => o.CustomerID,
(c, o) => new { c.Name, o.OrderDate, o.Total })
```

end example

A join clause followed by a query body clause:

```
from x1 in e1
join x2 in e2 on k1 equals k2
...
```

is translated into

```
from * in ( e1 ) . Join(
 e2 , x1 => k1 , x2 => k2 , ( x1 , x2 ) => new { x1 , x2 })
...
```

A join-into clause immediately followed by a select clause

```
from x1 in e1
join x2 in e2 on k1 equals k2 into g
select v
```