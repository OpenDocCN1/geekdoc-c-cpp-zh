# 5.16.1. Hint for `head`

If you haven’t finished writing `head` yet, go ahead and comment out what you did write and add the following stubbed out version of `head`:

```
head :: ∀ a. List a -> Maybe a
head _ = Nothing
```

This function is just so you can follow along.

If you have a completed Function for `head`, then you probably noticed that the compiler is complaining that it didn’t know what `Maybe` was. That’s because you need to import it from `Data.Maybe`.

So, if you haven’t tried that, please do so now before reading on.

If you simply added the following:

```
import Data.Maybe (Maybe)
```

but you’re now you’re getting an error on `Nothing` and/or `Just`, it’s because the above import only imports the Type `Maybe`. It doesn’t import the Data Constructors, `Nothing` and `Just`.

Remember, the only way we can construct something of Type `Maybe` is to use its Data Constructors.

So we need to change our `import` statement to:

```
import Data.Maybe (Maybe(..))
```

That should fix all of your problems with `Maybe`, et al. But, now the compiler has a problem with the test code I gave you. You’re probably getting an error like: