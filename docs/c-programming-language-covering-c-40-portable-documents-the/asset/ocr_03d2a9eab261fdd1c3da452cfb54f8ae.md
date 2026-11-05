# 7.16.2.2 Explicit Range Variable Types

A from clause that explicitly specifies a range variable type

```
from T x in e
```

is translated into

```
from x in ( e ) . Cast < T > ( )
```

A join clause that explicitly specifies a range variable type

```
join T x in e on k₁ equals k₂
```

is translated into

```
join x in ( e ) . Cast < T > ( ) on k₁ equals k₂
```

The translations in the following sections assume that queries have no explicit range variable types.

The example

```
from Customer c in customers
where c.City == "London"
select c
```

is translated into

```
from c in customers.Cast<Customer>()
where c.City == "London"
select c
```

the final translation of which is

```
customers.
Cast<Customer>().
Where(c => c.City == "London")
```

Explicit range variable types are useful for querying collections that implement the non-generic IEnumerable interface, but not the generic IEnumerable<T> interface. In the example above, this would be the case if customers were of type ArrayList.

# 7.16.2.3 Degenerate Query Expressions

A query expression of the form

```
from x in e select x
```

is translated into

```
( e ) . Select ( x => x )
```