# Chapter 7

# Algorithms 91

# More products

Encouraged by consumer demand, the chocolatier decides to introduce a third and even more exclusive line of chocolates, called Pyramid Luxe. One box of those will bring in a profit of $13. Let $x_1, x_2, x_3$ denote the number of boxes of each chocolate produced daily, with $x_3$ referring to Luxe. The old constraints on $x_1$ and $x_2$ persist, although the labor restriction now extends to $x_3$ as well: the sum of all three variables can be at most 400. What's more, it turns out that Nuit and Luxe require the same packaging machinery, except that Luxe uses three times as much, which imposes another constraint $x_2 + 3x_3 \le 600$. What are the best possible levels of production?

Here is the updated linear program.

```
max x1 + 6x2 + 13x3
x1 <= 200
x2 <= 300
x1 + x2 + x3 <= 400
x2 + 3x3 <= 600
x1, x2, x3 >= 0
```

**Figure 7.2** The feasible polyhedron for a three-variable linear program.

![](bbox=[0.431, 0.497, 0.792, 0.883])