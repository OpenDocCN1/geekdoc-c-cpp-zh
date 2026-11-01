```
s = 'Bears, beets, Battlestar Galactica'

x = s.find('beets')

print(x)  # 7, because that's the index 'beets' starts at in the string
```

The return value there of 7 is "good" data. We asked for a thing and we got it. But what if something goes wrong?

```
s = 'Bears, beets, Battlestar Galactica'

x = s.find('Dwight')

print(x)  # -1, because the substring isn't found
```

-1 here is the sentinel value we're looking for to tell us if there's an error.

We can make decisions on it. This is what I'd call "classic" error handling. This is the way people used to handle errors when Stonehenge was built. And, like Stonehenge, this method of handling errors is still in use to this day. If it ain't broke, don't fix it.

OK, yes, I admit Stonehenge is broke. Allow me my analogy!

```
s = 'Bears, beets, Battlestar Galactica'

x = s.find(substring)

if x == -1:
    print(f"Couldn't find {substring}")
else:
    print(f"Found {substring} at index {x}")
```

There! We successfully handled an error the classic way.

But now let's learn another way.

# 14.5 Error Handling with Exceptions

Problem-solving step: Understanding the Problem

Exceptions are another way of indicating that something's gone wrong.

We've already seen some of these. For example, if we run code that does this:

```
int("Hello!")  # Convert Hello! to integer
```

Python's going to be upset. "Hello!" isn't a number it's ever heard of. And when we run it, we get this message, and the program exits:

```
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ValueError: invalid literal for int() with base 10: 'Hello!'
```

That's an exception in action. We tried some code, and it raised an exception to tell us that what we were doing just wasn't going to work.

Exceptions are raised (also sometimes said to be thrown) for all kinds of things in Python.

Try to open a nonexistent file for reading:

```
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
FileNotFoundError: [Errno 2] No such file or directory: 'keyser_soze.txt'
```

Try to divide a number by zero: