Next, we use this new precondition as a postcondition on the middle state-
ment and compute its precondition, which is

```
{ y = B AND t = A }
```

Next, we use this new assertion as the postcondition on the first statement and apply the assignment axiom, which yields

```
{ y = B AND x = A }
```

which is the same as the precondition on the program, except for the order of operands on the AND operator. Because AND is a symmetric operator, our proof is complete.

The following example is a proof of correctness of a pseudocode program that computes the factorial function.

```
{n >= 0}
count = n;
fact = 1;
while count <> 0 do
    fact = fact * count;
    count = count - 1;
end
{fact = n!}
```

The method described earlier for finding the loop invariant does not work for the loop in this example. Some ingenuity is required here, which can be aided by a brief study of the code. The loop computes the factorial function in order of the last multiplication first; that is, (n - 1) * n is done first, assuming n is greater than 1. So, part of the invariant can be the following:

```
fact = (count + 1) * (count + 2) * . . . * (n - 1) * n
```

But we also must ensure that count is always nonnegative, which we can do by adding that to the assertion above, to get the following:

```
I = (fact = (count + 1) * . . . * n) AND (count >= 0)
```

Next, we must confirm that this I meets the requirements for invariants. Once again we let I also be used for P, so P clearly implies I. The next question is

```
{I and B} S {I}
```

I and B is the following:

```
((fact = (count + 1) * . . . * n) AND (count >= 0)) AND
    (count <> 0)
```