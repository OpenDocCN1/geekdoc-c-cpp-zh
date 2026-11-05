# (Inner) Join

```
```csharp
var result = from f in first
    join s in second on f equals s
    select new { f, s };

var result = first.Join(second,
    f => f,
    s => s,
    (f, s) => new { f, s });

// Result: {"a","a"}
//         {"c","c"}
```
```

# Left outer join

```
```csharp
var leftOuterJoin = from f in first
    join s in second on f equals s into temp
    from t in temp.DefaultIfEmpty()
    select new { First = f, Second = t };

// Or can also do:
var leftOuterJoin = from f in first
    from s in second.Where(x => x == f).DefaultIfEmpty()
    select new { First = f, Second = s };

// Result: {"a","a"}
//         {"b", null}
//         {"c","c"}

// Left outer join method syntax
var leftOuterJoinFluentSyntax = first.GroupJoin(second,
    f => f,
    s => s,
    (f, s) => new { First = f, Second = s })
    .SelectMany(temp => temp.Second.DefaultIfEmpty(),
    (f, s) => new { First = f.First, Second = s });
```
```

# Right Outer Join

```
```csharp
var rightOuterJoin = from s in second
    join f in first on s equals f into temp
    from t in temp.DefaultIfEmpty()
    select new {First=t,Second=s};

// Result: {"a","a"}
//         {"c","c"}
//         {null,"d"}
```
```

# Cross Join

```
```csharp
var CrossJoin = from f in first
    from s in second
    select new { f, s };

// Result: {"a","a"}
//         {"a","c"}
//         {"a","d"}
//         {"b","a"}
//         {"b","c"}
//         {"b","d"}
```
```