# 26 • Introduction to Standard Template Library 839

The sort() sorts the structures in ascending order according to the grade of each student and the program displays their data.

But if we want to have multiple ways of sorting, and let the user decide? In this case we use the second version of sort(). This version takes three parameters, where the first two are the same as the first version and the third is a pointer to the function to be used (or function object), instead of the operator(), to make the comparison. Its return value must be convertible to bool, with the value true to indicate that the elements are in the right order. For example, let's change the previous program:

```
int main() {
    int sel;
    cout << "Enter sort type (0: grade_order):";
    cin >> sel;
    if(sel == 0)
        sort(v.begin(), v.end());
    else
        sort(v.begin(), v.end(), name_order);
    ...
}
```

```
bool name_order(const Student& s1, const Student& s2) {
    if(s1.name < s2.name)
        return true;
    else
        return false;
}
```

Now, if the user does not enter 0, name_order() compares the name members and sorts the structures in alphabetical order.

# The count_if() Function

Some STL functions have a second version which applies a function to each element of the container. This second version typically ends with _if. For example, count() and count_if(). The first two parameters of count_if() are input iterators (e.g., first, last) that indicate the range, which is [first, last]. The third is a pointer to a function (or function object), which is applied to each element in [first, last]. The return value must be convertible to bool, with the value true to indicate that the element must be counted. count_if() returns the total of elements for which the function returns true value. In general, if _if versions are used when we are interested in finding values that meet some criteria. Let's look at an example of use:

```
#include <iostream> // Example 26.4
#include <vector>
#include <string>
#include <algorithm>
using namespace std;

bool islong(const string& s);
```