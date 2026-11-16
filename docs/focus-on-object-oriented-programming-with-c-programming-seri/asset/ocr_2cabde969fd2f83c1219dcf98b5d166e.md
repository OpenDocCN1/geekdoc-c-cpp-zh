```
Alpha& Alpha::operator=(const Alpha& a) {
    delete [] buf;
    buf = new char[strlen(a.buf) + 1];
    strcpy(buf, a.buf);
    i = a.i;
    d = a.d;
    return *this;
}
```

We return *this to go along with the usual C++ convention that an assignment should return a reference to its left-hand side.

However, this code has a serious bug. Try and find it before you read on.

...

It fails if you try to assign an object to itself:

```
a = a;
```

To fix this bug, we need a conditional statement in the code to guard against:

```
String s;
s = s;
```

Without this test, an assignment of an Alpha object to itself would delete the data member buf of that Alpha object and then try to copy the just-deleted data.

Once we are sure that we are dealing with two different objects, the assignment operator (unlike the copy constructor) should release any resources that held the old value. After that, the assignment operator usually does the same thing as the copy constructor, except that the assignment operator returns a value.