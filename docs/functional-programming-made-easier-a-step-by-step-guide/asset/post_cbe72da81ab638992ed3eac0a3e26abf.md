
```
M = { 0, 1, 2, 3, ...} and • = +, e = 0
```

Now let's add the Group requirement, i.e. Unique Inverses for all elements of the set:

```
G = { ..., -3, -2, -1, 0, 1, 2, 3, ...} and • = +, e = 0
```

Notice that the Empty Element, e, is its OWN Inverse and it's Unique since it's not an Inverse for any other element in the Set.

If we take e and apply to e we get e. So it acts as an Identity to all elements but also as an Inverse for itself. It also acts like Identity for itself.

Note that Inverses, a', take any element, a, and when applied with the Binary Operator map them to the Identity element, e, i.e. a' • a = e.

Here's another example of a Group:

```
G = { ..., 1/3, 1/2, 1, 2, 3, ...} and • = *, e = 1
```

Again, 1 is it's own Inverse, i.e. 1 * 1 = 1 and it's an Identity for every element, e.g. 1/3 * 1 = 1/3 including itself, 1 * 1 = 1.

An example of NOT a Group:

```
X = { ..., -3, -2, -1, 0, 1, 2, 3, ...} and • = -, e = 0
```

Subtraction fails us again due to the fact that it's NOT Associative:

```
(-3) - 3 /= 0
  3 - (-3) /= 0
```

## 8.11. Group Typeclass

In PureScript, Group is a Typeclass defined as:

```
class Monoid g <= Group g where ①
  ginverse :: g -> g ②
```

① Monoid is a Superclass of Group. Notice the backward fat arrow.

② `ginverse` returns the Inverse of the value it's given.

Notice how `ginverse` takes a g and returns a g. That's because Inverses are part of the same Set which in programming is the same Type.

## 8.12. Modular Arithmetic and Groups

Imagine you have a clock with 4 positions instead of 12. This clock starts with 0 instead of 1:

![](img/8c0e9b687c62642e828ccb5481e11313_327_0.png)

Let's start at position 3 and add 3 by going Clockwise 3 positions, i.e. from 3 to 0 to 1 to 2:

![](img/8c0e9b687c62642e828ccb5481e11313_327_1.png)

This kind of Arithmetic is also known as *Modular Arithmetic*.

Next, imagine we start at 2 and add 3. Once again we move Clockwise 3 positions and wind up at 1:

![](img/8c0e9b687c62642e828ccb5481e11313_328_0.png)

This clock represents the Integers Mod 4. Mod is short for Modulo.

Symbolically, it’s displayed as ℤ₄ which is the following Set, { 0, 1, 2, 3 }. Notice that these are same the numbers on our clock face.

But what about Subtraction? Can we subtract?

Actually, we can by going Counterclockwise. But, since we’re interested in Modular Arithmetic in the context of Groups and a Group only has 1 Binary Operator, let’s look at how we can get the same result as Subtraction using Addition instead.

In Math, we learned that Subtracting is like adding the Inverse or Negative number, e.g.:

```
10 - 3 = 10 + (-3)
```

Here -3 is the Inverse of 3. In Modular Arithmetic, we also have Inverses, but they aren’t negatives.

Remember, in the definition of a Group, every element in our Set has an Inverse such that:

```
a • a' = a' • a = e
```

where a' is the Inverse of a.

In regular Arithmetic, this is just a and -a. But this is not the case for Modular Arithmetic.

We can consult our clock to help us see why this is true:

![](img/8c0e9b687c62642e828ccb5481e11313_329_0.png)

Notice how Subtracting 1 is the same as Adding 3. That makes 3 the Inverse of 1 and vice versa. Here are the Inverses:

| a | a' |
|---|---|
| 0 | 0 |
| 1 | 3 |
| 2 | 2 |
| 3 | 1 |

Since our Binary Operator is +, adding a and a' always results in 0, which is the definition of Inverse that we saw in the Group requirement:

| a | a' | a • a' |
|---|---|---|
| 0 | 0 | 0 + 0 = 0 |
| 1 | 3 | 1 + 3 = 0 |
| 2 | 2 | 2 + 2 = 0 |
| 3 | 1 | 3 + 1 = 0 |

(If the above table doesn’t make sense, try each of these cases using our clock.)

We’ve shown that Integers Mod 4, ℤ₄, with a Binary Operator of + meets the unique requirement for a Group. But we need to make sure it’s Monoid.

To be a Monoid, we need an Identity Element. That would be 0. Apply it with our Binary Operator to any element of our set and we get back that element.

```
type ConstrainAbelian a b = Abelian a b
```

That’s a much better name since it reminds us that the `Abelian` Type Alias gives us a way to easily constrain a to be an Abelian Group, i.e. a must be a `Group` and `Commutative`. But what exactly is `Commutative`?

`Commutative` is a Typeclass:

```
class Semigroup a <= Commutative a
```

`Commutative` is just a `Semigroup` with the following implied law:

```
∀ x, y ⇒ x <> y = y <> x    [Commutative]
```

In PureScript, we cannot enforce the Commutativity of the `<>` operator, so the best we can do is just define it as such.

To get a better feel for how this Type Alias can be used, let’s look at a simple example:

```
find :: ∀ a. Abelian a (Set a -> Maybe a) ❶
```

> ❶ The b in the Alias Definition is the Function’s FULL Type Signature, i.e. `(Set a -> Maybe a)`.

This expands to:

```
find :: ∀ a. Group a => Commutative a => Set a -> Maybe a
```

So the `Abelian` Type Alias is just a HELPER for adding the necessary constraints to a function’s Type Signature, viz. `Group a => Commutative a =>`.

## 8.15. Arithmetic Operators in PureScript

Arithmetic Operators use unfamiliar types in PureScript. In Haskell, the Type is `Num`. Not scary at all.

To see these types, run the PureScript REPL with the following command:

```
npx spago repl
```

And then type `:t (+)` to determine the Type Signature for Addition:

```
```purescript
> :t (+)
forall a. Semiring a => a -> a -> a
```
```

The only part of the Type Signature that is baffling is the `Semiring` Constraint. The `a -> a -> a` makes sense. In fact, it implies that `+` is Closed for the Set of Inhabitants of Type `a`. So `Semiring` is at least a Magma.

Next, let’s try to see what Multiplication’s Type Signature is:

```
```purescript
> :t (*)
forall a. Semiring a => a -> a -> a
```
```

It also has a `Semiring` Constraint.

And what about Subtraction:

```
```purescript
> :t (-)
forall a. Ring a => a -> a -> a
```
```

That was unexpected. It’s got a `Ring` Constraint, whatever that is.

And finally, Division:

```
```purescript
> :t (/)
forall a. EuclideanRing a => a -> a -> a
```
```

Once again, this Constraint is quite the surprise.

So we have:

```
```text
Semiring
Ring
EuclideanRing
```
```

Who would’ve thought simple Arithmetic Operations that we learned in Grade School would be so complicated.

It turns out that in PureScript, Arithmetic Operators are defined using these Abstract Algebraic Structures. The benefit of doing this is that these Operators can be used for non-numeric things giving us the full power of these abstractions.

## 8.17. Semiring Typeclass

In PureScript, Semiring is a Typeclass defined as:

```
class Semiring a where
    add :: a -> a -> a
    zero :: a
    mul :: a -> a -> a
    one :: a

infixl 6 add as +
infixl 7 mul as *
```

① Order of operations makes * higher Precedence than + as is common in Arithmetic with Numbers.

We can see from the Type Signature of add and mul that they are Closed operations since they take 2 a’s and return an a. And there exists an Identity, zero, to be used with add and another Identity, one, to be used with mul.

The archetypical implementation is for Int:

```
instance semiringInt :: Semiring Int where
    add = intAdd
    zero = 0
    mul = intMul
    one = 1

foreign import intAdd :: Int -> Int -> Int
foreign import intMul :: Int -> Int -> Int
```

① Actual implementations are in Javascript.

Here’s the trivial implementation for Unit:

```
instance semiringUnit :: Semiring Unit where
    add _ _ = unit
    zero = unit
    mul _ _ = unit
    one = unit
```

Since Unit has a single inhabitant, unit, it’s the only solution to the add and mul operations. So we just ignore the Input Parameters.

And since **zero** and **one** must be an element of the Set, we use the only Inhabitant we have, **unit**, in both cases.

## 8.18. Semiring for Functions

One of the benefits of using Abstractions for simple Arithmetic is that you can generalize Numbers to things that behave similarly. For example, Functions.

You might not immediately think to replace Numbers with Functions, but it actually can be done. Here’s the **Semiring** instance for Functions:

```
instance semiringFn :: Semiring b => Semiring (a -> b) where
  add f g x = f x + g x
  zero = \_ -> zero
  mul f g x = f x * g x
  one = \_ -> one
```

This is a bit complicated and confusing so let’s break down each line one at a time.

```
instance semiringFn :: Semiring b => Semiring (a -> b) where
```

This instance is for Functions of Type **a -> b**, where **b** is also a **Semiring**. This will prove to be important once we look at **add** and **mul**.

But looking at this, we may ask, what about functions of multiple Parameters. Well, remember, thanks to Currying, all functions technically only have 1 Parameter. They instead return a function to support multiple Parameters. So **b** here COULD be a function.

We can best see this by replacing **b** with **(b -> (c -> d))**. We can see, once again, how functions of multiple Parameters are equivalent to a function that returns another function and so on until we’ve exhausted all of the Parameters.

And since functions of multiple Parameters are just functions that take 1 Parameter and return a function, that function fulfills the **Semiring b** Constraint.

Let’s look at the next line:

```
instance semiringFn :: Semiring b => Semiring (a -> b) where
  add f g x = f x + g x
```

The **add** function seems a bit strange when we consider its Type Signature:
