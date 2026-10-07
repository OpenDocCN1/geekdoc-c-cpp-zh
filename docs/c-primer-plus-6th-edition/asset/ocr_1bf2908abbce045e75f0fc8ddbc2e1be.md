# Introducing for Loops

What's a full expression? It's an expression that's not a subexpression of a larger expression. Examples of full expressions include an expression portion of an expression statement and an expression that serves as a test condition for a while loop.

Sequence points help clarify when postfix incrementation takes place. Consider, for instance, the code:

```
while (guests++ < 10)
cout << guests << endl;
```

(The while loop, discussed later this chapter, works like a for loop that has just a test expression.) Sometimes C++ newcomers use “use the value, then increment it” means in this context, to increment guests after it's in the cout statement. However, the guests++ 10 is a full expression because it is a while loop condition, so the end of this expression is a sequence point.Therefore, C++ guarantees the side effect (incrementing guests) takes place before the program moves on to cout. Using the postfix form, however, guarantees that guests will be incremented after the comparison,

Now consider this statement:

```
y = (4 + x++) + (6 + x++);
```

The expression 4 + x++ is not a full expression, so C++ does not guarantee that x will be incremented immediately after the subexpression 4 + x++ is evaluated. Here the full expression is the entire assignment statement, and the semicolon marks the sequence point, so that C++ guarantees that x will have been incremented twice by the time the program moves to the following statement. C++ does not specify whether x is increment after each subexpression is evaluated or only after all expressions have been evaluated, which is why you should avoid statements of this kind.

C++11 documentation has dropped the term “sequence point” because the concept doesn't carry over when discussing multiple threads of execution. Instead, descriptions are framed in terms of sequencing, with some events being described as sequenced before other events. This descriptive approach isnt intended to change the rules; the goal is to provide language that can clearly handle multithreaded programming.

# Prefix Versus Postfix

Clearly, whether you use the prefix or postfix form makes a difference if it is used for some purpose, such as a function argument or assigning to a variable. But what if the value of an increment or decrement expression isn't used? For example, are

```
x++;
```

```
and
++x;
```

different from one another? Or are

```
for (n = lim; n > 0; --n)
```