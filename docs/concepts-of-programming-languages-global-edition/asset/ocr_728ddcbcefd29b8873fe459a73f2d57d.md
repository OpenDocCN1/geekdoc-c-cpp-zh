Applying the assignment axiom to

```
y = y + 1 { y <= x }
```

we get {y + 1 <= x}, which is equivalent to {y < x}, which is implied by {y <= x and y <> x}. So, the earlier statement is proven.

Next, we must have

```
{I and (not B)} => Q
```

In our example, we have

```
{ (y <= x) and not (y <> x) } => {y = x}
{ (y <= x) and (y = x) } => {y = x}
{y = x} => {y = x}
```

So, this is obviously true. Next, loop termination must be considered. In this example, the question is whether the loop

```
{y <= x} while y <> x do y = y + 1 end {y = x}
```

terminates. Recalling that x and y are assumed to be integer variables, it is easy to see that this loop does terminate. The precondition guarantees that y initially is not larger than x. The loop body increments y with each iteration, until y is equal to x. No matter how much smaller y is than x initially, it will eventually become equal to x. So the loop will terminate. Because our choice of I satisfies all four criteria, it is a satisfactory loop invariant and loop precondition.

The previous process used to compute the invariant for a loop does not always produce an assertion that is the weakest precondition (although it does in the example).

As another example of finding a loop invariant using the approach used in mathematical induction, consider the following loop statement:

```
while s > 1 do s = s / 2 end {s = 1}
```

As before, we use the assignment axiom to try to find a loop invariant and a precondition for the loop. For zero iterations, the weakest precondition is {s = 1}. For one iteration, it is

```
wp(s = s / 2, {s = 1}) = {s / 2 = 1}, or {s = 2}
```

For two iterations, it is

```
wp(s = s / 2, {s = 2}) = {s / 2 = 2}, or {s = 4}
```

For three iterations, it is

```
wp(s = s / 2, {s = 4}) = {s / 2 = 4}, or {s = 8}
```

From these cases, we can see clearly that the invariant is

```
{s is a nonnegative power of 2}
```