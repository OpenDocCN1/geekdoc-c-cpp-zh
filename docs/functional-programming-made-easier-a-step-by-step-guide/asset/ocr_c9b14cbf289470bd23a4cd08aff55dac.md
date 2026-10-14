```
getAccounts :: AVar Accounts -> Aff (Array Account)
getAccounts accountsAVar = AVar.read accountsAVar >>= ???
```

① We’ll want to bind to a Function that will extract out just the Values of the Map.

And now, we’ll use values to extract just the values:

```
getAccounts :: AVar Accounts -> Aff (Array Account)
getAccounts accountsAVar =
  AVar.read accountsAVar >>= pure <<< Map.values -- COMPILER ERROR!!
```

① Don’t forget to wrap the results in Aff using pure. We are using bind after all.

And now we have the following compiler error:

![](bbox=[0.322, 0.37, 0.677, 0.508])

Can you see the problem?

Looks like values returns a List not an Array. If you like, you can look it up. But, I’m just going to add fromFoldable into the mix and see if that fixes it:

```
import Data.Array (fromFoldable)

getAccounts :: AVar Accounts -> Aff (Array Account)
getAccounts accountsAVar =
  AVar.read accountsAVar >>= pure <<< fromFoldable <<< Map.values
```

① Import fromFoldable.

② Convert the List that Map.values gives us to an Array using fromFoldable.

And this fixes it.

At this point you might be wondering why even write this Function. We could just call AVar.read in our code and you’d be right. But this approach is nice for 3 reasons.

First, it abstracts away the implementation details. We don’t have to know how the Accounts are stored in memory.