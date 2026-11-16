```
std::cout << " (" << gt.comparisons() << " comparisons, "
          << gt.swaps() << " swaps)\\n";
std::cout << "-----------------------------------\\n";

// Make a vector of strings
std::vector<std::string> str_original { "tree", "boy", "apple",
                                        "girl", "dog", "cat" };

// Make a working copy of the original vector
std::vector<std::string> str_working = str_original;
std::cout << "Before: ";
std::cout << str_working << "\\n";
Comparer<std::string> str_lt(less<std::string>),
                      str_gt(greater_than<std::string>);
selection_sort(str_working, str_lt);
std::cout << "Ascending: ";
std::cout << str_working << "\\n";
std::cout << " (" << str_lt.comparisons() << " comparisons, "
          << str_lt.swaps() << " swaps)\\n";
std::cout << "\\n";

// Make another copy of the original vector
str_working = str_original;
std::cout << "Before: ";
std::cout << str_working << "\\n";
selection_sort(str_working, str_gt);
std::cout << "Descending: ";
std::cout << str_working << "\\n";
std::cout << " (" << str_gt.comparisons() << " comparisons, "
          << str_gt.swaps() << " swaps)\\n";
std::cout << "\\n";
}
```

Listing 19.8 (genericstatisticsort.cpp) demonstrates that the generic Comparer class works equally as well with integers and strings:

```
Before: {23,-3,4,215,0,-3,2,23,100,88,-10}
Ascending: {-10,-3,-3,0,2,4,23,23,88,100,215}
(55 comparisons, 7 swaps)
----------------------------------------
Before: {23,-3,4,215,0,-3,2,23,100,88,-10}
Descending: {215,100,88,23,23,4,2,0,-3,-3,-10}
(55 comparisons, 5 swaps)
----------------------------------------
Before: {tree,boy,apple,girl,dog,cat}
Ascending: {apple,boy,cat,dog,girl,tree}
(15 comparisons, 3 swaps)
----------------------------------------
Before: {tree,boy,apple,girl,dog,cat}
Descending: {tree,girl,dog,cat,boy,apple}
(15 comparisons, 4 swaps)
----------------------------------------
```

Recall the IntList linked list class from Listings Listing 18.18 (intlist5.h) and Listing 18.19 (intlist5.cpp). It implemented a linked list of integer elements. Suppose we instead want to make a linked list of std::string