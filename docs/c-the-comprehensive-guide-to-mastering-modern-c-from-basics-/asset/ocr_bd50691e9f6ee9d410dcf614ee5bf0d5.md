The difference lies in the overloads—more specifically, in the type of the second parameter. Overall, the following overloads are declared for our classes:

```
ostream operator<<(ostream&os, const Calendar& cc);
ostream operator<<(ostream&os, const Clock& cc);
ostream operator<<(ostream&os, const CalendarClock& cc);
```

In Listing 18.15, there is a CalendarClock&. I get the compiler to take the other overloads by casting the parameter—that is, converting the type. As in a simple inheritance hierarchy, this also works with multiple base classes. And so, the following code sequentially calls the overloads for the two classes:

```
operator<<(os, (Calendar&cc)) << " ";
operator<<(os, (Clock&cc));
```

> If you explicitly need to reference a member of a base class, you can do so in different ways:

* You prefix the identifier with the base class, as in Clock::tick().
* Or you cast the reference to a reference of the base class, as in operator<<(os, (Clock&cc)). This also works for pointers.

This general approach is particularly useful in multiple inheritance.