# # Solutions to Chapter 8 | Recursion

**6.6** Implement the "paint fill" function that one see on many image editing programs. That is, given a screen (represented by a 2-dimensional array of Colors), a point, and a new color, fill in the surrounding area until you hit a border of that color.

# SOLUTION

First, let's visualize how this works. When we call Paint Fill (eg, "click" paint fill in the image editing application) on, say, a green pixel, we want to "bleed" outwards. Pixel by pixel, we expand outwards calling PaintFill on the surrounding pixel. When we hit a pixel that is not green, we stop. Returning green pixels may still be touched by another Paint Fill operation.

We can implement this algorithm recursively:

```
1 enum Color {
2 Black, White, Red, Yellow, Green
3 }
4 boolean PaintFill(Color[][][] screen, int x, int y, Color ocolor,
5 Color ocolor) {
6 if (x < 0 || x >= screen[].length ||
7 y < 0 || y >= screen.length) {
8 return false;
9 }
10 if (screen[y][x] == ocolor) {
11 PaintFill(screen, x - 1, y, ocolor, ncolor); // left
12 PaintFill(screen, x + 1, y, ocolor, ncolor); // right
13 PaintFill(screen, x, y - 1, ocolor, ncolor); // top
14 PaintFill(screen, x, y + 1, ocolor, ncolor); // bottom
15 }
16 }
17 return true;
18 }
20 boolean PaintFill(Color[][] screen, int x, int y, Color ncolor) {
21 return PaintFill(screen, x, y, screen[y][x], ncolor);
22 }
```

175 Cracking the Coding Interview | Concepts and Algorithms