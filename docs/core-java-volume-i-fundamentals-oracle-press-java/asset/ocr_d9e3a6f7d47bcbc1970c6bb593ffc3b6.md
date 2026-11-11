The `floorMod` method aims to solve a long-standing problem with integer remainders. Consider the expression `n % 2`. Everyone knows that this is 0 if n is even and 1 if n is odd. Except, of course, when n is odd and negative. Then it is -1. Why? When the first computers were built, someone had to make rules for how integer division and remainder should work for negative operands. Mathematicians had known the optimal (or “Euclidean”) rule for a few hundred years: always leave the remainder ≥ 0. But, rather than open a math textbook, those pioneers came up with rules that seemed reasonable but are actually inconvenient.

Consider this problem. You compute the position of the hour hand of a clock. An adjustment is applied, and you want to normalize to a number between 0 and 11. That is easy: `(position + adjustment) % 12`. But what if the adjustment is negative? Then you might get a negative number. So you have to introduce a branch, or use `((position + adjustment) % 12 + 12) % 12`. Either way, it is a hassle.

The `floorMod` method makes it easier: `floorMod(position + adjustment, 12)` always yields a value between 0 and 11. (Unfortunately, `floorMod` gives negative results for negative divisors, but that situation doesn’t often occur in practice.)

The `Math` class supplies the usual trigonometric functions:

```
```
Math.sin
Math.cos
Math.tan
Math.atan
Math.atan2
```
```

and the exponential function with its inverse, the natural logarithm, as well as the decimal logarithm:

```
```
Math.exp
Math.log
Math.log10
```
```