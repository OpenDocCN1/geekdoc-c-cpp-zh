```
doNothingWithLog :: Writer (Array String) Int
doNothingWithLog = bind
  (Writer (Tuple unit ["We did nothing"])) (\_ -> pure 0)
```

And next, we’ll substitute pure with its definition, i.e. pure x = Writer (Tuple x mempty) and apply 0 to it:

```
doNothingWithLog :: Writer (Array String) Int
doNothingWithLog = bind
  (Writer (Tuple unit ["We did nothing"])) (\_ -> Writer (Tuple 0 mempty))
```

Then we’ll substitute bind with its definition and apply the 2 Parameters. First, here’s bind’s definition:

```
instance bindWriter :: Monoid w => Bind (Writer w) where
  bind (Writer (Tuple x l1)) f =
    f x # \(Writer (Tuple y l2)) -> Writer (Tuple y (l1 <> l2))
```

And now we’ll substitute:

```
doNothingWithLog :: Writer (Array String) Int
doNothingWithLog = (\_ -> Writer (Tuple 0 mempty)) unit
  # \(Writer (Tuple y l2)) -> Writer (Tuple y (["We did nothing"] <> l2))
```

And then we’ll apply the first Function:

```
doNothingWithLog :: Writer (Array String) Int
doNothingWithLog = (Writer (Tuple 0 mempty))
  # \(Writer (Tuple y l2)) -> Writer (Tuple y (["We did nothing"] <> l2))
```

Then we’ll apply using #, where 0 binds to y and mempty binds to l2.

```
doNothingWithLog :: Writer (Array String) Int
doNothingWithLog = Writer (Tuple 0 (["We did nothing"] <> mempty))
```

And finally, we’ll apply <>: