# 7.16 Query expressions

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