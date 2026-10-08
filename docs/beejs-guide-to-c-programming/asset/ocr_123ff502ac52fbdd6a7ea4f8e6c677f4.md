# Chapter 23. Pointers add, Pointers to and More

```
print_math(add, 5, 7);   // 12
print_mult(mult, 5, 7);   // 35
}
```

Take a moment to digest. The idea here is that we're going to pass a pointer to a function
print_math(), and it's going to call that function some math.

This we can change the behavior of print_math() by passing another function into it. You can see
do that on lines 22-23 when we pass pointers to functions add and mult, respectively.

Now, on line 13, I think we can all agree the function signature of print_math() is a sight to behold. And,
if you can believe it, this one is actually pretty straight-forward to some things you can construct¹¹.

But let's digest it. Turns out there are only three parameters, but they're a little hard to see:

```
//                op        x    y
//      [---op---] |--| |--]
void print_math(*op)(int, int), int x, int y)
```

The first, op, is a pointer to a function that takes two as arguments and returns an int. This matches
signatures for both add() and mult().

The second, and x and y, are just standard int parameters.

Slowly and deliberately let your eyes over the signature while you identify the working parts. One thing
that always stands out for me is the sequence (*op)(, the parents and the asterisk. That's the giveaway it's a
pointer to a function.

Finally, jump back to the Pointers II chapter for a pointer-to-function example using the built-in qsort().

¹¹The Go Programming Language drew its type declaration syntax inspiration from the opposite of what C does.