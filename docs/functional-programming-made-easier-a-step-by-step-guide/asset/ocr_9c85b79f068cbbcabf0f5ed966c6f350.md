# 12.2.2. Implicit Behavior

When we construct a Type, we are implicitly defining some of its behavior. In the case of Maybe, we have two possibilities, a Just a or Nothing. In the case of Nothing, there are no values to work with. So by definition, we must terminate (or Short-circuit) all future computations with this value.

We didn’t have to make a decision to short-circuit or not. the Data Structure imposed this on us. Short-circuiting was implicit in the definition of Nothing.

In the case of a Tree:

```
data Tree a = Leaf a | Node (Tree a) (Tree a)
```

we have a recursive definition. Any Data Constructor that doesn’t have Tree a as a Type Parameter will terminate our recursion, e.g. Leaf a. This behavior is implicit in the definition. With List, we have a very similar case:

```
data List a = Nil | Cons a (List a)
```

Here Nil is analogous to Leaf a with the notable difference of Nil short-circuiting any further computations since it contains no other values. In contrast, Leaf a contains an a, which means we can compute with that a and there is no Implicit short-circuit unless we Explicitly choose to do so.

# 12.2.3. Explicit Behavior

We have seen the explicit behavior of Short-circuiting in the code we wrote for Either:

```
f :: Number -> Either String Number
f x = case divide 83.0 x of
  Left reason -> Left reason ①
  Right result -> Right $ result * 10.0
```

① Explicit Short-circuit, i.e. we’re not required to short-circuit like with Nothing.

Unlike Maybe, this was a choice we made base on our Intent for Either. We could’ve decided to treat divide-by-zero as equal to 0:

```
f :: Number -> Number ①
f x = 10.0 * case divide 83.0 x of
  Left reason -> 0.0 ②
  Right result -> result
```