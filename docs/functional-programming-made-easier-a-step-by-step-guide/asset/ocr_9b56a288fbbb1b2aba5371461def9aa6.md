```
log "________________________________"
log $ show $ runPredicate (cmap (_ + 1) (Predicate odd)) 10
log $ show $ runPredicate (cmap (_ + 2) (Predicate odd)) 10
log $ show $ runPredicate ((_ + 1) >$< (Predicate odd)) 10
log $ show $ runPredicate ((_ + 2) >$< (Predicate odd)) 10
```

1 Helpful for delimiting our output since they’re all Booleans.

2 Prints true.

3 Prints false.

4 Prints true.

5 Prints false.

Remember that (>$<) is the Binary Operator alias for cmap.

Notice that these tests cmap the function over the Predicate to augment the INPUT value BEFORE the Predicate function is executed.

You’ll also need to add these imports to keep the compiler happy:

```
import Data.Functor.Contravariant (cmap, (>$<))
```

Now write the Contravariant Instance for Predicate. Consult Pursuit to refresh your memory on Contravariant and look back at the previous Chapter for examples of writing such instances before moving on to the next section.

Also, keep in mind that cmap’s mapping function maps INPUTS.

# 15.7. Code for Contravariant Instance for Predicate

The instance code is very simple for Predicate. All we have to do is use cmap’s mapping function to map the INPUT to Predicate’s function. This can be accomplished using Function Composition:

```
import Data.Functor.Contravariant (class Contravariant, cmap, (>$<))

instance contravariantPredicate :: Contravariant Predicate where
  cmap f (Predicate g) = Predicate (g <<< f)
```

1 Import the Type Class Contrvariant.

2 We call f first to map the INPUT to something g expects.

Now run the test code and see what you get.