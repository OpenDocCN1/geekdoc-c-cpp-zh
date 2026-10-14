This coding Chapter is going to differ from earlier ones. You’re going to code like all the exercise Chapters, but sometimes we’ll code together when the going gets rough.

# 17.1. Writing `Applicative` Instance for `Maybe`

Create the `Maybe` Type from scratch providing all of the prerequisites for Applicative:

+   - Define the Type
+   - Create a `Show` Instance using `genericShow` (for our test code)
+   - Create a `Functor` Instance
+   - Create an `Apply` Instance
+   - Create an `Applicative` Instance

We’ve already done some of this before, but do yourself a favor and don’t look back at your old code. Write this from scratch for practice. The more times you write this the better.

Here’s the test code that you can now replace the placeholder test code with:

```
log $ show $ (+) <$> Just 21 <*> Just 21 ❶
log $ show $ (*) <$> pure 2 <*> (pure 21 :: Maybe Int) ❷ ❸
log $ show $ pure (+) <*> Just 17 <*> Just 25 ❹
```

+   ❶ Prints `(Just 42)`.
+   
+   ❷ Prints `(Just 42)`.
+   
+   ❸ The compiler has no way to know which `pure` we’re using here. So we let it know by telling it that one of the `pure` calls is a `Maybe`. It’ll be able to figure out the other from that.
+   
+   ❹ Prints `(Just 42)`.

So go ahead and write the code using the above 5-step plan before reading on.

# 17.2. Code for `Applicative` Instance for `Maybe`

We start out by creating the Type:

```
data Maybe a = Nothing | Just a
```

Then deriving `Generic` so we can use `genericShow`: