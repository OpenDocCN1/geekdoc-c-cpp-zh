Can you see where we went wrong? Turns out, we cannot use 0 since that’s the Additive Identity for Int. But this Function needs to work with all Semirings not just Int.

This is why Semiring has the value zero. A zero for Int is 0, but a zero for Number is 0.0. Let’s fix this by using a’s zero value:

```
addr :: ∀ a. Semiring a => Moore a a a
addr = Moore zero identity (+) ①
```

① The compiler will use the appropriate zero depending on what Type a unifies to. If a unifies with Int, then zero will be 0. If a unifies with Number, then zero will be 0.0.

Now, we have a general addr Function. Next, we need to write the interpreter that will take this Fold Definition and actually perform the foldl operation. We’re going to call this Function, runFoldL.

# 15.15. Writing runFoldL

We can finally add some test code to test the code we’ve been writing:

```
log "________________________"
log $ show $ runFoldL addr [1, 2, 3] ①
log $ show $ runFoldL addr (1.0 : 2.0 : 3.0 : Nil) ②
```

① Prints 6.

② Prints 6.0.

You’re also going to need the following imports:

```
import Data.Foldable (class Foldable, foldl)
import Data.List (List(..), (:))
```

Next, write a Function called runFoldL that takes a Moore, i.e. a Fold Definition, and a Foldable and performs the operation. Take a look at the test code to see how it’s used.

Take a swing at this before reading the solution. Even if all you get is the Type Signature, that’s better than not trying at all.

# 15.16. Code for runFoldL

First, as always, we write the Type Signature. runFoldL will take a Moore and a Foldable of Type a and perform the foldl over that Data Structure to produce a final result, b: