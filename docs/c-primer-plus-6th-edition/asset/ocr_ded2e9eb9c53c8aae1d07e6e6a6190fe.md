# Reference Variables

accumulate(dup,five); // add five's data to dup
dup = four; // overwrite the contents of dup with the contents of four

The second statement wipes the work accomplished by the first, so the original
assignment statement was not a good use of accumulate().

# Why Return a Reference?

Let's look a bit further at why returning a reference is different from the traditional return
mechanism. The latter works like passing by value does function parameters.
The expression following the return is evaluated, and value is passed back to the call-
ing function. Conceptually, this value is copied to a temporary location and the calling
program uses the value. Consider the following:

```
double m = sqrt(16.0);
cout = sqrt(25.0);
```

In the first statement, the value 4.0 is copied to a temporary location and the value
in that location is copied to m. In the second statement, the value 5.0 is copied to a tempo-
tary location, then the contents of that location are passed on out. (This is the concept-
tual description. In practice, an optimizing compiler might consolidate some of the steps).
Now consider this statement:

```
dup = accumulate(team,five);
```

If accumulate() returns a structure instead of a reference to a structure, this could
involve copying the entire structure to a temporary location and then copying that copy
of dup. With a reference return value, team is copied directly to dup, a more efficient
approach.

+   A function that returns a reference is actually an alias for the referred-variable.

# Being Careful About What a Return Refers To

The single most important point to remember when returning a reference is to avoid
returning a reference to a memory location that ceases to exist when the function termi-
ates. What you want to avoid is code like these:

```
free_throws = clone2(free_throws & ft)
{
free_throws newguy; // first step to big error
guy = ft; // copy info
return newguy; // return reference to copy
}
```

This has the unfortunate effect of returning a reference to a temporary variable
(newguy) passes from existence as soon as the function terminates. (Chapter 9,"Mem-ory Models and Namespaces," discusses the persistence of various kinds of variables.) Similarly, you should avoid returning pointers to such temporary variables.