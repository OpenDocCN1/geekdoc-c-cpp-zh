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

# 8.11. Group Typeclass

In PureScript, Group is a Typeclass defined as:

```
class Monoid g <= Group g where ①
  ginverse :: g -> g ②
```

① Monoid is a Superclass of Group. Notice the backward fat arrow.