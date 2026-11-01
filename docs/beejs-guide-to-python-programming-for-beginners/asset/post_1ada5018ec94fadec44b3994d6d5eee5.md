
```
round(2.5)  # 2
round(3.5)  # 4
```

You can also tell round() how many decimal places you want to round to:

```
round(3.1415926, 4)  # 3.1416
```

Note that Python has additional weird rounding behavior⁶ due to the limited precision of floating point numbers.

For always rounding up or down, use the functions ceil() and floor() from the math module.

ceil() returns the next integer greater than this number, and floor() returns the previous integer smaller than this number.

This makes perfect sense for positive numbers:

```
import math

math.ceil(2.1)  # 3
math.ceil(2.9)  # 3
math.ceil(3.0)  # 3
math.ceil(3.1)  # 4

math.floor(2.1)  # 2
math.floor(2.9)  # 2
math.floor(3.0)  # 3
math.floor(3.1)  # 3
```

But with negative numbers, it behaves differently than you might expect:

```
import math

round(2.3)      # 2
math.floor(2.3) # 2

round(-2.3)     # -2
math.floor(-2.3) # -3 (!!)

round(2.8)      # 3
math.ceil(2.8)  # 3

round(-2.8)     # -3
math.ceil(-2.8) # -2 (!!)
```

While round() heads to the nearest integer, floor() goes to the next smallest integer. With negative numbers, that's the next one farther away from zero. And the reverse is true for ceil().

If you want a round up function that works on positive and negative numbers, you could write a helper function like this:

```
import math

def round_up(x):
    return math.ceil(x) if x >= 0 else math.floor(x)

round_up(2.0)  # 2
round_up(2.1)  # 3
round_up(2.8)  # 3

round_up(-2.0)  # -2
round_up(-2.8)  # -3
```

I'll leave round_down() as an exercise. :)

```
round_up(-2.1)  # -3
round_up(-2.8)  # -3
```

If you want to always round up to the next whole number instead of doing banker's rounding, you can use this trick: add 0.5 to the number and then convert it to an int(). (If the number is negative, subtract 0.5 from it.)

```
int(0.5 + 0.5)  # 1
int(1.5 + 0.5)  # 2
int(2.5 + 0.5)  # 3

int(2.8 + 0.5)  # 3
int(2.2 + 0.5)  # 2

int(-2.2 - 0.5)  # -2
int(-2.8 - 0.5)  # -3
```

### 15.13 Large Numbers

Python is really good with large integer numbers. In fact, it has what we call *arbitrary precision integer math*. That means we can hold numbers as big as memory can handle, which is large.

So if you ask Python to compute 100000!, it will do it. The result, incidentally, is 465,575 digits long. No problem.

But the same is *not* true for floating point numbers (numbers with a decimal point). Python generally uses 64 bits to represent floating point numbers, which means there's a limit to the amount of precision—you can only have 16 digits in your number, though you can raise that number to huge positive or negative powers to get very large or very small numbers.

Floating point is brilliant because it can represent really huge and really small numbers, but the number of digits you have at your disposal is limited.

## Chapter 16: Appendix B: The REPL

### 16.1 What is the REPL?

The REPL, pronounced REP-al, is short for the Read-Evaluate-Print Loop.

Great. I mean, truly, that's awesome.

But what does any of that mean?!

Check this out. If you run Python on the command line (or whatever your OS's variant is), you'll end up with a prompt that looks like this:

```
$ python
Python 3.8.0 (default, Oct 23 2019, 18:51:26)
[GCC 9.2.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>>
```

And it just sits there, waiting for you to type something.

Actually, it's reading. The Read part of REPL.

So type something and hit RETURN!

```
>>> print("Hello, world!")
Hello, world!
```

What happened after you hit RETURN was that Python Evaluated your expression, and the Printed the result. And then it printed another >>> prompt, because it's doing this in a Loop! The REPL!

This is a method you could use to quickly test out Python commands to see how they work. It's not commonly used for development, but it is there if you find it convenient.

Any time you see the >>> prompt, it's waiting for another Python command.

```
>>> a = 20
>>> b = 30
>>> c = a + b
>>> print(c)
50
```

What about multi-line commands? Let's try printing numbers in a loop:

```
>>> for i in range(5):
...
```

Wait! What's that ... prompt? That means Python is waiting for more. The fact that the previous line ended in a : indicates that a block is to follow it. So Python is waiting for a properly-indented block. (Hit RETURN on a blank line to exit the block. If you get stuck in ... mode, just keep hitting RETURN until you get back out to the >>> prompt.)

```
| count(...)
|     S.count(sub[, start[, end]]) -> int
| 
|     Return the number of non-overlapping occurrences of substring sub in
|     string S[start:end]. Optional arguments start and end are
|     interpreted as in slice notation.
```

We see there's a description there of what the method does, as well as an important description of what each parameter to the function means. But let's look at this line in particular:

That's not Python. It's documentation, and it has its own way of being read.

Generally:

The S. refers to this string that we're operating on. For example, if I say:

the string "fee fie foe foo" is represented by S in the documentation.

The stuff after the -> indicates the type of the return value. This function returns an integer.

Now, what about that start and end stuff in the middle with the square brackets?

In documentation, square brackets indicate optional parameters to the function. Notice in my example, above, I didn't pass start or end... they're in square brackets, so they're optional.

Looking in more detail, you see the brackets are nested. This means you can make the call with a sub and a start... and then the end becomes optional. There's no way to call it with just a sub and an end, but no start. The optional end is optional if-and-only-if the optional start had already been specified.

Finally, you can ask for help on a specific function or method:

```
help("".count)  # Get help specifically on string.count method
```

### 16.4 dir()—Quick and Dirty Help

The dir() built-in function is like help(), except extraordinarily terse. It just returns a list of the methods on a particular thing.

For instance, we can get that list of methods and data attached to a dictionary by asking for dir({}) (or by passing any dict to dir()).

```
>>> dir({})
['__class__', '__contains__', '__delattr__', '__delitem__', '__dir__',
 '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__',
 '__getitem__', '__gt__', '__hash__', '__init__', '__init_subclass__',
 '__iter__', '__le__', '__len__', '__lt__', '__ne__', '__new__',
 '__reduce__', '__reduce_ex__', '__repr__', '__reversed__',
 '__setattr__', '__setitem__', '__sizeof__', '__str__',
 '__subclasshook__', 'clear', 'copy', 'fromkeys', 'get', 'items', 'keys',
 'pop', 'popitem', 'setdefault', 'update', 'values']
```

Not as good as help(), but it might get you the quick answer if you're like, "What do I call to get the values out of a dictionary, again? Oh, that's right. values()! Eureka!"

One place this is also useful is if you're using a poorly-documented piece of software¹. Asking for dir() on an object can give you insight on how to use it.

Though if you do this, beware that programmers change their undocumented interfaces all the time without telling people. There's a school of thought that says if something's undocumented, you shouldn't use it at all, lest it be silently changed or dropped some day in the distant future. And that school has a point.

### 16.5 Getting out of the REPL

Oh, sure, Beej, put this section at the end of the chapter. Well, I just wanted to make sure you read the middle bit. :)

Since the REPL is reading from the keyboard as a “file”, you should send an EOF (End Of File²) character to indicate that it should be done.

On Mac and Linux and BSD and Ultrix and MINIX and SunOS and IRIX and HP-UX and Solaris and GNU Hurd and Plan 9 From Bell Labs and any Unix variant, EOF is indicated from the keyboard with CTRL-d.

On Windows and Windows and Windows and Windows and any Windows variant and MS-DOS, EOF is indicated from the keyboard with CTRL-z. Followed by RETURN.

Additionally, on any system, you can type exit() at the >>> prompt and it'll quit out.
