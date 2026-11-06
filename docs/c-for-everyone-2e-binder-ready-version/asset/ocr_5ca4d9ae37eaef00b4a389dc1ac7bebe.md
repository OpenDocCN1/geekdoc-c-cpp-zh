# # 2.4 Problem Solving: First Do It By Hand

A very important step for developing an algorithm is to first carry out the computations *by hand*. If you can’t compute a solution yourself, it’s unlikely that you’ll be able to write a program that automates the computation.

To illustrate the use of hand calculations, consider the following problem. A row of black and white tiles needs to be placed along a wall. For aesthetic reasons, the architect has specified that the first and last tile shall be black. Your task is to compute the number of tiles needed and the gap at each end, given the space available and the width of each tile.

![](bbox=[0.41, 0.289, 0.73, 0.382])

To make the problem more concrete, let’s assume the following dimensions:

+   - Total width: 100 inches
+   - Tile width: 5 inches

Pick concrete values for a typical situation to use in a hand calculation.

The obvious solution would be to fill the space with 20 tiles, but that would not work—the last tile would be white.

Instead, look at the problem this way: The first tile must always be black, and then we add some number of white/black pairs:

![](bbox=[0.43, 0.578, 0.71, 0.611])

The first tile takes up 5 inches, leaving 95 inches to be covered by pairs. Each pair is 10 inches wide. Therefore the number of pairs is 95 / 10 = 9.5. However, we need to discard the fractional part since we can’t have fractions of tile pairs.

Therefore, we will use 9 tile pairs or 18 tiles, together with the initial black tile. Altogether, we require 19 tiles.

The tiles span 19 × 5 = 95 inches, leaving a total gap of 100 − 19 × 5 = 5 inches. The gap should be evenly distributed at both ends. At each end, the gap is (100 − 19 × 5) / 2 = 2.5 inches.

This computation gives us enough information to devise an algorithm with arbitrary values for the total width and tile width.

```
```
number of pairs = integer part of (total width - tile width) / (2 x tile width)
number of tiles = 1 + 2 x number of pairs
gap at each end = (total width - number of tiles x tile width) / 2
```
```

As you can see, doing a hand calculation gives enough insight into the problem that it becomes easy to develop an algorithm.