```
ordering-direction:
    ascending
    descending

select-or-group-clause:
    select-clause
    group-clause

select-clause:
    select expression

group-clause:
    group expression by expression

query-continuation:
    into identifier query-body
```

A query expression begins with a from clause and ends with either a select or group clause. The initial from clause may be followed by zero or more from, let, where, join or orderby clauses. Each from clause is a generator introducing a range variable that ranges over the elements of a sequence. Each let clause introduces a range variable representing a value computed by means of previous range variables. Each where clause is a filter that excludes items from the result. Each join clause compares specified keys of the source sequence with keys of another sequence, yielding matching pairs. Each orderby clause reorders items according to specified criteria. The final select or group clause specifies the shape of the result in terms of the range variables. Finally, an into clause can be used to “splice” queries by treating the results of one query as a generator in a subsequent query.

# 12.17.2 Ambiguities in query expressions

Query expressions use a number of contextual keywords (§7.4.4): ascending, by, descending, equals, from, group, into, join, let, on, orderby, select and where.

To avoid ambiguities that could arise from the use of these identifiers both as keywords and simple names these identifiers are considered keywords anywhere within a query expression, unless they are prefixed with “@” (§7.4.4) in which case they are considered identifiers. For this purpose, a query expression is any expression that starts with “from identifier” followed by any token except “;”, “=” or “,”.

# 12.17.3 Query expression translation

# 12.17.3.1 General

The C# language does not specify the execution semantics of query expressions. Rather, query expressions are translated into invocations of methods that adhere to the query-expression pattern (§12.17.4). Specifically, query expressions are translated into invocations of methods named where, Select, SelectMany, Join, GroupJoin, OrderBy, OrderByDescending, ThenBy, ThenByDescending, GroupBy, and Cast. These methods are expected to have particular signatures and return types, as described in §12.17.4. These methods may be instance methods of the object being queried or extension methods that are external to the object. These methods implement the actual execution of the query.

The translation from query expressions to method invocations is a syntactic mapping that occurs before any type binding or overload resolution has been performed. Following translation of query expressions, the resulting method invocations are processed as regular method invocations, and this may in turn uncover compile time errors. These error conditions include, but are not limited to, methods that do not exist, arguments of the wrong types, and generic methods where type inference fails.

A query expression is processed by repeatedly applying the following translations until no further reductions are possible. The translations are listed in order of application: each section assumes that the translations in the preceding sections have been performed exhaustively, and once exhausted, a section will not later be revisited in the processing of the same query expression.