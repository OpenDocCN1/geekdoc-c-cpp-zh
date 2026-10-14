```
x :: Array (Maybe Int) -- t (m a)
sequence x :: Maybe (Array Int) -- m (t a)
```

In this case, if any of the Maybe’s in the Array are Nothing, then the result will be Nothing. Same goes for:

```
x :: Array (Either String Int) -- t (m a)
sequence x :: Either String (Array Int) -- m (t a)
```

If any of the Either’s in the Array are Left, then the result will be the FIRST Left.

But how does that work?

It works this way for Maybe and Either because of how their apply instances are coded to short-circuit in those cases. At this, point is not really clear how the code for <*> affects sequence or traverse.

But it will be once we write the Traversable Instance for List. It also will become clear to see why there’s an Applicative Constraint on m.

# 16.14. Traversable for List

Writing this instance is hard. If you look at the source code in the PureScript library for help, it won’t be very helpful. In fact here it is:

```
instance traversableList :: Traversable List where
  traverse f = map (foldl (flip (:)) Nil)
    <<< foldl (\acc -> lift2 (flip (:)) acc <<< f) (pure Nil) ①
  sequence = traverse identity
```

① lift2 is a helper function that lifts a Pure Function into an Applicative. It does a map and an apply internally. It can be imported from Control.Apply.

This is difficult to understand because it was written using foldl to take advantage of its Tail Recursive nature, which makes it efficient in space but not time since it takes 2 passes over the list.

It needs 2 passes since using foldl produces the List in the reverse order. The map (foldl (flip (:)) Nil) part is to reverse the List INSIDE the Applicative. This reverse step is the second pass over the List.

Instead we’re going to write ours using foldr, which will be time efficient but not space. But the real reason is because the foldr implementation is far simpler to understand.

The next area of difficulty is that traversable is too abstract. So, to help us think more clearly about this, we’re going to create a simple concrete example to strategize with.