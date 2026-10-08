
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

If you insist on using the **Month(9999)** notation, on your head be it! In many cases, C++ will not try to stop a programmer from doing something potentially silly when the programmer explicitly insists; after all, the programmer might actually know better. Note that you cannot use the **Month(9999)** notation because that would allow only values that could be used in an initialization of a **Month**, and **int**s cannot.

Unfortunately, we cannot define a constructor for an enumeration to check initializer values, but it is trivial to write a simple checking function:

```cpp
Month int_to_month(int x)
{
    if (x<int(Month::jan) || int(Month::dec)<x) error("bad month");
    return Month(x);
}
```

We use the **int(Month::jan)** notation to get the **int** representation of **Month::jan**. Given that, we can write

```cpp
void f(int m)
{
    Month mm = int_to_month(m);
    // ...
}
```

What do we use enumerations for? Basically, an enumeration is useful whenever we need a set of related named integer constants. That happens all the time when we try to represent sets of alternatives (**up**, **down**; **yes**, **no**, **maybe**; **on**, **off**; **n**, **ne**, **e**, **se**, **s**, **sw**, **w**, **nw**) or distinctive values (**red**, **blue**, **green**, **yellow**, **maroon**, **crimson**, **black**).

### 9.5.1 “Plain” enumerations

In addition to the **enum classes**, also known as *scoped enumerations*, there are “plain” enumerations that differ from scoped enumerations by implicitly “exporting” their enumerators to the scope of the enumeration and allowing implicit conversions to **int**. For example:

```cpp
enum Month {                 // note: no “class”
    jan=1, feb, mar, apr, may, jun, jul, aug, sep, oct, nov, dec
};
Month m = feb;               // OK: feb in scope
Month m2 = Month::feb;       // also OK
m = 7;                       // error: can’t assign an int to a Month
```

```cpp
int n = m; // OK: we can assign a Month to an int
Month mm = Month(7); // convert int to Month (unchecked)
```

Obviously, “plain” **enums** are less strict than **enum classes**. Their enumerators can “pollute” the scope in which their enumerator is defined. That can be a convenience, but it occasionally leads to surprises. For example, if you try to use this Month together with the iostream formatting mechanisms (§11.2.1), you will find that **dec** for December clashes with **dec** for decimal.

Similarly, having an enumeration value convert to **int** can be a convenience (it saves us from being explicit when we want a conversion to **int**), but occasionally it leads to surprises. For example:

```cpp
void my_code(Month m)
{
  if (m==17) do_something(); // huh: 17th month?
  if (m==monday) do_something_else(); // huh: compare month to
  // Monday?
}
```

If **Month** is an **enum class**, neither condition will compile. If **monday** is an enumerator of a “plain” **enum**, rather than an **enum class**, the comparison of a month to **monday** would succeed, most likely with undesirable results.

Prefer the simpler and safer **enum classes** to “plain” **enums**, but expect to find “plain” **enums** in older code: **enum classes** are new in C++11.

## 9.6 Operator overloading

You can define almost all C++ operators for class or enumeration operands. That’s often called operator overloading. We use it when we want to provide conventional notation for a type we design. For example:

```cpp
enum class Month {
Jan=1, Feb, Mar, Apr, May, Jun, Jul, Aug, Sep, Oct, Nov, Dec
};
Month operator++(Month& m) // prefix increment operator
{
m = (m==Month::Dec) ? Month::Jan : Month(int(m)+1); // “wrap
// around”
return m;
}
```

The `?:` construct is an “arithmetic if”: **m** becomes **Jan** if (**m**==**Month::Dec**) and **Month**(**int**(**m**)+1) otherwise. It is a reasonably elegant way of expressing the fact that months “wrap around” after December. The **Month** type can now be used like this:

```cpp
Month m = Month::Sep;
++m;      // m becomes Oct
++m;      // m becomes Nov
++m;      // m becomes Dec
++m;      // m becomes Jan (“wrap around”)
```

You might not think that incrementing a **Month** is common enough to warrant a special operator. That may be so, but how about an output operator? We can define one like this:

```cpp
vector<string> month_tbl;

ostream& operator<<(ostream& os, Month m)
{
  return os << month_tbl[int(m)];
}
```

This assumes that **month_tbl** has been initialized somewhere so that (for example) **month_tbl[int(Month::Mar)]** is “**March**” or some other suitable name for that month; see §10.11.3.

You can define just about any operator provided by C++ for your own types, but only existing operators, such as **+**, **-**, **\***, **/**, **%**, **[]**, **()**, **^**, **!**, **&&**, **<<**, **>>**, and **>=**. You cannot define your own operators; you might like to have **\*** or **$** as operators in your program, but C++ won’t let you. You can define operators only with their conventional number of operands; for example, you can define unary **-**, but not unary **<=** (less than or equal), and binary **+**, but not binary **!** (not). Basically, the language allows you to use the existing syntax for the types you define, but not to extend that syntax.

An overloaded operator must have at least one user-defined type as operand:

```cpp
int operator+(int,int);   // error: you can’t overload built-in +
Vector operator+(const Vector&, const Vector&);      // OK
Vector operator+=(const Vector&, int);                // OK
```

It is generally a good idea not to define operators for a type unless you are really certain that it makes a big positive change to your code. Also, define operators only with their conventional meaning: **+** should be addition, binary **\*** multiplication, **[]** access, **()** call, etc. This is just advice, not a language rule, but it is good advice: conventional use of operators, such as **+** for addition, can significantly help us understand a program. After all, such use is the result of hundreds of years of experience with mathematical notation. Conversely, obscure operators and unconventional use of operators can be a significant distraction and a source of errors. We will not elaborate on this point. Instead, in the following chapters, we will simply use operator overloading in a few places where we consider it appropriate.

Note that the most interesting operators to overload aren’t **+**, **-**, **\***, and **/** as people often assume, but **=**, **==**, **!=**, **<**, **[]** (subscript), and **()** (call).

## 9.7 Class interfaces

We have argued that the public interface and the implementation parts of a class should be separated. As long as we leave open the possibility of using structs for types that are “plain old data,” few professionals would disagree. However, how do we design a good interface? What distinguishes a good public interface from a mess? Part of that answer can be given only by example, but there are a few general principles that we can list and that are given some support in C++:

- Keep interfaces complete.
- Keep interfaces minimal.
- Provide constructors.
- Support copying (or prohibit it) (see §14.2.4).
- Use types to provide good argument checking.
- Identify nonmodifying member functions (see §9.7.4).
- Free all resources in the destructor (see §17.5).

See also §5.5 (how to detect and report run-time errors).

The first two principles can be summarized as “Keep the interface as small as possible, but no smaller.” We want our interface to be small because a small interface is easy to learn and easy to remember, and the implementer doesn’t waste a lot of time implementing unnecessary and rarely used facilities. A small interface also means that when something is wrong, there are only a few functions to check to find the problem. On average, the more public member functions are, the harder it is to find bugs – and please don’t get us started on the complexities of debugging classes with public data. But of course, we want a complete interface; otherwise, it would be useless. We couldn’t use an interface that didn’t allow us to do all we really needed.

Let’s look at the other – less abstract and more directly supported – ideals.
