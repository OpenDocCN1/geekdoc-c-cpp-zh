```
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

# 18.6.2 next() and prev()

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