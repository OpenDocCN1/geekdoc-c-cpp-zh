# If-Else-If

15–20 minutes

# Activity Overview

With a title should come a reward! And so we come to our last activity showcasing the tools of Twine. Now that there are three possible titles, else how about if the old woman gives the players a reward based on which they have?

# Instructions

To accomplish this, we're going to extend the conditional statement macro to include two new macros: else and else-if. These two new macros, along with the plain conditional, will let you create a chain of possibilities for things to happen in your game. The general format looks like this:

```
($variable is value)[hook a]
(else)[hook b]
```

This says something very simple, despite how complex it looks: if a variable has a particular value, then Twine will execute hook a; otherwise, it will execute hook b. Through everything you've done so far, you've seen that a hook can show text, display a link, or other actions. If that's not exciting enough for you, you can also have a more complex chain with several conditions based on the value of the variables.

```
($variable is value a)[hook a]
(else-if: $variable is value b)[hook b]
(else)[hook c]
```