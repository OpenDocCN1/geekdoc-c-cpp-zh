
```
posFirst = std::lower_bound(myListA.begin(), myListA.end(),
    searchValue);
posLast = std::upper_bound(myListA.begin(), myListA.end(),
    searchValue);

std::cout << "Value " << searchValue << " position "
    << distance(myListA.begin(), posFirst) + 1
    << " up to " << distance(myListA.begin(), posLast) + 1
    << " contiguously" << std::endl;
}
```

The output is:

```
** Block III, Lower and upper bounds
list, ASC -2, -1, 0, 3, 5, 6, 32, 99, 100, 100, 100, 234,
Value 100 position 9 up to 12 contiguously
```

In order to obtain the result from both the lower bound and the upper bound algorithms and return them as a pair, we use the std::equal_range algorithm that we now discuss.

## 18.5.4 First and Last Possible Positions as a Pair

Both algorithms in this category return the range of elements whose value is equal to a target value. The range contains the first position and the last position of an element whose value could be inserted without breaking the sorting order. In other words, the range is the closed-open interval [begin, end).

```
void EqualRanges()
{
    std::cout << "\n** Block IV, Equal ranges\n";
    std::list<int> myListA = { 3,5,6,-1,234,100,100,100,32,6,99,0,
        -2,6,6 };

    int searchValue = 6;
    print(myListA, "list, unsorted");
    myListA.sort();
    print(myListA, "list, sorted");

    // Find the range of values that contain a given value.
    typedef std::list<int>::iterator it;
    std::pair<it, it> range
        = equal_range(myListA.begin(),
            myListA.end(), searchValue);

    std::cout << "Value " << searchValue
        << " lies in OFFSET closed-open range ["
        << distance(myListA.begin(), range.first)
        << "," << distance(myListA.begin(), range.second)
        << "]" << std::endl;
}
```

The output is:

```
** Block IV, Equal ranges
list, unsorted 3,5,6,-1,234,100,100,100,32,6,99,0,-2,6,6,
list, sorted -2,-1, 0, 3, 5, 6, 6, 6, 6, 32, 99, 100, 100, 100, 234,
Value 6 lies in OFFSET closed-open range [5,9)
```

## 18.5.5 Merging

The algorithms in this category merge two ranges in a number of ways:

- Merge two source ranges into a destination range.
- Set operations on set-like containers: union, intersection, difference, symmetric difference (‘Venn diagram stuff’).

An example of using the first algorithm is:

```
void Merge()
{
    std::cout << "\n** Block V, Merge\n";
    std::list<int> myListA = { 3,5,6,1,2,3 };
    std::list<int> myListB = { -3,-5,-6,1,2,3 };

    myListA.sort(); myListB.sort();
    print(myListA, "List A");
    print(myListB, "List B");
    std::list<int> mergedList;
    std::merge(myListA.begin(), myListA.end(), myListB.begin(),
               myListB.end(),
               std::front_insert_iterator<std::list<int>>(mergedList));
    print(mergedList, "Merged list front insert");

    std::list<int> mergedListII;
    std::merge(myListA.begin(), myListA.end(), myListB.begin(), myListB.end(),
               std::back_insert_iterator<std::list<int>>(mergedListII));
    print(mergedListII, "Merged list back insert");
}
```

The output is:

```
** Block V, Merge
List A 1, 2, 3, 3, 5, 6,
List B -6, -5, -3, 1, 2, 3,
Merged list front insert 6, 5, 3, 3, 3, 2, 2, 1, 1, -3, -5, -6,
Merged list back insert -6, -5, -3, 1, 1, 2, 2, 3, 3, 3, 5, 6,
```

We give a final example to show how to compute the union and intersection of two sets:

```
void SetUnion()
{ // Union etc. of sets
std::cout << "\n** Block VI, Union\n";
std::set<int> v1 = { 1, 2, 3, 4, 5 };
std::set<int> v2 = { 3, 4, 5, 6, 7 };
std::vector<int> dest;

std::set_union(std::begin(v1), std::end(v1),
               std::begin(v2), std::end(v2),
               std::back_inserter(dest));

for (auto e : dest) { std::cout << e << ", "; }

dest.clear();
std::set_intersection(std::begin(v1), std::end(v1),
                      std::begin(v2), std::end(v2),
                      std::back_inserter(dest));

std::cout << '\n';
for (auto e : dest) { std::cout << e << ", "; }
}
```

The output is:

```
** Block VI, Union
1, 2, 3, 4, 5, 6, 7,
3, 4, 5,
```

Finally, we recall that the algorithms in Exercise 2 of Chapter 17 can be used to test whether a range is sorted.

## 18.6 AUXILIARY ITERATOR FUNCTIONS

For completeness, we discuss a number of auxiliary functions that deal with iterators and that are useful when using and extending STL algorithms. In particular, the distance() algorithm is important and useful.

The algorithms solve the following problems:

- Advance the position of an iterator by a positive or negative offset.
- Helper functions to move to the next or previous iterator positions.
- Find the difference between two iterators.
- Swap the values to which two iterators refer.

### 18.6.1 advance()

This algorithm increments the position of an iterator that is passed as an argument. The iterator is allowed to step forward or backward:

```
void Advance()
{
using List = std::list<int>;
List myList{ 1, 2, 3, 4, 5, 6 };

// advance()
auto pos = myList.begin();  // 1
std::cout << *pos << '\n';

std::advance(pos, 3);      // 4
std::cout << *pos << '\n';
std::advance(pos, -1);     // 3
std::cout << *pos << '\n';

// In general, advancing outside container
// results in undefined behaviour
pos = myList.begin();
std::advance(pos, 8);      // I get '2'
std::cout << *pos << '\n';
}
```

The output is:

```
**** Block I, advance() ****
1,4,3,2,
```

The algorithm does not check whether it crosses the end of a sequence; in such cases the result leads to undefined behaviour. Complexity is constant for random-access iterators and it is linear for other iterators.

### 18.6.2 next() and prev()

These helper functions are used to move to subsequent or previous iterator positions. They can be used to check the values of next or previous elements when iterating in a range. They can also be used to simplify the pre- and post-increment operators associated with iterators:

```
void NextPrev()
{
    // prev() left as an exercise!

    std::cout << "\n**** Block II, next() and prev() ****\n";
    using List = std::list<int>;
    List myList{ 1, 2, 3, 4, 5, 6 };

    // advance()
    auto pos = myList.begin();      // 1
    std::cout << *pos << ",";
    while (pos != std::end(myList) && std::next(pos) != std::end(myList))
    {
        ++pos;
        std::cout << *pos << ",";
    }
}
```

The output is:

```
**** Block II, next() and prev() ****
1,2,3,4,5,6,
```

As with advance(), next() does not check whether it has crossed the end of a sequence nor does prev() check whether it has crossed the beginning of a sequence.

### 18.6.3 distance()

This function computes the difference between two iterators. For random-access iterators the value is the difference of the iterators and it has constant complexity. For other iterators the complexity is linear. For this reason it is advisable not to use this function with non-random-access iterators:

```
void Distance()
{
    std::cout << "\n**** Block III, distance() ****\n";

    using List = std::list<int>;
    List myList{ 1, 2, 3, 4, 5, 6 };

    auto pos2 = std::find(std::begin(myList), std::end(myList), 3);
    std::cout << std::distance(std::begin(myList), pos2) << '\n';      // 2

    auto pos3 = std::find(pos2, std::end(myList), 6);
    if (pos3 != std::end(myList))
    {
        std::cout << std::distance(pos2, pos3) << '\n';                // 3
    }

    auto pos4 = std::find(std::begin(myList), std::end(myList), 6);
    std::cout << std::distance(std::begin(myList), pos4) << '\n';// 5

    auto pos5 = std::find(std::begin(myList), std::end(myList), 1);
    std::cout << std::distance(std::begin(myList), pos5) << '\n';      // 0
}
```

The output is:

```
**** Block III, distance() ****
2
3
5
0
```

### 18.6.4 iter_swap()

This function swaps the values to which two iterators refer:

```
void IterSwap()
{
    std::cout << "\n**** Block IV, iter_swap() ****\n";
    // 101 examples
    int* j = new int; int* i = new int;
    *j = 1; *i = 2;
    std::cout << "Before swap: " << *i << ", " << *j << '\n';
    std::iter_swap(j, i);
    std::cout << "After swap: " << *i << ", " << *j << '\n';
    delete j; delete i;

    // Part 2
    std::vector<int> v1 = { 0,1 };
    std::vector<bool> v2 = { true, false };

    print(v1, "v1");
    print(v2, "v2");
    std::iter_swap(std::begin(v1), std::begin(v1) + 1);
    std::iter_swap(std::begin(v2), std::begin(v2) + 1);
    print(v1, "v1");
    print(v2, "v2");
}
```

The output is:

```
**** Block IV, iter_swap() ****
Before swap: 2, 1
After swap: 1, 2

v1 0, 1,
v2 true, false,

v1 1, 0,
false, true,
```

## 18.7 NEEDLE IN A HAYSTACK: FINDING THE RIGHT STL ALGORITHM

We have now completed our discussion of STL algorithms. In this section we provide some rules to help find the most suitable algorithm or combination of algorithms that realise a given requirement. First, it is important to know what the problem is and what the requirements are (for example, efficiency, interoperability with your current software frameworks and maintainability). Second, we determine which category (for example, the sorted range algorithms) the requirement belongs to and then we determine which specific algorithm in the category realises the requirement. Some general questions are:

- A1: What is the most suitable container?
- A2: What are the typical operations to be performed on the container?
