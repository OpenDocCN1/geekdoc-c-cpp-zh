```
(orders)
.OrderBy(o => o.Customer.Name)
.ThenByDescending(o => o.Total)
end example
```

The following translations assume that there are no let, where, join or orderby clauses, and no more than the one initial from clause in each query expression.

# 12.20.3.6 Select clauses

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

# 12.20.3.7 Group clauses

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

# 12.20.3.8 Transparent identifiers

Certain translations inject range variables with transparent identifiers denoted by *. Transparent identifiers exist only as an intermediate step in the query-expression translation process.