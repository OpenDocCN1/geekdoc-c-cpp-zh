
applied to strings. This object is called as a function object by the `sort` generic algorithm. The generic algorithm calls the function object's `operator()` member to compare two string objects. The function object's `operator()` will, in turn, call `operator<` of the string data type. Eventually, when `sort` returns, the first element of the vector will contain the string having the greatest string value of all.

The function object's `operator()` itself is not visible at this point. Don't confuse the parentheses in the `greater<string>()` argument with calling `operator()`. When `operator()` is actually used inside `sort`, it receives two arguments: two strings to compare for ‘greaterness’. Since `greater<string>::operator()` is defined inline, the call itself is not actually present in the above `sort` call. Instead `sort` calls `string::operator>` through `greater<string>::operator()`.

Now that we know that a constructor is passed as argument to (many) generic algorithms, we can design our own function objects. Assume we want to sort our vector case-insensitively. How do we proceed? First we note that the default `string::operator<` (for an incremental sort) is not appropriate, as it does case sensitive comparisons. So, we provide our own `CaseInsensitive` class, which compares two strings case insensitively. Using the standard C function `strcasecmp`, the following program performs the trick. It case-insensitively sorts its command-line arguments in ascending alphabetic order:

```cpp
#include <iostream>
#include <string>
#include <cstring>
#include <algorithm>
using namespace std;

class CaseInsensitive
{
    public:
        bool operator()(string const &left, string const &right) const
        {
            return strcasecmp(left.c_str(), right.c_str()) < 0;
        }
};
int main(int argc, char **argv)
{
    sort(argv, argv + argc, CaseInsensitive());
    for (int idx = 0; idx < argc; ++idx)
        cout << argv[idx] << " ";
    cout << '\n';
}
```

The default constructor of the class `CaseInsensitive` is used to provide `sort` with its final argument. So the only member function that must be defined is `CaseInsensitive::operator()`. Since we know it's called with string arguments, we define it to expect two string arguments, which are used when calling `strcasecmp`. Furthermore, `operator()` function is defined inline, so that it does not produce overhead when called by the `sort` function. The `sort` function calls the function object with various combinations of strings. If the compiler grants our inline requests, it will in fact call `strcasecmp`, skipping two extra function calls.

The comparison function object is often a *predefined function object*. Predefined function object classes are available for many commonly used operations. In the following sections the available predefined function objects are presented, together with some examples showing their use. Near the end of the section about function objects *function adaptors* are introduced.

Predefined function objects are used predominantly with generic algorithms. Predefined function objects exist for arithmetic, relational, and logical operations. In section 23.3 predefined function objects are developed performing bitwise operations.

### 18.1.1 Arithmetic function objects

The arithmetic function objects support the standard arithmetic operations: addition, subtraction, multiplication, division, modulo and negation. These function objects invoke the corresponding operators of the data types for which they are instantiated. For example, for addition the function object `plus<Type>` is available. If we replace `Type` by `size_t` then the addition operator for `size_t` values is used, if we replace `Type` by `string`, the addition operator for strings is used. For example:

```cpp
#include <iostream>
#include <string>
#include <functional>
using namespace std;

int main(int argc, char **argv)
{
    plus<size_t> uAdd;            // function object to add size_ts

    cout << "3 + 5 = " << uAdd(3, 5) << '\n';

    plus<string> sAdd;            // function object to add strings

    cout << "argv[0] + argv[1] = " << sAdd(argv[0], argv[1]) << '\n';
}
/*
    Output when called as: a.out going

    3 + 5 = 8
    argv[0] + argv[1] = a.outgoing
*/
```

Why is this useful? Note that the function object can be used with all kinds of data types (not only with the predefined datatypes) supporting the operator called by the function object.

Suppose we want to perform an operation on a left hand side operand which is always the same variable and a right hand side argument for which, in turn, all elements of an array should be used. E.g. we want to compute the sum of all elements in an array; or we want to concatenate all the strings in a text-array. In situations like these function objects come in handy.

As stated, function objects are heavily used in the context of the generic algorithms, so let's take a quick look ahead at yet another one.

The generic algorithm `accumulate` visits all elements specified by an iterator-range, and performs a requested binary operation on a common element and each of the elements in the range, returning the accumulated result after visiting all elements specified by the iterator range. It's easy to use this algorithm. The next program accumulates all command line arguments and prints the final string:

```cpp
#include <iostream>
#include <string>
#include <functional>
#include <numeric>
using namespace std;

int main(int argc, char **argv)
{
    string result =
        accumulate(argv, argv + argc, string(), plus<string>());

    cout << "All concatenated arguments: " << result << '\n';
}
```

The first two arguments define the (iterator) range of elements to visit, the third argument is `string`. This anonymous string object provides an initial value. We could also have used

```cpp
string("All concatenated arguments: ")
```

in which case the `cout` statement could simply have been `cout << result << '\n'`. The string-addition operation is used, called from `plus<string>`. The final concatenated string is returned.

Now we define a class `Time`, overloading `operator+`. Again, we can apply the predefined function object `plus`, now tailored to our newly defined datatype, to add times:

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <functional>
#include <numeric>
using namespace std;

class Time
{
    friend ostream &operator<<(ostream &str, Time const &time);
    size_t d_days;
    size_t d_hours;
    size_t d_minutes;
    size_t d_seconds;
public:
    Time(size_t hours, size_t minutes, size_t seconds);
    Time &operator+=(Time const &rValue);
};
Time operator+(Time const &lValue, Time const &rValue)
{
    Time ret(lValue);
    ret += rValue;
    return ret;
}

Time::Time(size_t hours, size_t minutes, size_t seconds)
:
    d_days(0),
    d_hours(hours),
    d_minutes(minutes),
    d_seconds(seconds)
{}
Time &Time::operator+=(Time const &rValue)
{
    d_seconds   += rValue.d_seconds;
    d_minutes   += rValue.d_minutes   + d_seconds / 60;
    d_hours     += rValue.d_hours     + d_minutes / 60;
    d_days      += rValue.d_days      + d_hours / 24;
    d_seconds   %= 60;
    d_minutes   %= 60;
    d_hours     %= 24;
    return *this;
}
ostream &operator<<(ostream &str, Time const &time)
{
    return str << time.d_days << " days, " << time.d_hours <<
                                 " hours, " <<
                  time.d_minutes << " minutes and " <<
                  time.d_seconds << " seconds.";
}
int main(int argc, char **argv)
{
    vector<Time> tvector;

    tvector.push_back(Time(1, 10, 20));
    tvector.push_back(Time(10, 30, 40));
    tvector.push_back(Time(20, 50, 0));
    tvector.push_back(Time(30, 20, 30));

    cout <<
        accumulate
        (
            tvector.begin(), tvector.end(), Time(0, 0, 0), plus<Time>()
        ) <<
        '\n';
}
// Displays: 2 days, 14 hours, 51 minutes and 30 seconds.
```

The design of the above program is fairly straightforward. `Time` defines a constructor, it defines an insertion operator and it defines its own `operator+`, adding two time objects. In `main` four `Time` objects are stored in a `vector<Time>` object. Then, `accumulate` is used to compute the accumulated time. It returns a `Time` object, which is inserted into `cout`.

While the first example did show the use of a *named* function object, the last two examples showed the use of *anonymous* objects that were passed to the (`accumulate`) function.

The STL supports the following set of arithmetic function objects. The function call operator (`operator()`) of these function objects calls the matching arithmetic operator for the objects that are passed to the function call operator, returning that arithmetic operator’s return value. The arithmetic operator that is actually called is mentioned below:

- `plus<>`: calls the binary `operator+`;
- `minus<>`: calls the binary `operator-`;
- `multiplies<>`: calls the binary `operator*`;
- `divides<>`: calls `operator/`;
- `modulus<>`: calls `operator%`;
- `negate<>`: calls the unary `operator-`. This arithmetic function object is a unary function object as it expects one argument.

In the next example the `transform` generic algorithm is used to toggle the signs of all elements of an array. `transform` expects two iterators, defining the range of objects to be transformed; an iterator defining the begin of the destination range (which may be the same iterator as the first argument); and a function object defining a unary operation for the indicated data type.

```cpp
#include <iostream>
#include <string>
#include <functional>
#include <algorithm>
using namespace std;

int main(int argc, char **argv)
{
    int iArr[] = { 1, -2, 3, -4, 5, -6 };
```
