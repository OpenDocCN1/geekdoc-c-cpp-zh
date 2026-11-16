![](bbox=[0.07, 0.05, 0.32, 0.22])

# ## SMELLY CODE

One of the best ways to learn to write good code is to learn how to recognize bad code. Code that doesn't work is obviously bad, but there are other hallmarks. Most programmers call these Code Smells. There are lots of them (there's an infinite number of ways for anything to be not-quite-right), and every theorist seems to list them differently, but here are a few to get you started:

# ## RIGIDITY

If changing one piece of code requires changes to another piece, which might then require changes to a third piece, and..., the code is rigid. And smelly.

# ## FRAGILITY

Cynical programmers (that is, anybody who's done it for a living) say that there are always three bugs in any application: the one you know about, the one you don't know about, and the one you're going to create when you fix the one you know about. Fragile code breaks in unexpected ways, in areas that don't seem to be related to what you're working on.

# ## IMMOBILITY

A common situation: You're modifying an application, and you want to re-use a bit of code. But the snippet you need is so tightly entrenched that the only way to re-use it is to cut and paste. You're looking at code that's immobile. That's a smelly waste of time.

# ## REDUNDANCY

Immobile code is the primary cause of this design smell. When you're programming, some kinds of lazy are good. If there's any bit of code that appears in more than one place, you've got a smelly problem, because if the snippet needs to change (and it will), you need to change it everywhere. How do you spell "boring"?

# ## OPACITY

I really wish I had money for every time I've seen a comment like "Don't know how this works, but it does" in a release application. I don't need to tell you that this is unacceptable, right? If you don't understand it, how are you going to know how to change it? You should write code that makes comments seem unnecessary. (But comment everything anyway.) If you need the comment to understand the snippet, then your code is opaque, and opacity smells. Really, really badly.