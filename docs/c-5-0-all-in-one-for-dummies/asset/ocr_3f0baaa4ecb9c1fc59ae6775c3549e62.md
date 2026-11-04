The decimal variable type has two significant limitations, however. First, a decimal is not considered a counting number because it may contain a fractional value. Consequently, you can't use them in flow-control loops, which I explain in Chapter 5 of this minibook.

The second problem with decimal variables is equally as serious or even more so. Computations involving decimal values are significantly slower than those involving either simple integer or floating-point values — and I do mean significant. On a crude benchmark test of 300,000,000 adds and subtracts, the operations involving decimal variables were approximately 50 times slower than those involving simple int variables. The relative computational speed gets even worse for more complex operations. Besides that, most computational functions, such as calculating sines or exponents, are not available for the decimal number type.

Clearly, the decimal variable type is most appropriate for applications such as banking, in which accuracy is extremely important but the number of calculations is relatively small.

# # Examining the bool Type: Is It Logical?

Finally, a logical variable type. Except in this case, I really mean a type "logical." The Boolean type bool can have two values: true or false. I kid thee not — a whole variable type for just two values. Not even a "maybe."

![](bbox=[0.153, 0.592, 0.224, 0.681])

Former C and C++ programmers are accustomed to using the int value 0 (zero) to mean false and nonzero to mean true. That doesn't work in C#.

You declare a bool variable this way:

```
```
bool thisIsABool = true;
```
```

No conversion path exists between bool variables and any other types. In other words, you can't convert a bool directly into something else. (Even if you could, you shouldn't because it doesn't make any sense.) In particular, you can't convert a bool into an int (such as false becoming 0) or a string (such as false becoming the word "false").

# # Checking Out Character Types

A program that can do nothing more than spit out numbers may be fine for mathematicians, accountants, insurance agents with their mortality figures, and folks calculating cannon-shell trajectories. (Don't laugh. The original computers were built to generate tables of cannon-shell trajectories to help