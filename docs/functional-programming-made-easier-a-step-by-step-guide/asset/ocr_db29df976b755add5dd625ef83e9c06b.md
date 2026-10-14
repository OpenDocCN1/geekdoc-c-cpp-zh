Here is a date from the past. We’ve all needed to parse a date before and we’re all too familiar with the Regular Expression to do so:

```
\d{1,2}\/\d{1,2}\/\d{4}
```

If you not familiar with Regular Expressions this will be confusing and appear to be gibberish. Even if you are, you have to think about it far too long and when I initially wrote this expression, I wrote it wrong. I forgot to escape the forward slash characters.

So we’d like to have something better than this, but parsing is parsing and the same issues arise in all parsers, which means we can use this example to help us think about ours.

Let’s look at this Regular Expression in detail:

```
\d{1,2}    -- digits 1 or 2
\\         -- forward slash (escaped since it's a special character)
\d{1,2}    -- digits 1 or 2
\\         -- forward slash (escaped since it's a special character)
\d{4}      -- digits 4
```

We have 3 unique "mini-parsers":

```
\d{1,2}    -- digits 1 or 2
\\         -- forward slash (escaped since it's a special character)
\d{4}      -- digits 4
```

In typical Functional fashion, it would be nice to build Parsers for each of these and then combine them somehow to finish the whole job. In Functional Programming, we combine Functions by composing them where the output of one Function is the input to another.

So if we’re going to combine Parsers to build larger Parsers, each Parser will need to whittle away at our String, doing their part, until we fail or success to parse.

That means that the Parsing State is going to need to be passed from Parser to Parser, i.e. when the current Parser is done, it passes what’s left of the String to the next Parser who takes a stab at parsing what’s left.

Also, if a single Parser in the chain were to fail, we want to short-circuit the parsing and return the error, hopefully with some useful information as to what went wrong.

# 17.9. Writing an Applicative Parser

Now that we have a Strategy for how to implement Parsers that can be combined to produce more complex