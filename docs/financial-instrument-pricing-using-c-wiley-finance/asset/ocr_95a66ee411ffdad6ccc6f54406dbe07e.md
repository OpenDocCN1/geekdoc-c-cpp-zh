```
```cpp
std::cout << ": found? " << std::boolalpha
          << std::includes(range.begin(), range.end(),
                           searchRange.begin(), searchRange.end())<< '\n';

auto CmpNoCase = [](char a, char b)
    {return std::tolower(a) < std::tolower(b);};

std::vector<char> v1 = { 'a', 'b', 'c', 'f', 'h', 'x' };

std::vector<char> v2 = { 'A', 'B', 'C' };
std::cout << ": (case-insensitive) " << std::boolalpha
          << std::includes(v1.begin(), v1.end(), v2.begin(), v2.end(),
                           CmpNoCase) << '\n';
}
```
```

The output is:

```
```text
** Block II, Range includes
: found? true
: (case-insensitive) true
```
```

# 18.5.3 First and Last Positions

The four algorithms in this category are similar to the non-modifying algorithms `std::find` and `std::find_if` that we already discussed in Chapter 17 (Section 17.3.3) but in the current case complexity is logarithmic for random-access iterators and linear otherwise. The complexity of the algorithms in Section 17.3.3 is always linear.

The main functionality is:

+   - Find the first element that has a value not less than a given target value (`lower_bound`).
+   - Return the position of the first element that has a value greater than the target value (`upper_bound`).

An example of use is:

```
```cpp
void Bounds()
{
    std::cout << "\n** Block III, Lower and upper bounds\n";
    // Searching for first and last possible positions.
    // We do not take the option of using a binary predicate.
    std::list<int> myListA
        = { 3, 5, 6, -1, 234, 100, 100, 100, 32, 99, 0, -2 };

    // Default sort is ascending.
    myListA.sort();
    print(myListA, "list, ASC");

    int searchValue = 100;
    std::list<int>::iterator posFirst, posLast;
```
```