```
class IsRecord a where
  isRecord :: a -> Boolean

instance isRecordRecord :: IsRecord (Record a) where
  isRecord _ = true

instance isRecordOther :: IsRecord a where -- COMPILER ERROR
  isRecord _ = false
```

+   1. Here we have a Class whose `isRecord` Method returns `true` if it’s a `Record`.
+   2. This is `Record`'s instance for `IsRecord`.
+   3. What we’re trying to do here is write an instance for EVERY OTHER Type to have it return `false` since we’ve already handled the `Record` instance.

The compiler isn’t happy with this. Can you see why?

It may be clear to us what we’re trying to do here, and it works fine for every Type except for `Record`.

When the Type is `Record a`, it matches both instances. In the first instance, `Record a` unifies with `Record a`. In the second instance, `Record a` unifies with `a`. (Remember the `a` in `Record a` is different than `a` in `class IsRecord a`.)

What we need is a way to specify the first instance as a specific case and to specify the second as a Catch-All. And we can do exactly that with *Instance Chaining*.

```
class IsRecord a where
  isRecord :: a -> Boolean

instance isRecordRecord :: IsRecord (Record a) where
  isRecord _ = true
else instance isRecordOther :: IsRecord a where
  isRecord _ = false
```

The addition of the keyword `else` "Chains" these two instances together.

When using Instance Chaining, order matters. So if we were to swap the instance order the compiler will NOT complain. It just will NEVER use the second one since `a` will match all Types. This is the same issue we’ve seen with Pattern Matching.

# 6.10. Orphaned Instances

There are some restrictions on where we can define instances of Classes and for good reason, which will become apparent soon enough: