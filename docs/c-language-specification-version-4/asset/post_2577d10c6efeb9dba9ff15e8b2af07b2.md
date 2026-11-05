
## 7.16 Query expressions

*Query expressions* provide a language integrated syntax for queries that is similar to relational and hierarchical query languages such as SQL and XQuery.

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

A query expression begins with a from clause and ends with either a select or group clause. The initial from clause can be followed by zero or more from, let, where, join or orderby clauses. Each from clause is a generator introducing a range variable which ranges over the elements of a sequence. Each let clause introduces a range variable representing a value computed by means of previous range variables. Each where clause is a filter that excludes items from the result. Each join clause compares specified keys of the source sequence with keys of another sequence, yielding matching pairs. Each orderby clause reorders items according to specified criteria. The final select or group clause specifies the shape of the result in terms of the range variables. Finally, an into clause can be used to “splice” queries by treating the results of one query as a generator in a subsequent query.

### 7.16.1 Ambiguities in query expressions

Query expressions contain a number of “contextual keywords”, i.e., identifiers that have special meaning in a given context. Specifically these are from, where, join, on, equals, into, let, orderby, ascending, descending, select, group and by. In order to avoid ambiguities in query expressions caused by mixed use of these identifiers as keywords or simple names, these identifiers are considered keywords when occurring anywhere within a query expression.

For this purpose, a query expression is any expression that starts with “from identifier” followed by any token except “;”, “=” or “,”.

In order to use these words as identifiers within a query expression, they can be prefixed with “@” (§2.4.2).

### 7.16.2 Query expression translation

The C# language does not specify the execution semantics of query expressions. Rather, query expressions are translated into invocations of methods that adhere to the query expression pattern (§7.16.3). Specifically, query expressions are translated into invocations of methods named where, Select, SelectMany, Join, GroupJoin, OrderBy, OrderByDescending, ThenBy, ThenByDescending, GroupBy, and Cast. These methods are expected to have particular signatures and result types, as described in §7.16.3. These methods can be instance methods of the object being queried or extension methods that are external to the object, and they implement the actual execution of the query.

The translation from query expressions to method invocations is a syntactic mapping that occurs before any type binding or overload resolution has been performed. The translation is guaranteed to be syntactically correct, but it is not guaranteed to produce semantically correct C# code. Following translation of query expressions, the resulting method invocations are processed as regular method invocations, and this may in turn uncover errors, for example if the methods do not exist, if arguments have wrong types, or if the methods are generic and type inference fails.

A query expression is processed by repeatedly applying the following translations until no further reductions are possible. The translations are listed in order of application: each section assumes that the translations in the preceding sections have been performed exhaustively, and once exhausted, a section will not later be revisited in the processing of the same query expression.

Assignment to range variables is not allowed in query expressions. However a C# implementation is permitted to not always enforce this restriction, since this may sometimes not be possible with the syntactic translation scheme presented here.

Certain translations inject range variables with transparent identifiers denoted by *. The special properties of transparent identifiers are discussed further in §7.16.2.7.

### 7.16.2.1 Select and groupby clauses with continuations

A query expression with a continuation

```
from ... into x ...
```

is translated into

```
from x in ( from ... ) ...
```

The translations in the following sections assume that queries have no into continuations.

The example

```
from c in customers
group c by c.Country into g
select new { Country = g.Key, CustCount = g.Count() }
```

is translated into

```
from g in
    from c in customers
    group c by c.Country
select new { Country = g.Key, CustCount = g.Count() }
```

the final translation of which is

```
customers.
GroupBy(c => c.Country).
Select(g => new { Country = g.Key, CustCount = g.Count() })
```

### 7.16.2.2 Explicit range variable types

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
join T x in e on k1 equals k2
```

is translated into

```
join x in ( e ) . Cast < T > ( ) on k1 equals k2
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
where(c => c.City == "London")
```

Explicit range variable types are useful for querying collections that implement the non-generic IEnumerable interface, but not the generic IEnumerable<T> interface. In the example above, this would be the case if customers were of type ArrayList.

### 7.16.2.3 Degenerate query expressions

A query expression of the form

```
from x in e select x
```

is translated into

```
( e ) . Select ( x => x )
```

The example

```
from c in customers
select c
```

is translated into

```
customers.Select(c => c)
```

A degenerate query expression is one that trivially selects the elements of the source. A later phase of the translation removes degenerate queries introduced by other translation steps by replacing them with their source. It is important however to ensure that the result of a query expression is never the source object itself, as that would reveal the type and identity of the source to the client of the query. Therefore this step protects degenerate queries written directly in source code by explicitly calling Select on the source. It is then up to the implementers of Select and other query operators to ensure that these methods never return the source object itself.

### 7.16.2.4 From, let, where, join and orderby clauses

A query expression with a second from clause followed by a select clause

```
from x1 in e1
from x2 in e2
select v
```

is translated into

```
( e1 ) . SelectMany( x1 => e2 , ( x1 , x2 ) => v )
```

**A query expression with a where clause**

```
from x in e
where f
...
```

is translated into

```
from x in ( e ) . Where ( x => f )
...
```

**A query expression with a join clause without an into followed by a select clause**

```
from x1 in e1
join x2 in e2 on k1 equals k2
select v
```

is translated into

```
( e1 ) . Join( e2 , x1 => k1 , x2 => k2 , ( x1 , x2 ) => v )
```

**A query expression with a join clause without an into followed by something other than a select clause**

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

**A query expression with a join clause with an into followed by a select clause**

```
from x1 in e1
join x2 in e2 on k1 equals k2 into g
select v
```

is translated into

```
( e1 ) . GroupJoin( e2 , x1 => k1 , x2 => k2 , ( x1 , g ) => v )
```

**A query expression with a join clause with an into followed by something other than a select clause**

```
from x1 in e1
join x2 in e2 on k1 equals k2 into g
```

is translated into

```
from * in ( e1 ) . GroupJoin(
    e2 , x1 => k1 , x2 => k2 , ( x1 , g ) => new { x1 , g })
...
```

**A query expression with an orderby clause**

```
from x in e
orderby k1 , k2 , ... , kn
...
```

is translated into
