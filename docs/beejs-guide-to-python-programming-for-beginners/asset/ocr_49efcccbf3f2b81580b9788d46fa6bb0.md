Let's do exactly that:

```
import sys
import calendar

year = sys.argv[1]
month = sys.argv[2]

calendar.prmonth(year, month)
```

When we run it with:

```
python cal.py 1970 1
```

though, something bad happens:

```
Traceback (most recent call last):
  File "cal.py", line 7, in <module>
    calendar.prmonth(year, month)
  File "/usr/lib/python3.8/calendar.py", line 350, in prmonth
    print(self.formatmonth(theyear, themonth, w, l), end='')
  File "/usr/lib/python3.8/calendar.py", line 358, in formatmonth
    s = self.formatmonthname(theyear, themonth, 7 * (w + 1) - 1)
  File "/usr/lib/python3.8/calendar.py", line 341, in formatmonthname
    s = month_name[themonth]
  File "/usr/lib/python3.8/calendar.py", line 59, in __getitem__
    funcs = self._months[i]
TypeError: list indices must be integers or slices, not str
```

Yikes!

Let's take this error apart and see if we can tell what's up. It's not really being that forthcoming, is it?

Start at the top. It tells you what file the error is in on the first line: cal.py on line 7. And it shows us the line below that... it's where we're calling calendar.prmonth().

But that looks fine, right?

Going farther down, it's showing us the call stack, that is, the path of function calls that culminated in the error. And those are in the calendar.py file, which is the calendar module.

We didn't even write that code! How dare there be an error in it!

Well, it's not an error—it's the module telling us, in a roundabout way, we're not using it right.

Finally, at the bottom, we see the error itself: TypeError. And the description:

```
TypeError: list indices must be integers or slices, not str
```

We don't have any lists in our code, so what's it even talking about lists for? Well, who knows how the stuff is implemented in the library, but scan that error message and see if there's anything in there that hints toward what we have to do.

It says "must be integers or slices, not str". Hmmm.

When we called it with

```
calendar.prmonth(1970, 1)
```

it was fine, but now it's not? Wait—when we called it that way, we passed integers in... but now we're passing in sys.argv[1]. Is that an integer?

There's a built-in function called type() we can use. Let's add this code:

```
import sys
import calendar

year = sys.argv[1]
```