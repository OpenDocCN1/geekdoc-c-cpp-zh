# ## 16.3 Algorithms

Sections 16.3.1–16.3.13 demonstrate many of the Standard Library algorithms.

# ### 16.3.1 fill, fill_n, generate and generate_n

Figure 16.1 demonstrates algorithms fill, fill_n, generate and generate_n. Algorithms fill and fill_n set every element in a range of container elements to a specific value. Algorithms generate and generate_n use a generator function to create a value for every element in a range of container elements. The generator function takes no arguments and returns a value that can be placed in an element of the container.

```
```cpp
// Fig. 16.1: Fig16_01.cpp
// Algorithms fill, fill_n, generate and generate_n.
#include <iostream>
#include <algorithm> // algorithm definitions
#include <array> // array class-template definition
#include <iterator> // ostream_iterator
using namespace std;

char nextLetter(); // prototype of generator function

int main()
{
   array<char, 10> chars;
   ostream_iterator<char> output(cout, " ");
   fill(chars.begin(), chars.end(), '5'); // fill chars with 5s

   cout << "chars after filling with 5s:\\n";
   copy(chars.cbegin(), chars.cend(), output);

   // fill first five elements of chars with As
   fill_n(chars.begin(), 5, 'A');

   cout << "\\n\\nchars after filling five elements with As:\\n";
   copy(chars.cbegin(), chars.cend(), output);

   // generate values for all elements of chars with nextLetter
   generate(chars.begin(), chars.end(), nextLetter);

   cout << "\\n\\nchars after generating letters A-J:\\n";
   copy(chars.cbegin(), chars.cend(), output);

   // generate values for first five elements of chars with nextLetter
   generate_n(chars.begin(), 5, nextLetter);

   cout << "\\n\\nchars after generating K-O for the"
        << " first five elements:\\n";
   copy(chars.cbegin(), chars.cend(), output);
   cout << endl;
} // end main
```
```

**Fig. 16.1** | Algorithms fill, fill_n, generate and generate_n. (Part 1 of 2.)