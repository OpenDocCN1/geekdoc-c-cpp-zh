
```
class Functor f <= Apply f where
  apply :: ∀ a b. f (a -> b) -> f a -> f b

infixl 4 apply as <*>
```

Again, we can see that we’ll first need a `Functor` Instance:

```
class Functor f where
  map :: ∀ a b. (a -> b) -> f a -> f b
```

We finally have something that doesn’t have a Superclass. So our plan is to first write the `Functor`, then the `Apply` and finally the `Applicative`, which is the main goal of this Chapter.

Go ahead and write the `Functor` Instance for our `Parser` before reading the solution.

If you got stuck, I’d suggest writing the Type Signature for the `map` Function specialized for `Parser`. Try that and see if it doesn’t help a bit. Once you’ve tried that, get as far as you can and then read on.

Let’s write the `Functor` Instance one line at a time and see how far we can get:

```
instance functorParser :: Functor (Parser a) where
```

Remember, that `Parser`’s Kind is `Type -> Type -> Type`. That means we’ll need to hold a Type Parameter constant.

But we’ve held the WRONG parameter constant. We want to map over the Parsed Value not the Error. We want to hold the Error Type constant like we’ve done with `Either`’s Functor instance:

```
instance functorEither :: Functor (Either a) where
  map _ (Left x) = Left x
  map f (Right y) = Right $ f y
```

So we’re going to need to SWAP our Type Parameters to our `Parser` Type:

```
newtype Parser e a = Parser (ParseFunction e a) ❶
```

> ❶ Swapped `a` and `e` from our earlier definition.

Go ahead and change your code to swap these Type Parameters.

You know, it might be a good idea to swap `a` and `e` in `ParseFunction` too. This will keep us from getting the

I'm going to first add the part where we call the original Function and pass it s (ignoring compiler errors):

```
instance functorParser :: Functor (Parser e) where
  map :: ∀ a b. (a -> b) -> Parser e a -> Parser e b
  map f (Parser g) = Parser \s -> g s        -- COMPILER ERROR!!
```

And next, I'll call our mapping Function f AFTER we've called g:

```
instance functorParser :: Functor (Parser e) where
  map :: ∀ a b. (a -> b) -> Parser e a -> Parser e b
  map f (Parser g) = Parser \s -> f $ g s        -- COMPILER ERROR!!
```

We still have a compiler error so let's look at it in detail:

```
import Data.Tuple (Tuple)
import Effect (Effect)
import Effect.Console (log)

type ParserState a = Tuple String a

class ParserError e

type ParserFunction a e = ParserError

data Parser e a = Parser (ParserFunction)

instance functorParser :: Functor (Parser e) where
  map :: ∀ a b. (a -> b) -> Parser e a -> Parser e b
  map f (Parser g) = Parser \s -> f $ g s

Could not match type

Either e1 (Tuple String a0)

with type

a0

while checking that type Either e1 (Tuple String a0)
  is at least as general as type a0
while checking that expression g s
  has type a0
in value declaration functorParser
```

We can see that g s is the problem since it's underlined.

We can also see that we have a type mismatch, Either e1 (Tuple String a0) with a0.

This is because f wants an a or a0 as the compiler calls it and we've given f an Either e1 (Tuple String a0), which is what g s returns.

So, f wants to operate on a0 here but a0 is buried inside first an Either and then a Tuple. So it looks like we're going to have to do some fancy mapping to get f to make 2 hops.

But that may be a bit difficult to do in one fell swoop. So go ahead and add map f into g s and see what new compiler error you get before reading on.

To map f over g s, we simply change $ to <$> :

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

```
map f (g s)
```

Okay, now let’s add another map:

```
map map f (g s)    -- COMPILER ERROR!!
```

Clearly, we need to some Parentheses, but where? We can randomly just start putting in Parentheses until we make the compiler happy, but this is just flailing and may work as a strategy in this simple case, but it’s really a terrible general strategy.

Instead of flailing, let reason it out. Looking at the FIRST map, we know it wants a Function as it’s first Parameter. But of what Type?

Looking at the Type Signature:

```
map :: ∀ a b. (a -> b) -> f a -> f b
```

So the Function map wants as it’s first Parameter is of a -> b, but we’ve passed it ANOTHER map which isn’t a Function of 2 Parameters.

With only 1 map, it was happy when we passed f because it’s a Function of 2 Parameters. So do we have a Function of 2 Parameters other than f?

Yes we do. It’s map f. Here’s its Type Signature:

```
map f :: ∀ a b. f a -> f b
```

So, this should be the FIRST Parameter to the FIRST map. Go ahead and add the Parentheses to make map f the first Parameter before reading on.

Here’s the change:

```
instance functorParser :: Functor (Parser e) where
  map :: ∀ a b. (a -> b) -> Parser e a -> Parser e b
  map f (Parser g) = Parser \s -> map (map f) (g s)
```

> We’re mapping map f over g s, which once it’s inside of the Either maps f over the Tuple.

This compiles.

Now I’m not a fan of this syntax since it has too many maps for my taste. So I’m going to change the first map to (<$>) in Prefixed Notation first:

```
instance functorParser :: Functor (Parser e) where
  map :: ∀ a b. (a -> b) -> Parser e a -> Parser e b
  map f (Parser g) = Parser \s -> (<$>) (map f) (g s)
```

And now I'm going to rewrite it in Infixed Notation:

```
instance functorParser :: Functor (Parser e) where
  map :: ∀ a b. (a -> b) -> Parser e a -> Parser e b
  map f (Parser g) = Parser \s -> map f <$> g s ①
```

① Once again, we're mapping map f over g s, which once it's inside of the Either maps f over the Tuple.

This syntax is my personal favorite and you'll probably find this style more common. But if you like the previous way, feel free to use it.

Whew. That was some work. Maybe you'll want to take a break and continue after a good 20 or 30 minutes.

Hopefully, you've taken that break and are ready to work on Apply. Go ahead and write Apply or get as far as you can before reading more.

As usual, we'll write the Type Signature first:

```
instance applyParser :: Apply (Parser e) where ①
```

① Once again, we hold the e constant.

Next, we'll write the specialized Type Signature just to help us keep the Types straight in our heads. I usually delete this line when it compiles because it's not required:

```
instance applyParser :: Apply (Parser e) where
  apply :: ∀ a b. Parser e (a -> b) -> Parser e a -> Parser e b
```

If you got this far, you're doing great. If not, that's okay, simply type this code into your Module.

Next step, write the Function but only left-hand side of the equal sign before reading on.

Here's the Function's left-hand side:

```
instance applyParser :: Apply (Parser e) where
  apply :: ∀ a b. Parser e (a -> b) -> Parser e a -> Parser e b
  apply (Parser f) (Parser g) = ???
```
