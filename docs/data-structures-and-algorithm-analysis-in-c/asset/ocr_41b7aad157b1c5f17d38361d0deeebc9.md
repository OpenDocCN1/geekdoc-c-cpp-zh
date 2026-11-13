```
/**
 * Simple insertion sort.
 */
template <typename Comparable>
void insertionSort( vector<Comparable> & a )
{
    for( int p = 1; p < a.size( ); ++p )
    {
        Comparable tmp = std::move( a [ p ] );

        int j;
        for( j = p; j > 0 && tmp < a [ j - 1 ]; --j )
            a [ j ] = std::move( a [ j - 1 ] );
        a [ j ] = std::move( tmp );
    }
}
```

# Figure 7.2 Insertion sort routine

# 7.2.2 STL Implementation of Insertion Sort

In the STL, instead of having the sort routines take an array of comparable items as a single parameter, the sort routines receive a pair of iterators that represent the start and endmarker of a range. A two-parameter sort routine uses just that pair of iterators and presumes that the items can be ordered, while a three-parameter sort routine has a function object as a third parameter.

Converting the algorithm in Figure 7.2 to use the STL introduces several issues. The obvious issues are

+   1. We must write a two-parameter sort and a three-parameter sort. Presumably, the two-parameter sort invokes the three-parameter sort, with `less<Object>{ }` as the third parameter.
+   2. Array access must be converted to iterator access.
+   3. Line 11 of the original code requires that we create tmp, which in the new code will have type `Object`.

The first issue is the trickiest because the template type parameters (i.e., the generic types for the two-parameter sort are both Iterator; however, Object is not one of the generic type parameters. Prior to C++11, one had to write extra routines to solve this problem. As shown in Figure 7.3, C++11 introduces decltype which cleanly expresses the intent.

Figure 7.4 shows the main sorting code that replaces array indexing with use of the iterator, and that replaces calls to operator< with calls to the less than function object.

Observe that once we actually code the InsertionSort algorithm, every statement in the original code is replaced with a corresponding statement in the new code that makes