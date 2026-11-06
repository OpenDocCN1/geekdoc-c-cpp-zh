
```cpp
int iArr[] = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10};

cout << count_if(iArr, iArr + 10, bind2nd(less_equal<int>(), 6)) <<
     ', ';
cout << count_if(iArr, iArr + 10, bind2nd(not2(greater<int>()), 6)) <<
     ', ';
cout << count_if(iArr, iArr + 10, not1(bind2nd(greater<int>(), 6))) <<
     '\n';
}
// Displays: 6 6 6
```

One may wonder which of these alternative approaches is the faster. Using the first approach, in which a directly available function object was used, two actions must be performed for each iteration by `count_if`:

- The binder’s `operator()` is called;
- The operation `<=` is performed.

When the compiler uses inline as requested, only the second step is actually performed.

Using the second approach, using the `not2` negator to negate the truth value of the complementary logical function object, three actions must be performed for each iteration by `count_if`:

- The binder’s `operator()` is called;
- The negator’s `operator()` is called;
- The operation `>` is performed.

When the compiler uses inline as requested, only the third step is actually performed.

Using the third approach, using `not1` negator to negate the truth value of the binder, three actions must be performed for each iteration by `count_if`:

- The negator’s `operator()` is called;
- The binder’s `operator()` is called;
- The operation `>` is performed.

When the compiler uses inline as requested, only the third step is actually performed.

With a commonly used optimization flag like `-O2` the compiler tries to grant inline requests. However, if the compiler ignores the inline requests the first variant will be faster.

## 18.2 Iterators

In addition to the conceptual iterator types presented in this section the STL defines several adaptors allowing objects to be passed as iterators. These adaptors are presented in the upcoming sections. Before those adaptors can be used the `<iterator>` header file must have been included.

Iterators are objects acting like pointers. Iterators have the following general characteristics:

- Two iterators may be compared for (in)equality using the `==` and `!=` operators. The *ordering* operators (e.g., `>`, `<`) can usually not be used.
- Given an iterator `iter`, `*iter` represents the object the iterator points to (alternatively, `iter->` can be used to reach the members of the object the iterator points to).
- `++iter` or `iter++` advances the iterator to the next element. The notion of advancing an iterator to the next element is consequently applied: several containers support `reverse_iterator` types, in which the `++iter` operation actually reaches a previous element in a sequence.
- *Pointer arithmetic* may be used with iterators of containers storing their elements consecutively in memory like vector and deque. For such containers `iter + 2` points to the second element beyond the one to which `iter` points.
- Merely defining an iterator is comparable to having a 0-pointer. Example:

  ```cpp
  #include <vector>
  #include <iostream>
  using namespace std;

  int main()
  {
      vector<int>::iterator vi;

      cout << *vi;        // prints 0
  }
  ```

STL containers usually define members offering iterators (i.e., they define their own type `iterator`). These members are commonly called `begin` and `end` and (for reverse iterators (type `reverse_iterator`)) `rbegin` and `rend`.

Standard practice requires iterator ranges to be *left* inclusive. The notation `[left, right)` indicates that `left` is an iterator pointing to the first element, while `right` is an iterator pointing just beyond the last element. The iterator range is empty when `left == right`.

The following example shows how all elements of a vector of strings can be inserted into `cout` using its iterator ranges `[begin(), end())`, and `[rbegin(), rend())`. Note that the `for`-loops for both ranges are identical. Furthermore it nicely illustrates how the auto keyword can be used to define the type of the loop control variable instead of using a much more verbose variable definition like `vector<string>::iterator` (see also section 3.3.5):

```cpp
#include <iostream>
#include <vector>
#include <string>
using namespace std;

int main(int argc, char **argv)
{
    vector<string> args(argv, argv + argc);

    for (auto iter = args.begin(); iter != args.end(); ++iter)
        cout << *iter << " ";
    cout << '\n';

    for (auto iter = args.rbegin(); iter != args.rend(); ++iter)
        cout << *iter << " ";
    cout << '\n';
}
```

Furthermore, the STL defines `const_iterator` types that must be used when visiting a series of elements in a constant container. Whereas the elements of the vector in the previous example could have been altered, the elements of the vector in the next example are immutable, and `const_iterators` are required:

```cpp
#include <iostream>
#include <vector>
#include <string>
using namespace std;

int main(int argc, char **argv)
{
    vector<string> const args(argv, argv + argc);

    for
    (
        vector<string>::const_iterator iter = args.begin();
            iter != args.end();
                ++iter
    )
        cout << *iter << " ";
    cout << '\n';

    for
    (
        vector<string>::const_reverse_iterator iter = args.rbegin();
            iter != args.rend();
                ++iter
    )
        cout << *iter << " ";
    cout << '\n';

    return 0;
}
```

The examples also illustrates that plain pointers can be used as iterators. The initialization vector<string> args(argv, argv + argc) provides the args vector with a pair of pointer-based iterators: argv points to the first element to initialize args with, argv + argc points just beyond the last element to be used, ++argv reaches the next command line argument. This is a general pointer characteristic, which is why they too can be used in situations where iterators are expected.

The STL defines five types of iterators. These iterator types are expected by generic algorithms, and in order to create a particular type of iterator yourself it is important to know their characteristics. In general, iterators (see also section 21.13) must define:

- `operator==`, testing two iterators for equality,
- `operator!=`, testing two iterators for inequality,
- `operator++`, incrementing the iterator, as prefix operator,
- `operator*`, to access the element the iterator refers to,

The following types of iterators are used when describing generic algorithms in chapter 19:

- InputIterators:

  InputIterators are used to read from a container. The dereference operator is guaranteed to work as rvalue in expressions. Instead of an InputIterator it is also possible to use (see below) Forward-, Bidirectional- or RandomAccessIterators. Notations like InputIterator1 and InputIterator2 may be used as well. In these cases, numbers are used to indicate which iterators 'belong together'. E.g., the generic algorithm inner_product has the following prototype:

  ```cpp
  Type inner_product(InputIterator1 first1, InputIterator1 last1,
                     InputIterator2 first2, Type init);
  ```

- inserter calls the container’s `insert` member adding new elements starting at a specified starting point. E.g., to copy all elements of source to the destination container, starting at the beginning of destination, shifting up existing elements to beyond the newly inserted elements:

  ```cpp
  copy(source.begin(), source.end(), inserter(destination,
       destination.begin()));
  ```

The inserter adaptors require the existence of two typedefs:

- `typedef Data value_type`, where Data is the data type stored in the class offering `push_back`, `push_front` or `insert` members (Example: `typedef std::string value_type;`)
- `typedef value_type const &const_reference`

Concentrating on `back_inserter`, its iterator expects the name of a container supporting a member `push_back`. The inserter’s `operator()` member calls the container’s `push_back` member. Objects of any class supporting a `push_back` member can be passed as arguments to `back_inserter` provided the class adds

```cpp
typedef DataType const &const_reference;
```

to its interface (where `DataType const &` is the type of the parameter of the class’s member `push_back`). Example:

```cpp
#include <iostream>
#include <algorithm>
#include <iterator>
using namespace std;

class Insertable
{
    public:
        typedef int value_type;
        typedef int const &const_reference;

        void push_back(int const &)
        {}
};

int main()
{
        int arr[] = {1};
        Insertable insertable;

        copy(arr, arr + 1, back_inserter(insertable));
}
```

### 18.2.2 Iterators for ‘istream’ objects

The `istream_iterator<Type>` can be used to define a set of iterators for istream objects. The general form of the `istream_iterator` iterator is:

```cpp
istream_iterator<Type> identifier(istream &in)
```

Here, Type is the type of the data elements read from the istream stream. It is used as the ‘begin’ iterator in an iterator range. Type may be any type for which `operator>>` is defined in combination with istream objects.
