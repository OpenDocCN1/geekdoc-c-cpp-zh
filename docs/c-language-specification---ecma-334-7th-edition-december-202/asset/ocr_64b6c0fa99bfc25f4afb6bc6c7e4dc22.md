```
o => o.CustomerID,
(c, o) => new { c, o }
join d in details on o.OrderID equals d.OrderID
join p in products on d.ProductID equals p.ProductID
select new { c.Name, o.OrderDate, p.ProductName }
```

which is further reduced to

```
customers
    .Join(orders, c => c.CustomerID,
        o => o.CustomerID, (c, o) => new { c, o })
    .Join(details, * => o.OrderID, d => d.OrderID, (*, d) => new { *, d })
    .Join(products, * => d.ProductID, p => p.ProductID,
        (*, p) => new { c.Name, o.OrderDate, p.ProductName })
```

the final translation of which is

```
customers
    .Join(orders, c => c.CustomerID,
        o => o.CustomerID, (c, o) => new { c, o })
    .Join(details, x => x.o.OrderID, d => d.OrderID, (x, d) => new { x, d })
    .Join(products, y => y.d.ProductID, p => p.ProductID,
        (y, p) => new { y.x.c.Name, y.x.o.OrderDate, p.ProductName })
```

where x and y are compiler-generated identifiers that are otherwise invisible and inaccessible. end example

# 12.20.4 The query-expression pattern

The Query-expression pattern establishes a pattern of methods that types can implement to support query expressions.

A generic type C<T> supports the query-expression-pattern if its public member methods and the publicly accessible extension methods could be replaced by the following class definition. The members and accessible extenson methods is referred to as the "shape" of a generic type C<T>. A generic type is used in order to illustrate the proper relationships between parameter and return types, but it is possible to implement the pattern for non-generic types as well.

```
delegate R Func<T1,R>(T1 arg1);
delegate R Func<T1,T2,R>(T1 arg1, T2 arg2);

class C
{
    public C<T> Cast<T>() { ... }
}

class C<T> : C
{
    public C<T> Where(Func<T,bool> predicate) { ... }
    public C<U> Select<U>(Func<T,U> selector) { ... }
    public C<U> SelectMany<U,V>(Func<T,C<U>> selector,
        Func<T,U,V> resultSelector) { ... }
    public C<U> Join<U,K,V>(C<U> inner, Func<T,K> outerKeySelector,
        Func<U,K> innerKeySelector, Func<T,U,V> resultSelector) { ... }
    public C<U> GroupJoin<U,K,V>(C<U> inner, Func<T,K> outerKeySelector,
        Func<U,K> innerKeySelector, Func<T,C<U>,V> resultSelector) { ... }
    public O<T> OrderBy<K>(Func<T,K> keySelector) { ... }
    public O<T> OrderByDescending<K>(Func<T,K> keySelector) { ... }
```