```
instance functorParser :: Functor (Parser e) where
  map :: ∀ a b. (a -> b) -> Parser e a -> Parser e b
  map f (Parser g) = Parser \s -> f <$> g s      -- COMPILER ERROR!!
```

And our new compiler error is:

```
import Data.Tuple (Tuple)
import Effect (Effect)
import Effect.Console (log)

type ParserState a = Tuple String a

class ParserError e

type ParserFunction a e = ParserError e

data Parser e a = Parser (ParserFunction

instance functorParser :: Functor (Parse
  map :: ∀ a b. (a -> b) -> Parser e a -
  map f (Parser g) = Parser \s -> f <$> g s
Could not match type

Tuple String a1

with type

a1

while trying to match type Either e2 (Tuple String a1)
with type t0 a1
while checking that expression g s
has type t0 a1
in value declaration functorParser
```

From this error we can see that we’ve made 1 hop, i.e. into Either, but we need to map again so we map the a0 inside the Tuple.

Good thing we made a the second Parameter of our Tuple. If the Type Parameters were swapped, we wouldn’t be able to use map to map a, We’d have to use lmap from Bifunctor instead, which isn’t terrible but I’d rather stick with map when possible.

So how do we do this map? We can’t just add another <$> :

```
f <$> <$> g s      -- COMPILER ERROR!!
```

That’s not a valid use of a Binary Operator. Can you think of a way?

We have:

```
f <$> g s
```

We want to map f again. If you have any ideas, then give them a try and see how you do. If not, keep reading.

Let’s rewrite this using map instead of <$> to see if that gives us some insight: