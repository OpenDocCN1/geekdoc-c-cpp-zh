The “body” of an enumeration is simply a list of its enumerators. The class in **enum class** means that the enumerators are in the scope of the enumeration. That is, to refer to **jan**, we have to say **Month::jan**.

You can give a specific representation value for an enumerator, as we did for **jan** here, or leave it to the compiler to pick a suitable value. If you leave it to the compiler to pick, it’ll give each enumerator the value of the previous enumerator plus one. Thus, our definition of **Month** gave the months consecutive values starting with **1**. We could equivalently have written

```
enum class Month {
    jan=1, feb=2, mar=3, apr=4, may=5, jun=6,
    jul=7, aug=8, sep=9, oct=10, nov=11, dec=12
};
```

However, that’s tedious and opens the opportunity for errors. In fact, we made two typing errors before getting this latest version right; it is better to let the compiler do simple, repetitive “mechanical” things. The compiler is better at such tasks than we are, and it doesn’t get bored.

If we don’t initialize the first enumerator, the count starts with **0**. For example:

```
enum class Day {
    monday, tuesday, wednesday, thursday, friday, saturday, sunday
};
```

Here **monday** is represented as **0** and **sunday** is represented as **6**. In practice, starting with **0** is often a good choice.

We can use our **Month** like this:

```
Month m = Month::feb;

Month m2 = feb;            // error: feb is not in scope
m = 7;                      // error: can't assign an int to a Month
int n = m;                  // error: can't assign a Month to an int
Month mm = Month(7);        // convert int to Month (unchecked)
```

**Month** is a separate type from its “underlying type” **int**. Every **Month** has an equivalent integer value, but most **ints** do not have a **Month** equivalent. For example, we really do want this initialization to fail:

```
Month bad = 9999;          // error: can't convert an int to a Month
```

If you insist on using the **Month(9999)** notation, on your head be it! In many cases, C++ will not try to stop a programmer from doing something potentially