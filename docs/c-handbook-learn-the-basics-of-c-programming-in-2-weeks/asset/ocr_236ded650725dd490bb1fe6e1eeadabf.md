# *Tuples*

Tuples and lists are similar except for one thing: tuples cannot be edited. After creating a tuple, you won't be able to change it in any way. You can't expand, edit, or delete the elements within a tuple. If you'll ignore this immutability, you can say that lists and tuples are identical.

You should use commas when declaring tuples:

```
unchanging = "rocks", 0, "the universe"
```

Sometimes, you have to differentiate tuples using parentheses. This process is similar to performing several assignments using the same line. Here's a simple example:

```
foo, bar = "rocks", 0, "the universe" # 3 elements here
foo, bar = "rocks", (0, "the universe") # 2 elements here because the second element is a tuple
```