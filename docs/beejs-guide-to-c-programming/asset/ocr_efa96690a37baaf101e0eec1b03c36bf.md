# Chapter 4. Functions

At first glance, it looks like i is 10, and we pass it to the function increment(). There the value gets incremented, when we print it, it must be 11, right?

> "Get used to disappointment."
—Dread Pirate Roberts, The Princess Bride

But it's not 11—it prints 10! 

It's all about that the expressions you pass to functions copied onto their corresponding parameters. The parameter is a copy, not the original.

So i is 10 out in main(). And we pass it to increment(). The corresponding parameter is called a in that function.

And the copy happens, as if by assignment. Loosely, a = i. So at that point, a is also 10. And out in main(), i is also 10.

Then we increment to 11. But we're not touching i at! It remains 10.

Finally, the function is complete. All local variables are discarded (bye, a!) and we return to main(), where i is still 10.

And we print it, 10, and we're done

This is why in the previous example with the plus_one() function, we returned the locally modified value so that we could see it in main().

Seems a bit restrictive, how? Like you can only get one piece of data back from a function, is what you're thinking. There is, however, another way to get data back; C folks call it it passing by reference and that's a story we'll tell another time.

But no fancy-schmancy name will distract you from the fact that EVERYTHING you pass to a function WITHOUT EXCEPTION is copied into its corresponding parameter, and the function operates on local copy, NO MATTER WHAT. Remember, even when we're talking about this so-called passing by reference.

# 4.2 Function Prototypes

If you recall back in the age a few sections ago, I mentioned that you you had to define the function before you used it, the compiler wouldn't know ahead of time, and would bomb out with an error.

This isn't quite strictly. You can notify the compiler in advance that you'll be using a function of a certain type that has a certain parameter list. That way function can be defined (even in a different file), as long as the function prototype has been declared before you can call that.

Fortunately, the function prototype is quite easy. It's merely a copy of the first line of the function definition with a semicolon attached to the end for good measure. For example, this code calls a function that defined later, because a prototype has been declared first:

```
#include <stdio.h>
```

```
int foo(void);    // This is the prototype!
```

```
int main(void)
{}
```

```
    int i;
```

```
// We can call foo() here before it's definition because the
// prototype has already been declared, above!
```

```
    i = foo();
```