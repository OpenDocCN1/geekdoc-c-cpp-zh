of the Tuple.

Next, we add the z parameter (see the Javascript version of h):

```
h :: Int -> Tuple String Int
h z = ???
```

The next step calls f and captures both the computational result and the Side-effect:

```
h :: Int -> Tuple String Int
h z =
  let Tuple s r = f z
  ???
```

Here the computational Result is r and the Side-effect is s.

Next, we need to call g with the result of f, which is r. Then we’ll capture g’s result and Side-effect:

```
h :: Int -> Tuple String Int
h z =
  let Tuple s r = f z
      Tuple s' t = g r
  ???
```

We capture g’s computational Result in t and the Side-effect in s'.

And finally, we have to return the final computational Result and the overall Side-effect. The final computational result is easy. It’s just t.

But what’s the overall Side-effect?

Looking back out our Javascript implementation, we can see that when we call f, the log will first contain the String "added 10\n" and then when we call g, "multiplied by 100\n" will appended to it. We should do the same here by simply concatenating f’s Side-effect with g’s:

```
h :: Int -> Tuple String Int
h z =
  let Tuple s r = f z
      Tuple s' t = g r in
  Tuple (s <> s') t
```