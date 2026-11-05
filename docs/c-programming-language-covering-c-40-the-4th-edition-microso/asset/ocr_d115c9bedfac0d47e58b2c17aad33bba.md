```
```text
( e ) . Select( x => v )
```
```

except when *v* is the identifier *x*, the translation is simply

```
```text
( e )
```
```

For example,

```
```csharp
from c in customers.Where(c => c.City == "London")
select c
```
```

is simply translated into

```
```csharp
customers.Where(c => c.City == "London")
```
```

# 7.16.2.6  *GroupBy* Clauses

A query expression of the form

```
```text
from x in e group v by k
```
```

is translated into

```
```text
( e ) . GroupBy( x => k , x => v )
```
```

except when *v* is the identifier *x*, the translation is

```
```text
( e ) . GroupBy( x => k )
```
```

The example

```
```csharp
from c in customers
group c.Name by c.Country
```
```

is translated into

```
```csharp
customers.
GroupBy(c => c.Country, c => c.Name)
```
```

# 7.16.2.7  *Transparent Identifiers*

Certain translations inject range variables with *transparent identifiers* denoted by *. Transparent identifiers are not a proper language feature; they exist only as an intermediate step in the query expression translation process.

When a query translation injects a transparent identifier, further translation steps propagate the transparent identifier into anonymous functions and anonymous object initializers. In those contexts, transparent identifiers have the following behavior:

+   - When a transparent identifier occurs as a parameter in an anonymous function, the members of the associated anonymous type are automatically in scope in the body of the anonymous function.