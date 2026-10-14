This should display:

```
Compiling Main
[info] Build succeeded.
placeholder
```

Go ahead and model a Type or Type Alias called `ParserState` that contains both the parsed value of Type `a` and a `String`. Do this before reading on.

So, modeling this Type isn’t straightforward since there are lots of ways to do it. I’ll display a few:

```
type ParserState a = Tuple String a

data ParserState a = ParserState String a

newtype ParserState a = ParserState (Tuple String a)
```

While the `data` and `newtype` are proper types, I don’t see the need for anything more than a simple Type Alias, at least at this point. I may find that I’ll regret this decision, but for now, I think it’s good enough. It will let us leverage the code written for `Tuple`, eg. `Functor`, `Bifunctor`, `Applicative`, etc.

Notice that we have the Polymorphic Parameter, `a` second. That’s so we can have a leverage `Tuple`'s `Functor` Instance. Not sure if we’re going to need it, but there’s no skin off our noses at this point, so we might as well put it second.

So change your code to use the Type Alias:

```
import Data.Tuple (Tuple) ❶

type ParserState a = Tuple String a ❷
```

❶ We’ll need to import `Tuple`.

❷ We’ve placed the `a` Type Parameter second just in case we want to map over it someday.

Next, step in modeling our Parser is to model the error Type. There are 3 possibilities for modeling it. First, is to just make it a human readable `String` using a Type Alias:

```
type ParserError = String
```

The second approach is to make it computer readable using a Sum Type or a Coproduct: