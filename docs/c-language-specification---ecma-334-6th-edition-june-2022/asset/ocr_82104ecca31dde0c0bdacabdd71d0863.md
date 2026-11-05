Example: The example

```
```csharp
from c in customers
from o in c.Orders
orderby o.Total descending
select new { c.Name, o.Total }
```
```

is translated into

```
```csharp
from * in (customers).SelectMany(c => c.Orders, (c,o) => new { c, o })
orderby o.Total descending
select new { c.Name, o.Total }
```
```

which is further translated into

```
```csharp
customers
    .SelectMany(c => c.Orders, (c,o) => new { c, o })
    .OrderByDescending(* => o.Total)
    .Select(* => new { c.Name, o.Total })
```
```

which, when transparent identifiers are erased, is equivalent to

```
```csharp
customers
    .SelectMany(c => c.Orders, (c,o) => new { c, o })
    .OrderByDescending(x => x.o.Total)
    .Select(x => new { x.c.Name, x.o.Total })
```
```

where x is a compiler generated identifier that is otherwise invisible and inaccessible.

The example

```
```csharp
from c in customers
join o in orders on c.CustomerID equals o.CustomerID
join d in details on o.OrderID equals d.OrderID
join p in products on d.ProductID equals p.ProductID
select new { c.Name, o.OrderDate, p.ProductName }
```
```

is translated into

```
```csharp
from * in (customers).Join(
    orders,
    c => c.CustomerID,
    o => o.CustomerID,
    (c, o) => new { c, o })
join d in details on o.OrderID equals d.OrderID
join p in products on d.ProductID equals p.ProductID
select new { c.Name, o.OrderDate, p.ProductName }
```
```

which is further reduced to

```
```csharp
customers
    .Join(orders, c => c.CustomerID, o => o.CustomerID, (c, o) => new { c, o })
    .Join(details, * => o.OrderID, d => d.OrderID, (*, d) => new { *, d })
    .Join(products, * => d.ProductID, p => p.ProductID,
        (*, p) => new { c.Name, o.OrderDate, p.ProductName })
```
```

the final translation of which is

```
```csharp
customers
    .Join(orders, c => c.CustomerID, o => o.CustomerID, (c, o) => new { c, o })
    .Join(details, x => x.o.OrderID, d => d.OrderID, (x, d) => new { x, d })
```
```