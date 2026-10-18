# SELF-TEST EXERCISES

+   1. If v is a vector, what does v.begin() return? What does v.end() return?
+   2. If p is an iterator for a vector object v, what is *p?
+   3. Suppose v is a vector of ints. Write a for loop that outputs all the elements of v, except for the first element.

# Kinds of Iterators

Different containers have different kinds of iterators. Iterators are classified according to the kinds of operations that work on them. Vector iterators are of the most general form; that is, all the operations work with vector iterators. So, we will again use the vector container to illustrate iterators. In this case we use a vector to illustrate the iterator operators of decrement and random access. Display 18.2 shows another program using a vector object named container and an iterator p.

# DISPLAY 18.2 Bidirectional and Random Access Iterator Use (part 1 of 2)

```
//Program to demonstrate bidirectional and random access iterators.
#include <iostream>
#include <vector>
using std::cout;
using std::endl;
using std::vector;

int main()
{
    vector<char> container;
    container.push_back('A');
    container.push_back('B');
    container.push_back('C');
    container.push_back('D');

    for (int i = 0; i < 4; i++)
        cout << "container[" << i << "] == " << container[i] << endl;
    vector<char>::iterator p = container.begin();
    cout << "The third entry is " << container[2] << endl;
    cout << "The third entry is " << p[2] << endl;
    cout << "The third entry is " << *(p + 2) << endl;

    cout << "Back to container[0].\n";
    p = container.begin();
    cout << "which has value " << *p << endl;
```

Three different notations for the same thing.

This notation is specialized to vectors and arrays.

These two work for any random access iterator.