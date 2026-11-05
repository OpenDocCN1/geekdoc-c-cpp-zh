```
join_into_clause
  : 'join' type? identifier 'in' expression 'on' expression
    'equals' expression 'into' identifier
  ;

orderby_clause
  : 'orderby' orderings
  ;

orderings
  : ordering (',' ordering)*
  ;

ordering
  : expression ordering_direction?
  ;

ordering_direction
  : 'ascending'
  | 'descending'
  ;

select_or_group_clause
  : select_clause
  | group_clause
  ;

select_clause
  : 'select' expression
  ;

group_clause
  : 'group' expression 'by' expression
  ;

query_continuation
  : 'into' identifier query_body
  ;
```

A query expression begins with a from clause and ends with either a select or group clause. The initial from clause may be followed by zero or more from, let, where, join or orderby clauses. Each from clause is a generator introducing a range variable that ranges over the elements of a sequence. Each let clause introduces a range variable representing a value computed by means of previous range variables. Each where clause is a filter that excludes items from the result. Each join clause compares specified keys of the source sequence with keys of another sequence, yielding matching pairs. Each orderby clause reorders items according to specified criteria.The final select or group clause specifies the shape of the result in terms of the range variables. Finally, an into clause can be used to "splice" queries by treating the results of one query as a generator in a subsequent query.

# 12.20.2 Ambiguities in query expressions

Query expressions use a number of contextual keywords (§6.4.4): ascending, by, descending, equals, from, group, into, join, let, on, orderby, select and where.