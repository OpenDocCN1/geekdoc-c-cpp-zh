```
\h -> ??? :: (b -> Int) -> Int  -- function AFTER mapping
h :: (b -> Int)             -- 1st parameter to final function
g :: (a -> Int) -> Int       -- original function
```

We know we’re going to have to call g eventually. So let’s add that:

```
\h -> g ??? :: (b -> Int) -> Int  -- function AFTER mapping
h :: (b -> Int)             -- 1st parameter to final function
g :: (a -> Int) -> Int       -- original function
```

But we cannot just pass h directly to g since g wants an a -> Int but h is b -> Int.

We could, however, pass h to g if we could just change h to accept a’s instead of b’s. We can do this by composing h with a conversion function, f, like:

```
f :: a -> b
h <<< f :: a -> Int
```

Here we’re going to convert the a we’re given to a b so that it can be passed to h. Now, it should be pretty clear that f is the mapping function from Functor. We can see that by just looking at f’s Type Signature.

Let’s add these to the mix:

```
\h -> g ??? :: (b -> Int) -> Int  -- function AFTER mapping
h :: b -> Int                 -- 1st parameter to final function
g :: (a -> Int) -> Int        -- original function
f :: a -> b                   -- Functor mapping function
h <<< f :: a -> Int            -- a function that g will accept
```

Notice that h <<< f is EXACTLY what g needs. And now we can replace the ??? in our final function with that:

```
\h -> g (h <<< f) :: (b -> Int) -> Int  -- function AFTER mapping
h :: b -> Int                 -- 1st param to final function
g :: (a -> Int) -> Int        -- original function
f :: a -> b                   -- Functor mapping function
h <<< f :: a -> Int            -- a function that g will accept
```

The mapping function’s Type Signature, a -> b, informs us that we need to create a Functor Instance: