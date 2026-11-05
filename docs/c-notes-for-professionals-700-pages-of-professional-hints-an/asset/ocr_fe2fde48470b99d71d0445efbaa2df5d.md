```
// anon.Equals(anon4) == false (anon and anon4 have different types, see below)
```

Two anonymous types are considered the same if and only if their properties have the same name and type and appear in the same order.

```
var anon = new { Foo = 1, Bar = 2 };
var anon2 = new { Foo = 7, Bar = 1 };
var anon3 = new { Bar = 1, Foo = 3 };
var anon4 = new { Fa = 1, Bar = 2 };
// anon and anon2 have the same type
// anon and anon3 have different types (Bar and Foo appear in different orders)
// anon and anon4 have different types (property names are different)
```

# Section 34.4: Generic methods with anonymous types

Generic methods allow the use of anonymous types through type inference.

```
void Log<T>(T obj) {
    // ...
}
Log(new { Value = 10 });
```

This means LINQ expressions can be used with anonymous types:

```
var products = new[] {
    new { Amount = 10, Id = 0 },
    new { Amount = 20, Id = 1 },
    new { Amount = 15, Id = 2 }
};
var idsByAmount = products.OrderBy(x => x.Amount).Select(x => x.Id);
// idsByAmount: 0, 2, 1
```

# Section 34.5: Instantiating generic types with anonymous types

Using generic constructors would require the anonymous types to be named, which is not possible. Alternatively, generic methods may be used to allow type inference to occur.

```
var anon = new { Foo = 1, Bar = 2 };
var anon2 = new { Foo = 5, Bar = 10 };
List<T> CreateList<T>(params T[] items) {
    return new List<T>(items);
}
var list1 = CreateList(anon, anon2);
```

In the case of List<T>, implicitly typed arrays may be converted to a List<T> through the ToList LINQ method:

```
var list2 = new[] {anon, anon2}.ToList();
```

# Section 34.6: Implicitly typed arrays

Arrays of anonymous types may be created with implicit typing.

```
var arr = new[] {
    new { Id = 0 },
```