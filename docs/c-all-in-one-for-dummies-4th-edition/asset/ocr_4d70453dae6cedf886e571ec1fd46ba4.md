anywhere in your code, as long as you don’t break a string or word in two by putting a comment in the middle. Much of the code in the remainder of this chapter has comments in it so that you can see how to use comments and so that you can get a few more ideas about how the code works.

![](bbox=[0.163, 0.174, 0.226, 0.242])

WARNING

Some beginning programmers get the mistaken idea that comments appear in the application window when the application runs. That is not the case. A comment does not write anything to the console. To write things to the console, use `cout`.

# Converting Types

Sometimes, you just don’t have the type of things you want. You might want to trade in your 2014 Ford Taurus for that brand-new Porsche. But, needless to say, unless you have plenty of money, that might be difficult.

But converting between different types in C++ — now, *that’s* a lot easier. For example, you may have a string variable called `digits`, and it holds the string "123". Further, you want to somehow get the numbers inside that string into an integer variable called `amount`. Thus, you want `amount` to hold the value 123; that is, you want to convert the string to a number.

# Understanding how int and string conversions work

In Listing 2-1, later in this chapter, you see how you can convert between numbers and strings. Book 1, Chapter 8 shows some sample code for converting a number to a string. This example employs that same technique along with a similar technique for converting a string back to a number.

Converting strings is an interesting concept in C++ because an outstanding feature lets you *write to* and *read from* a string just as you would to and from a console. For example, although you can write a number 12 out to a console by using code like this:

```
```cpp
cout << 12;
```
```

you can actually do the same thing with strings: You can write a number 12 to a string, as in

```
```cpp
mystring << 12;
```
```