![](bbox=[0.117, 0.085, 0.858, 0.495])

# FIGURE 1.6 Output from the arguments Script.

Let's look at what we did. We only made one small change, so the first and the last lines of the script are exactly the same. On the second line, we changed it to read MESSAGE="Wake up, "$1. For those new to arguments, this may seem a bit confusing (what in the world is $1?). Arguments in bash scripting have a very specific naming convention, as detailed in Table 1.1.

# Table 1.1
Argument Variables

| Argument | Behavior |
| $0 | The name of our script |
| $1 | The first argument |
| $2 | The second argument |
| $9 | The ninth argument |
| $# | The number of arguments we have |