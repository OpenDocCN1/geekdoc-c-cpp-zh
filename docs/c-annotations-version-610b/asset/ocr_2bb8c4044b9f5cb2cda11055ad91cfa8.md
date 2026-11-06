```
~~~cpp
        {
            return !strcasecmp(first.c_str(), second.c_str());
        }
    };
    int main()
    {
        string first[] =
        {
            "Alpha", "bravo", "Charley", "delta", "Echo",
            "foxtrot", "Golf", "hotel"
        };
        string second[] =
        {
            "alpha", "bravo", "charley", "delta", "echo",
            "foxtrot", "golf", "hotel"
        };
        string *last = first + sizeof(first) / sizeof(string);

        cout << "The elements of `first' and `second' are pairwise " <<
            (equal(first, last, second) ? "equal" : "not equal") <<
            '\n' <<
            "compared case-insensitively, they are " <<
            (
                equal(first, last, second, CaseString()) ?
                    "equal" : "not equal"
            ) << '\n';
    }
    /*
    Displays:
        The elements of `first' and `second' are pairwise not equal
        compared case-insensitively, they are equal
    */
~~~
```

# ## 19.1.10 equal_range

+   - Header file: `<algorithm>`
+   - Function prototypes:
+       - `pair<ForwardIterator, ForwardIterator> equal_range(ForwardIterator first, ForwardIterator last, Type const &value);`
+       - `pair<ForwardIterator, ForwardIterator> equal_range(ForwardIterator first, ForwardIterator last, Type const &value, Compare comp);`
+   - Description (see also identically named member functions of, e.g., the map (section 12.3.6) and multimap (section 12.3.7)):
+       - The first prototype: starting from a sorted sequence (where the `operator<` of the data type to which the iterators point was used to sort the elements in the provided range), a pair of iterators is returned representing the return value of, respectively, `lower_bound` (returning the first element that is not smaller than the provided reference value, see section 19.1.25) and `upper_bound` (returning the first element beyond the provided reference value, see section 19.1.66).
+       - The second prototype: starting from a sorted sequence (where the `comp` function object was used to sort the elements in the provided range), a pair of iterators is returned representing the return values of, respectively, the functions `lower_bound` (section 19.1.25) and `upper_bound` (section 19.1.66).