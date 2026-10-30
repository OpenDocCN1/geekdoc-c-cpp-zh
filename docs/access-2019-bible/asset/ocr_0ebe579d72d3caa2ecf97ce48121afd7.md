# **FIGURE 24.4**

A long statement extends beyond the code window.

![](bbox=[0.168, 0.174, 0.868, 0.523])

The underscore is typically referred to as the line continuation character, but the space that comes before it is equally important. You need both characters, space and underscore, to continue a line. The line continuation character can't be used in the middle of a string. Notice in the preceding example that the long string is broken up into four smaller strings and concatenated together with ampersands. To spread a long string over multiple lines, it must be broken up so that the line continuation character can be used.

# Multi-statement lines

Another way to improve the readability of your code is by putting two or more statements on one line. VBA uses the colon to separate statements on the same line. If you have a lot of short statements that are taking up a lot of vertical space in the code pane, you can put a few of them on the same line to clean up the code. In the following example, many similar statements are grouped together:

```
i = 12: j = 45: k = 32
l = 87: m = 77: n = 2
o = 89: p = 64: q = 52
```

Those nine statements are assigning numbers to nine different variables. If they were written out one after the other, they would eat up a lot of the code window. By putting three statements on each line, less space is wasted. This technique is useful when you have small