
## 9.7.4 const member functions

For built-in types, such as **int** and **double**, the default constructor notation means **0**, so **int()** is a complicated way of saying **0**, and **double()** a long-winded way of saying **0.0**.

Using a default constructor is not just a matter of looks. Imagine that we could have an uninitialized **string** or **vector**.

```cpp
string s;
for (int i=0; i<cs.size(); ++i)    // oops: loop an undefined number of times
    s[i] = toupper(s[i]);           // oops: read and write a random memory location

vector<string> v;
v.push_back("bad");                 // oops: write to random address
```

If the values of **s** and **v** were genuinely undefined, **s** and **v** would have no notion of how many elements they contained or (using the common implementation techniques; see §17.5) where those elements were supposed to be stored. The results would be use of random addresses – and that can lead to the worst kind of errors. Basically, without a constructor, we cannot establish an invariant – we cannot ensure that the values in those variables are valid (§9.4.3). We must insist that such variables are initialized. We could insist on an initializer and then write

```cpp
string s1 = "";
vector<string> v1 {};
```

But we don't think that's particularly pretty. For **string**, **""** is rather obvious for “empty string.” For **vector**, **{}** is pretty for a vector with no elements. However, for many types, it is not easy to find a reasonable notation for a default value. For many types, it is better to define a constructor that gives meaning to the creation of an object without an explicit initializer. Such a constructor takes no arguments and is called a *default constructor*.

There isn't an obvious default value for dates. That's why we haven't defined a default constructor for **Date** so far, but let's provide one (just to show we can):

```cpp
class Date {
public:
    // ...
    Date();                 // default constructor
    // ...
private:
    int y;
    Month m;
    int d;
};
```

We have to pick a default date. The first day of the 21st century might be a reasonable choice:

```cpp
Date::Date()
       :y(2001), m(Month::jan), d{1}
{
}
```

Instead of placing the default values for members in the constructor, we could place them on the members themselves:

```cpp
class Date {
public:
       // ...
       Date();                          // default constructor
       Date(int y, Month m, int d);
       Date(int y);                     // January 1 of year y
       // ...
private:
       int y {2001};
       Month m {Month::jan};
       int d {1};
};
```

That way, the default values are available to every constructor. For example:

```cpp
Date::Date(int yy)                     // January 1 of year yy
      :y(yy)
{
       if (!is_valid()) throw Invalid{};     // check for validity
}
```

Because Date(int) does not explicitly initialize the month (m) or the day (d), the specified initializers (Month::jan and 1) are implicitly used. An initializer for a class member specified as part of the member declaration is called an in-class initializer.

If we didn't like to build the default value right into the constructor code, we could use a constant (or a variable). To avoid a global variable and its associated initialization problems, we use the technique from §8.6.2:

```cpp
const Date& default_date()
{
       static Date dd {2001, Month::jan, 1};
       return dd;
}
```

We used **static** to get a variable (**dd**) that is created only once, rather than each time `default_date()` is called, and initialized the first time `default_date()` is called. Given `default_date()`, it is trivial to define a default constructor for **Date**:

```cpp
Date::Date()
    :y(default_date().year()),
    m(default_date().month()),
    d(default_date().day())
{
}
```

Note that the default constructor does not need to check its value; the constructor for `default_date` already did that. Given this default **Date** constructor, we can now define nonempty vectors of **Dates** without listing element values:

```cpp
vector<Date> birthdays(10); // ten elements with the default Date value,
                            // Date{}
```

Without the default constructor, we would have had to be explicit:

```cpp
vector<Date> birthdays(10,default_date()); // ten default Dates

vector<Date> birthdays2 = { // ten default Dates
    default_date(), default_date(), default_date(), default_date(), default_date(),
    default_date(), default_date(), default_date(), default_date(), default_date()
};
```

We use parentheses, `()`, when specifying the element counts for a **vector**, rather than the `{}` initializer-list notation, to avoid confusion in the case of a **vector**<**int**> (§18.2).

Some variables are meant to be changed — that’s why we call them “variables” — but some are not; that is, we have “variables” representing immutable values. Those, we typically call *constants* or just **consts**. Consider:

```cpp
void some_function(Date& d, const Date& start_of_term)
{
    int a = d.day();   // OK
    int b = start_of_term.day(); // should be OK (why?)
    d.add_day(3); // fine
    start_of_term.add_day(3); // error
}
```

Here we intend **d** to be mutable, but **start_of_term** to be immutable; it is not acceptable for **some_function()** to change **start_of_term**. How would the compiler know that? It knows because we told it by declaring **start_of_term const**. So far, so good, but then why is it OK to read the **day** of **start_of_term** using **day()**? As the definition of **Date** stands so far, **start_of_term.day()** is an error because the compiler does not know that **day()** doesn’t change its **Date**. We never told it, so the compiler assumes that **day()** may modify its **Date** and reports an error.

We can deal with this problem by classifying operations on a class as modifying and nonmodifying. That’s a pretty fundamental distinction that helps us understand a class, but it also has a very practical importance: operations that do not modify the object can be invoked for **const** objects. For example:

```cpp
class Date {
public:
// ...
int day() const; // const member: can’t modify the object
Month month() const; // const member: can’t modify the object
int year() const; // const member: can’t modify the object

void add_day(int n); // non-const member: can modify the object
void add_month(int n); // non-const member: can modify the object
void add_year(int n); // non-const member: can modify the object

private:
int y; // year
Month m;
int d; // day of month
};

Date d <2000, Month::jan, 20>;
const Date cd <2001, Month::feb, 21>;

cout << d.day() << " " << cd.day() << '\n'; // OK
d.add_day(1); // OK
cd.add_day(1); // error: cd is a const
```

We use **const** right after the argument list in a member function declaration to indicate that the member function can be called for a **const** object. Once we have declared a member function **const**, the compiler holds us to our promise not to modify the object. For example:

```cpp
int Date::day() const
{
    ++d;    // error: attempt to change object from const member function
    return d;
}
```

Naturally, we don’t usually try to “cheat” in this way. What the compiler provides for the class implementer is primarily protection against accident, which is particularly useful for more complex code.

## 9.7.5 Members and “helper functions”

When we design our interfaces to be minimal (though complete), we have to leave out lots of operations that are merely useful. A function that can be simply, elegantly, and efficiently implemented as a freestanding function (that is, as a non-member function) should be implemented outside the class. That way, a bug in that function cannot directly corrupt the data in a class object. Not accessing the representation is important because the usual debug technique is “Round up the usual suspects”; that is, when something goes wrong with a class, we first look at the functions that directly access the representation: one of those almost certainly did it. If there are a dozen such functions, we will be much happier than if there were 50.

Fifty functions for a **Date** class! You must wonder if we are kidding. We are not: a few years ago I surveyed a number of commercially used **Date** libraries and found them full of functions like **next\_Sunday()**, **next\_workday()**, etc. Fifty is not an unreasonable number for a class designed for the convenience of the users rather than for ease of comprehension, implementation, and maintenance.

Note also that if the representation changes, only the functions that directly access the representation need to be rewritten. That’s another strong practical reason for keeping interfaces minimal. In our **Date** example, we might decide that an integer representing the number of days since January 1, 1900, is a much better representation for our uses than \(year, month, day\). Only the member functions would have to be changed.

Here are some examples of *helper functions*:

```cpp
Date next_Sunday(const Date& d)
{
    // access d using d.day(), d.month(), and d.year()
    // make new Date to return
}
```
