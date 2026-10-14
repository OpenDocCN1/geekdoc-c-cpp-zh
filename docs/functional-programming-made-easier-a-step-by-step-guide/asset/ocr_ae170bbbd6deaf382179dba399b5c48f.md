The syntax is ? followed by a lowercase name. I usually don’t care about the name since I’m using an IDE, i.e. VSCode. The name is more important if you’re compiling at the command line and you have several Type Holes and need to distinguish them from one another.

In Haskell, Type Holes are unnamed and are the underscore character, _ and do not have the same restriction for requiring a clean compile to provide useful Type inference information.

Now, we’ll just add the Stack execution code that matches the order of our Monad Stack, i.e. ExceptT first, then WriterT and so on:

```
runApp :: Int -> AppM String String Int Unit -> ?x
runApp s = flip runStateT s <<< runWriterT <<< runExceptT
```

Once this compiles, the compiler will tell us the following:

![](bbox=[0.146, 0.365, 0.854, 0.514])

This saves us from having to figure out this complex Type and we can now replace our Type Hole with the inferred Type. Let’s also add unwrap to eliminate the Identity Monad:

```
import Data.Newtype (unwrap) ①

runApp
  :: Int
  -> AppM String String Int Unit
  -> Tuple (Tuple (Either String Unit) String) Int ②
runApp s = unwrap <<< flip runStateT s <<< runWriterT <<< runExceptT
```

① Import unwrap.

② The inferred Type from the Type Hole minus Identity since we’re unwrapping now.

And just because our code compiles doesn’t mean we’re done. Let’s take a look at it in full for any areas of improvement: