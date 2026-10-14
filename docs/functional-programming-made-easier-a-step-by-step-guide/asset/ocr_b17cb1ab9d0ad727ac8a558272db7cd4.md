[info] Build succeeded.
placeholder

# 15.1. Writing the Predicate odd

Let’s revisit the concept of a Predicate. A Predicate is a function that takes a value and determines if it meets some predefined criteria and returns a Boolean. An example of that is even from Data.Int:

```
import Data.Int.Bits ((.&.)) ①

even :: Int -> Boolean
even x = x .&. 1 == 0 ②
```

① Import bit level AND operator.

② Mask the Least Significant bit and if it’s 0 then we have an even number.

If you’re not too good with Binary Arithmetic, here’s a quick primmer. Here is a table of numbers in both Decimal and their Binary Equivalent:

```
0 = 0000
1 = 0001
2 = 0010
3 = 0011
4 = 0100
5 = 0101
6 = 0110
7 = 0111
```

Notice that all odd numbers have a 1 in the Least Significant position, i.e. the rightmost bit. Also remember that an AND operation is only true, or, in the Binary world, equal to 1, when both values are true:

```
0 .&. 0 = 0
0 .&. 1 = 0
1 .&. 0 = 0
1 .&. 1 = 1
```

With that Truth Table in mind, here are a few numbers ANDed with 1 to see what’s going on inside the function even: