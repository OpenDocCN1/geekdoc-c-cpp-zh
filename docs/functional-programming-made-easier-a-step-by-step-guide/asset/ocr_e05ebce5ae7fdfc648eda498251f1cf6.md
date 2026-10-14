① getAddress is the one and only Method of Typeclass HasAddress.

Please don’t conflate this with Object Oriented methods. While the words Class and Method are used, they have different meanings here.

There is a requirement for Typeclasses that may not be obvious at first blush.

Every Typeclass Method must have its Polymorphic Parameter in its Type Signature.

The reason for this is because calling getAddress isn’t enough information to determine which getAddress to call since many Types can be instances of HasAddress. The compiler needs a Type to determine which getAddress to call.

If we look back at our class, we can see that each Method (all 1 of them) requires an a as one of its Parameters:

```
class HasAddress a where
  getAddress :: a -> Address ①
```

① Requires a as the first Parameter. This information is sufficient for the compiler to determine which HasAddress instance to use.

Just for a moment, let’s imagine we didn’t have this restriction:

```
-- COMPILER ERROR!!
class HasAddress a where
  getAddress :: Address
```

Here is the exact error:

![](bbox=[0.17, 0.665, 0.83, 0.82])

The error specifies that there are "arguments" that cannot be determined, viz. a.

# 6.5. Built-in Typeclasses

In PureScript, there are many built-in Typeclasses. Most of the ones we’re going to look at have equivalent,