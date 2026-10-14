That means we have:

```
getAt :: ∀ a. Int -> List a -> Maybe a
getAt index list = ...
```

❶ ??? was replaced by `Maybe a` to account for the possibility of a failure.

❷ The details of the Function are not important here.

Here’s another one:

```
f :: ∀ a b. a -> Int -> (a -> b) -> List a -> b
```

This may seem pretty complex, but it’s actually not. It looks a lot like `getAt` but with the added Type `b` and the extra Parameter `a -> b`.

So this Function simply does what `getAt` does, but before it returns a Value, it converts it from Type `a` to `b` using the supplied conversion Function (3rd Parameter).

Here’s what this Function looks like:

```
getAtConvert :: ∀ a b. a -> Int -> (a -> b) -> List a -> b
getAtConvert def index convert list = ...
```

❶ The details of the Function are not important here.

But wait. I thought we couldn’t have a Function from `a -> b`. What gives?

While it’s true that we cannot write a Function from ANY `a` to ANY `b`, we could write a Function from `Int` to `String` and then call `getAtConvert` with it:

```
intToString :: Int -> String
intToString i = show i

getAtConvert (-1) 2 intToString (1 : 2 : 3 : Nil)
```

❶ Here our default value is `-1` and our index is `2`.

When we call this Function with `intToString`, our Type Parameter `a` gets unifies with `Int` and `b` gets unifies with `String`. Our `convert` Function’s Type is `a -> b` or, in this particular case, `Int -> String`. A Function from `Int` to `String` is a Function we can write.

We cannot have a free-standing Function with the Type Signature of `a -> b` since we cannot write code for converting ANY `a` to ANY `b`. But in this case, the caller of our Function can pick Concrete Types for `a` and `b`,