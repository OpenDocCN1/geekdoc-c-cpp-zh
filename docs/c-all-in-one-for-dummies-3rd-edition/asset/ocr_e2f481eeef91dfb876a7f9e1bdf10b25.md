# # Characters

Another type of variable you can have is a character variable. A *character variable* can hold a single — just one — character. It holds a value between –127 and 128 or between 0 and 255. Normally, a *character* is anything that can be typed, such as a letter of the alphabet, a digit, or another symbol you see on the computer keyboard, but a character can also hold nonprintable values.

To use a character variable, you use the type name `char`. To initialize a character variable, you put the character inside *single* quotes. (If you use double quotes, the compiler issues an error message.) The following is an example of a character:

```
```
char ch;
ch = 'a';
cout << ch << endl;
```
```

The character variable here is called `ch`. We initialized it to the character `a`, which, you notice, is surrounded by single quotes. We then printed it by using `cout`.

# ## Null character

One important character in the programming world is the *null* character. Deep down inside the computer’s memory, the computer stores each character by using a number, and the null character’s number is 0. There’s nothing to actually see with the null character; we can’t draw a picture of it in this book for you to hang on your wall. (Bummer.) All we can do is describe it. Yes, ever once in a while, computer people have to become philosophers. But the null character is important because it is often used to signify the end of something — not the end of the world or anything big like that, but the end of some data.

To notate the null character in C++, use `\0`, as in

```
```
char mychar = '\0';
```
```

# ## Nonprintable and other cool characters

In addition to the null character, several other cool characters are available — some that have a look to them and can be printed and some that do not and cannot. The null character is an example of a *nonprintable* character. You can try to print one, but you get either a blank space or nothing at all, depending on the compiler.

But some characters are special in that they do something when you print, though you can’t type them directly. One example is the newline character.