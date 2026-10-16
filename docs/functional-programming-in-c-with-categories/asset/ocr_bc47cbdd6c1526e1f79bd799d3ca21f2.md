![](bbox=[0.33, 0.11, 0.78, 0.32])

F(f∘g) = F(f) ∘ F(g)

This simply states that for any functions f and g the following must hold functor(value).map(x=>f(g(x))).value ≡ functor(value).map(f).map(g). Or in a Visual form:

![](bbox=[0.23, 0.42, 0.84, 0.54])

Again, those two laws seem that are mathematically strict, but in real software development, those two conditions express a well-designed map method that behaves as someone would expect it to behave.

we expect for example that those two expressions should give the same result:

```
new[] { 2.0, 3, 4, 5 }.ToList().Map(discountedPrice.Compose(title));
```

```
new[] { 2.0, 3, 4, 5 }.ToList().Map(discountedPrice).Map(title);
```

More generally for all f and g the following should hold:

```
// Law 1-identity preserving fmap id = id
```

```
Id(value).Map(x=>x).value ≡ (value)
```

```
// Law 2-composition of functions is preserved fmap (f . g)== fmap f . fmap g
```

```
Id (value).Map(x=>f(g(x))).value ≡ Id (value).Map(f).Map(g).value
```