```
```purescript
delete
  :: ∀ proxy r1 r2 l a
  . IsSymbol l
  => Lacks l r1
  => Cons l a r1 r2
  => proxy l
  -> Record r2
  -> Record r1
```
```

> These Constraints are built into the compiler.

To understand this, first look at `proxy`’s Type Parameter `l`, which stand for the `label` in Row `r2` that we’re going to delete. It has an `IsSymbol` constraint, which means it must be a Literal String. You cannot use a Variable of Type `String` here.

The next 2 Constraints is where the Type-level magic happens.

First is `Lacks l r1`. This Constraint says that Row `r1`, which is the Row of the returned Record, must not contain the `Symbol`, `l`. This make sense since `delete` is supposed to remove that field and `Record r1` is returned. Remember, we can construct Records from Rows using the Data Constructor `Record`.

Second is `Cons l a r1 r2`. The `l` is our `Symbol` and represents a Label. The `a` is a Type and represents the Label’s Type. Remember that Rows consists of Pairs of Labels and their corresponding Types:

```
```purescript
type SomeRow = ( someLabel :: String, someOtherLable :: Int )
```
```

So, `Cons` is a Constraint that will make sure that Row `r1`, i.e. the labels after the deletion, cons’d with the Label, `l`, of Type `a` is equal to the Row, `r2`, i.e. the labels that we started with.

In other words, `Lacks` makes sure that the final returned Row, `r1`, doesn’t already have the label we’re going to delete and `Cons` makes sure that the only difference between the Rows `r1` and `r2` is that one label.

All this checking is done at the Type level, which is why it’s Type Safe and why `writeBody__` fails to compile.

If you look at the implementation of `delete`, it simply calls Javascript to delete a field from a Javascript Object, which is the underlying representation of PureScript Records. This can be safely done because it’s already been Type Checked by the compiler, so we know the key must be in the Object before Javascript tries to `delete` it.

For now, modify you `loggingRouter` to look like: