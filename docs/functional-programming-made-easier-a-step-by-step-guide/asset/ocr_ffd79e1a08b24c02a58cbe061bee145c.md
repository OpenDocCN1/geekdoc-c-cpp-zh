In these kinds of programming languages, x represents a placeholder in memory where numbers can be stored. We look to the right side of the equation first and evaluate it much like we would in Math and then we take the result of that evaluation and place it into a memory location named x.

In Functional Programming, there are no Variables. We still call them Variables like we did in Math but they don't vary like we are used to in Programming. Our thinking has to go back to middle school where we learned Algebra.

Remembering our Algebra word problems:

```
Mrs. Johnson has 20 students in her class. 12 of the students have brown hair, 3 have red and the rest have blonde. How many students have blonde hair?
```

Our fist step in solving this is to define our "Variables". So we'd write down the following:

```
Let s = number of students
Let b = students with brown hair
Let r = students with red hair
Let y = students with blonde hair
```

Then we'd write our formula:

```
y = s - b - r
```

To do this in PureScript, we write something very similar:

```
let s = 20      -- number of students
  b = 12      -- students with brown hair
  r = 3       -- students with red hair
  y = s - b - r -- students with blonde hair
```

Just like in Math, the variable s stands for number of students. The number of students doesn't change in the middle of our problem. It's always 20. In Math and in Functional Programming s is immutable.

So how did we solve for y in Math?

We substituted:

```
y = s - b - r
  = 20 - 12 - 3
```