We could look it up, but I’m not exactly sure of which Error this is. Probably the one in Effect.Exception and if I’m right, it has a Show Instance, which will turn it into a String.

But, honestly, it’s actually faster to just lmap show over the Aff and if the compiler doesn’t complain, then we’re good:

```
import Data.Bifunctor (lmap) ①

createAccount :: Account -> Aff (Either String Unit)
createAccount account =
  -- COMPILER ERROR!!
  let x = lmap show <$> try $ appendTextFile ASCII
          accountsFile $ accountToCSV account :: ?x ②
  in pure $ pure unit
```

① Import lmap.

② The map via <$> maps into the Aff, which contains an Either. Then the lmap show will map over the left side of the Either.

The compiler error:

![](bbox=[0.235, 0.48, 0.765, 0.63])

When I see code with a lot of Binary Operators and an incomprehensible error like this, I always start adding Parentheses to see if I have a Precedence problem:

```
createAccount :: Account -> Aff (Either String Unit)
createAccount account =
  let x = lmap show <$> (try $ appendTextFile ASCII
          accountsFile $ accountToCSV account) :: ?x ①
  in pure $ pure unit
```

① Added Parentheses left of <$>.

And now with the compiler error gone, we get the following Type Hole message: