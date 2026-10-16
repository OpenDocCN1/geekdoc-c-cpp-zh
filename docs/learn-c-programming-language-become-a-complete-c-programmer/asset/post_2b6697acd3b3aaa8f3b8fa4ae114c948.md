
- To place objects on the stack, in statically allocated memory, and in other objects
- To copy and move objects (§3.3, §17.5)
- To refer directly to named objects (as opposed to accessing through pointers and references) This makes concrete classes simple to reason about and easy for the compiler to generate optimal code for. Thus, we prefer concrete classes for small, frequently used, and performance-critical types, such as complex numbers (§5.6.2), smart pointers (§5.2.1), and containers (§4.4).

It was an early explicit aim of C++ to support the definition and efficient use of such user-defined types very well. They are a foundation of elegant programming. As usual, the simple and mundane is statistically far more significant than the complicated and sophisticated. In this light, let us build a better **Date** class:

```cpp
namespace Chrono {
enum class Month { jan=1, feb, mar, apr, may, jun, jul, aug, sep, oct, nov, dec };
class Date {
public: // public interface:
class Bad_date { }; // exception class
explicit Date(int dd ={}, Month mm ={}, int yy ={}); // {} means “pick a default”

// nonmodifying functions for examining the Date:
int day() const;
Month month() const;
int year() const;

string string_rep() const;
void char_rep(char s[], int max) const;
// string representation
// C-style string representation

// (modifying) functions for changing the Date:
Date& add_year(int n);
Date& add_month(int n);
Date& add_day(int n);

private:
bool is_valid();
int d, m, y;
};

// add n years // add n months // add n days

// check if this Date represents a date // representation
bool is_date(int d, Month m, int y); bool is_leapyear(int y);
// true for valid date // true if y is a leap year
bool operator==(const Date& a, const Date& b); bool operator!=(const Date& a, const Date& b);
const Date& default_date(); // the default date
ostream& operator<<(ostream& os, const Date& d); // print to os
istream& operator>>(istream& is, Date& d); // read Date from is into d } // Chrono
}
```

This set of operations is fairly typical for a user-defined type:

- [1] A constructor specifying how objects/variables of the type are to be initialized (§16.2.5).
- [2] A set of functions allowing a user to examine a **Date**. These functions are marked **const** to indicate that they don’t modify the state of the object/variable for which they are called.
- [3] A set of functions allowing the user to modify **Dates** without actually having to know the details of the representation or fiddle with the intricacies of the semantics.
- [4] Implicitly defined operations that allow **Dates** to be freely copied (§16.2.2).
- [5] A class, **Bad_date**, to be used for reporting errors as exceptions.
- [6] A set of useful helper functions. The helper functions are not members and have no direct access to the representation of a **Date**, but they are identified as related by the use of the namespace **Chrono**.

I defined a **Month** type to cope with the problem of remembering the month/day order, for example, to avoid confusion about whether the 7th of June is written **{6,7}** (American style) or **{7,6}** (European style).

I considered introducing separate types **Day** and **Year** to cope with possible confusion of **Date{1995,Month::jul,27}** and **Date{27,Month::jul,1995}**. However, these types would not be as useful as the **Month** type. Almost all such errors are caught at run time anyway – the 26th of July year 27 is not a common date in my work. Dealing with historical dates before year 1800 or so is a tricky issue best left to expert historians. Furthermore, the day of the month can’t be properly checked in isolation from its month and year.

To save the user from having to explicitly mention year and month even when they are implied by context, I added a mechanism for providing a default. Note that for **Month** the **{}** gives the (default) value **0** just as for integers even though it is not a valid **Month** (§8.4). However, in this case, that’s exactly what we want: an otherwise illegal value to represent “pick the default.” Providing a default (e.g., a default value for **Date** objects) is a tricky design problem. For some types, there is a conventional default (e.g., **0** for integers); for others, no default makes sense; and finally, there are some types (such as **Date**) where the question of whether to provide a default is nontrivial. In such cases, it is best – at least initially – not to provide a default value. I provide one for **Date** primarily to be able to discuss how to do so.

I omitted the cache technique from §16.2.9 as unnecessary for a type this simple. If needed, it can be added as an implementation detail without affecting the user interface. Here is a small – and contrived – example of how **Dates** can be used:

```cpp
void f(Date& d)
{
    Date lvb_day {16,Month::dec,d.year()};
    if (d.day()==29 && d.month()==Month::feb) { // ...
    }

    if (midnight()) d.add_day(1);
    cout << "day after:" << d+1 << '\n';

    Date dd; // initialized to the default date
    cin >> dd;
    if (dd==d) cout << "Hurray!\n";
}
```

This assumes that the addition operator, +, has been declared for Dates. I do that in §16.3.3.

Note the use of explicit qualification of dec and feb by Month. I used an enum class (§8.4.1) specifically to be able to use short names for the months, yet also ensure that their use would not be obscure or ambiguous.

Why is it worthwhile to define a specific type for something as simple as a date? After all, we could just define a simple data structure:

```cpp
struct Date {
int day, month, year;
};
```

Each programmer could then decide what to do with it. If we did that, though, every user would either have to manipulate the components of Dates directly or provide separate functions for doing so. In effect, the notion of a date would be scattered throughout the system, which would make it hard to understand, document, or change. Inevitably, providing a concept as only a simple structure causes extra work for every user of the structure.

Also, even though the Date type seems simple, it takes some thought to get right. For example, incrementing a Date must deal with leap years, with the fact that months are of different lengths, and so on. Also, the day-month-and-year representation is rather poor for many applications. If we decided to change it, we would need to modify only a designated set of functions. For example, to represent a Date as the number of days before or after January 1, 1970, we would need to change only Date’s member functions.

To simplify, I decided to eliminate the notion of changing the default date. Doing so eliminates some opportunities for confusion and the likelihood of race conditions in a multi-threaded program (§5.3.1). I seriously considered eliminating the notion of a default date altogether. That would have forced users to consistently explicitly initialize their Dates. However, that can be inconvenient and surprising, and more importantly common interfaces used for generic code require default construction (§17.3.3). That means that I, as the designer of Date, have to pick the default date. I chose January 1, 1970, because that is the starting point for the C and C++ standard-library time routines (§35.2, §43.6). Obviously, eliminating set_default_date() caused some loss of generality of Date. However, design – including class design – is about making decisions, rather than just deciding to postpone them or to leave all options open for users.

To preserve an opportunity for future refinement, I declared default_date() as a helper function:

```cpp
const Date& Chrono::default_date();
```

### 16.3.1 Member Functions

Naturally, an implementation for each member function must be provided somewhere. For example:

```cpp
Date::Date(int dd, Month mm, int yy)
:d{dd}, m{mm}, y{yy}
```
