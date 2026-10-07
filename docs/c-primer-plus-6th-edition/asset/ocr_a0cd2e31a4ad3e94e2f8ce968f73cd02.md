quiz 11 is a 20
quiz 12 is a 20
quiz 13 is a 20
...

The first loop correctly halts after displaying the first five quiz scores. But the second starts by displaying the whole array. Worse than that, it says every value is 20.And still, it doesn't stop at the end of the array! And worst of all, the program can (although not necessarily) freeze other applications running at the time and require a computer reboot.
Things go wrong, of course, is with the following test expression:

```
quizscores[i] = 20
```

First, because it assigns a nonzero value to the array element, the expression is always nonzero, never always true. Second, because the expression assigns values to the array elements, actually changes the data. The test expression remains true, the program continues changing data beyond the end of the array. It keeps putting more and 20s into memory! This is not good.
The difficulty with this kind of error is that the code is syntactically correct, the compiler won't tag it as an error. (However, years of C and C++ programmers making this error actually led many compilers to issue a warning, asking if that's what you meant to do).

> Caution
Don't use = to compare equality; use ==.

Like C, C++ gives you freedom from most programming languages. This comes at the cost of requiring greater responsibility on your part. But with your good planning prevents a program from going beyond the bounds of a standard C++ array. However, with C++ classes, you can design a protected array type that prevents this sort of nonsense. Chapter 13,"Class Inheritance,"provides an example. For now, you should build the protection into your programs when you need it. For example, the loop in Listing5.10 should include a test that keeps it from going past the last member. That's true even for the "good" loop. If all the scores were 20s, the "good" loop, too, would exceed the array bounds. In short, the loop needs to test the values of the array and the array index. Chapter 6 shows how to use loop operators to combine two sets into one sin-condition.

# Comparing C-Style Strings

Suppose you want to see if string in a character array is the word mate. If word is the array name, the following test might not do what you think it should do:

```
word == "mate"
```

Remember that the name of an array is a synonym for its address. Similarly, a quoted string constant is a synonym for its address. Thus, the preceding relational expression