```
if len(sys.argv) != 3:
    print("usage: cal.py year month")
    sys.exit()  # stop running

year = int(sys.argv[1])
month = int(sys.argv[2])

if month < 1 or month > 12:
    print("Month must be 1-12!")
    sys.exit()  # stop running

calendar.prmonth(year, month)
```

Ship it!

# 12.7 Importing Specific Attributes

There’s an alternate syntax for import that you can use to bring attributes from a module directly into the global namespace.

What do I mean by that?

Well, the upshot is that if you’re tired of typing the module name followed by a dot to access a particular function or piece of data, you can bring that in to use directly, instead.

Let’s do an example.

The time modules have a function called ctime() that prints the time out in a classic format.

```
import time

print(time.ctime())  # "Sun Feb  9 13:37:00 2020"
```

But if you’re going to call it repeatedly, it might make the code look worse to have “time.” all over the place.

We can do this, instead:

```
# Bring in ctime() explicitly:

from time import ctime

print(ctime())  # Look, ma! No "time."!
```

If a module has multiple things you want to import, you can bring them in with a comma list:

```
# import all three!

from time import ctime, localtime, monotonic
```

Or, if you’re feeling bold, you can import it all!

```
from time import *
```

But I generally recommend against that. It takes time for Python to do it, and if you only need a few things, pick them explicitly.

Furthermore, a lot of devs rely on the module name being a visual cue that we’re talking about a function in a module, here. If we come across some code that says:

```
print(ctime())
```

Is that a function that the programmer-defined, or is it something that we from imported from somewhere? By putting the name of the module first, it helps mitigate that ambiguity: