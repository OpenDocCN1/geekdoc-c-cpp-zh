silly when the programmer explicitly insists; after all, the programmer might actually know better. Note that you cannot use the **Month(9999)** notation because that would allow only values that could be used in an initialization of a **Month**, and **int**s cannot.

Unfortunately, we cannot define a constructor for an enumeration to check initializer values, but it is trivial to write a simple checking function:

```
```cpp
Month int_to_month(int x)
{
    if (x<int(Month::jan) || int(Month::dec)<x) error("bad month");
    return Month(x);
}
```
```

We use the **int(Month::jan)** notation to get the **int** representation of **Month::jan**. Given that, we can write

```
```cpp
void f(int m)
{
    Month mm = int_to_month(m);
    // ...
}
```
```

What do we use enumerations for? Basically, an enumeration is useful whenever we need a set of related named integer constants. That happens all the time when we try to represent sets of alternatives (**up**, **down**; **yes**, **no**, **maybe**; **on**, **off**; **n**, **ne**, **e**, **se**, **s**, **sw**, **w**, **nw**) or distinctive values (**red**, **blue**, **green**, **yellow**, **maroon**, **crimson**, **black**).

# ### 9.5.1 “Plain” enumerations

In addition to the **enum classes**, also known as *scoped enumerations*, there are “plain” enumerations that differ from scoped enumerations by implicitly “exporting” their enumerators to the scope of the enumeration and allowing implicit conversions to **int**. For example:

```
```cpp
enum Month {                 // note: no “class”
    jan=1, feb, mar, apr, may, jun, jul, aug, sep, oct, nov, dec
};
Month m = feb;               // OK: feb in scope
Month m2 = Month::feb;       // also OK
m = 7;                       // error: can’t assign an int to a Month
```
```