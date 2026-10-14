```
component
  :: ∀ m
  . MonadAff m
  -- COMPILER ERROR!!
  => H.Component Query Input Output m
```

Here’s the error:

![](bbox=[0.412, 0.238, 0.588, 0.412])

Looks like Query takes a Parameter, so let’s give it one:

```
type Query a = Void -- COMPILER ERROR!!
```

Now, we have a different error:

![](bbox=[0.323, 0.56, 0.677, 0.646])

Looks like we cannot have a Phantom on Type Aliases. We can change it to a real Type or we can use a Type called Const:

```
newtype Const a b = Const a
```

This lets us do:

```
import Data.Const (Const)

type Query :: ∀ k. k -> Type ①
type Query = Const Void
```

① Const takes 2 parameter. We are only Partially Applying Void to Const. Because of this, the compiler