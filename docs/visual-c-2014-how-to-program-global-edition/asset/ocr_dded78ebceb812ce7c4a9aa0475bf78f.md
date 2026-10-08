# Answers to Self-Review Exercises

+   8.1 a) arrays; variables, type c) foreach. d) two-dimension-
alf) f) foreach (doubled in numbers). g) an array of strings, usually called args. h) args.length; i test. j) params modifier. k getter-only.

8.2 The answers to Self-Review Exercise 8.2 are:

+   a) False. An array can store values of the same type.
b) False. Array index must be an integer or an index.
c) For individual value-type elements of an array False. A called method receives and ma-
ipulates a copy of the value of such element, modifications do not affect the orig-\inal value. If the reference of an array is passed to a method, modifications to
t array elements in the called method are indeed reflected in the original.
individual elements of an array type: True. A called method receives a copy of thenreference of such element, and changes to the referenced object will be reflected in
the original element.
d) False. Command-line arguments are separated by whitespace.
e) As of C# 6, you can use-property initialization in auto-implemented prop-\erty declarations.

8.3 The answers to Self-Review Exercise 8.3 are:

```
var total = 0.0;
foreach (var element in fractions)
{
    total += element;
}
```

8.4 The answers to Self-Review Exercise 8.4 are:

+   a) var table = new int[ArraySize, ArraySize]
b) Nine.
c) for (var x = 0; x < table.GetLength(0)); ++x
{
    for (var y = 0; y < table.GetLength(1); ++y)
{
    table[x, y] = x + y;
}

8.5 The answers to Self-Review Exercise 8.5 are:

+   a) Error: Assigning a value to a constant after it's been initialized.
Correction: Assign the correct value to the const declaration.
b) Error: Referencing an array element outside the bounds of the array (b[10]).
Correction: Change the << operator to <.