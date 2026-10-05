844 Introduction to C++

# PREDEFINED ITERATORS

STL provides some types of defined iterators, which are declared in the iterator file. Their main purpose is to expand the generality of the STL algorithms. In this section we'll briefly present some of them. For example, STL provides ostream_iterator, which is an output iterator that can be used to write data in an output stream. Typically, the ostream_iterator and istream_iterator are provided as arguments to algorithms. For example:

```
#include <iostream> // Example 26.5
#include <iterator>
int main() {
    int a[] = {10, 20, 30, 40, 50};
    std::ostream_iterator<int, char> out_it(std::cout, " ");

    copy(a, a+5, out_it);
    return 0;
}
```

The first argument (e.g., int) indicates the type of data to be written to the output stream. The second (e.g., char) indicates the character that the output stream handles. In the constructor of the iterator, the first argument (e.g., cout) indicates the output stream. The second indicates the separator between the values (e.g., a space). Instead of using a named iterator (e.g., out_it), we can create an anonymous iterator like this:

```
copy(a, a+5, ostream_iterator<int, char>(cout, " "));
```

Similarly, there is the istream_iterator, which is an input iterator that can be used to read data from an input stream:

```
#include <iostream> // Example 26.6
#include <vector>
#include <iterator>
using namespace std;

int main() {
    vector<int> v(5);

    cout << "Enter 5 integers and then a character: ";
    copy(istream_iterator<int, char>(cin), istream_iterator<int, char>(),
         v.begin());
    copy(v.begin(), v.end(), ostream_iterator<int, char>(cout, " "));
    return 0;
}
```

The first argument (e.g., int) indicates the type of data to be read from the input stream. The second (e.g., char) indicates the character type used by the input stream. The argument of the constructor (e.g., cin) indicates the input stream. If the argument is missing, it corresponds to an iterator that indicates that there is no data to read or a read error occurred. In our example, these two iterators are used to determine the copy range in copy(). That is, copying occurs until the end of the input data is met or some reading error occurs. Thus, when the user enters five integers, the program reads them