
## lower_bound Algorithm

Line 20 uses the `lower_bound` algorithm to find the first location in a sorted sequence of values at which the third argument could be inserted in the sequence such that the sequence would still be *sorted in ascending order*. The first two iterator arguments must be at least *forward iterators*. The third argument is the value for which to determine the lower bound. The algorithm returns a *forward iterator* pointing to the position at which the insert can occur. A second version of `lower_bound` takes a fourth argument, a *binary predicate function* indicating the order in which the elements were *originally sorted*.

## upper_bound Algorithm

Line 25 uses the `upper_bound` algorithm to find the last location in a sorted sequence of values at which the third argument could be inserted in the sequence such that the sequence would still be sorted in *ascending order*. The first two iterator arguments must be at least *forward iterators*. The third argument is the value for which to determine the upper bound. The algorithm returns a *forward iterator* pointing to the position at which the insert can occur. A second version of `upper_bound` takes a fourth argument, a *binary predicate function* indicating the order in which the elements were *originally sorted*.

## equal_range Algorithm

Line 31 uses the `equal_range` algorithm to return a pair of *forward iterators* containing the results of performing both a `lower_bound` and an `upper_bound` operation. The first two arguments must be at least *forward iterators*. The third is the value for which to locate the equal range. The algorithm returns a pair of *forward iterators* for the lower bound (`eq.first`) and upper bound (`eq.second`), respectively.

## Locating Insertion Points in Sorted Sequences

Algorithms `lower_bound`, `upper_bound` and `equal_range` are often used to locate insertion points in sorted sequences. Line 40 uses `lower_bound` to locate the first point at which 5 can be inserted in order in `a`. Line 47 uses `upper_bound` to locate the last point at which 7 can be inserted in order in `a`. Line 55 uses `equal_range` to locate the first and last points at which 5 can be inserted in order in `a`.

## 16.3.12 Heapsort

Figure 16.12 demonstrates the Standard Library algorithms for performing the **heapsort sorting algorithm**, in which an array of elements is arranged into a data structure called a *heap*. Heapsort is discussed in detail in computer science courses called "Data Structures" and "Algorithms." For more information and additional resources, see:

en.wikipedia.org/wiki/Heapsort

```cpp
// Fig. 16.12: fig16_12.cpp
// Algorithms push_heap, pop_heap, make_heap and sort_heap.
#include <iostream>
#include <algorithm>
#include <array>
#include <vector>
#include <iterator>
using namespace std;

int main()
{
    const size_t SIZE = 10;
    array< int, SIZE > init = { 3, 100, 52, 77, 22, 31, 1, 98, 13, 40 };
    array< int, SIZE > a( init ); // copy of init
    ostream_iterator< int > output( cout, " " );

    cout << "\nArray a before make_heap:\r\n";
    copy( a.cbegin(), a.cend(), output );

    make_heap( a.begin(), a.end() ); // create heap from array a
    cout << "\nArray a after make_heap:\r\n";
    copy( a.cbegin(), a.cend(), output );

    sort_heap( a.begin(), a.end() ); // sort elements with sort_heap
    cout << "\nArray a after sort_heap:\r\n";
    copy( a.cbegin(), a.cend(), output );

    // perform the heapsort with push_heap and pop_heap
    cout << "\nArray init contains:\n";
    copy( init.cbegin(), init.cend(), output ); // display array init
    cout << endl;

    vector< int > v;

    // place elements of array init into v and
    // maintain elements of v in heap
    for ( size_t i = 0; i < SIZE; ++i )
    {
        v.push_back( init[ i ] );
        push_heap( v.begin(), v.end() );
        cout << "\nv after push_heap[" << i << "]: ";
        copy( v.cbegin(), v.cend(), output );
    } // end for

    cout << endl;

    // remove elements from heap in sorted order
    for ( size_t j = 0; j < v.size(); ++j )
    {
        cout << "\nv after " << v[ 0 ] << " popped from heap\n";
        pop_heap( v.begin(), v.end() - j );
        copy( v.cbegin(), v.cend(), output );
    } // end for

    cout << endl;
} // end main
```

Fig. 16.12  |  Algorithms push_heap, pop_heap, make_heap and sort_heap. (Part 1 of 3).

```
Array a before make_heap:
3 100 52 77 22 31 1 98 13 40
Array a after make_heap:
100 98 52 77 40 31 1 3 13 22
Array a after sort_heap:
1 3 13 22 31 40 52 77 98 100

Array init contains: 3 100 52 77 22 31 1 98 13 40

v after push_heap(init[0]): 3
v after push_heap(init[1]): 100 3
v after push_heap(init[2]): 100 3 52
v after push_heap(init[3]): 100 77 52 3
v after push_heap(init[4]): 100 77 52 3 22
v after push_heap(init[5]): 100 77 52 3 22 31
v after push_heap(init[6]): 100 77 52 3 22 31 1
v after push_heap(init[7]): 100 98 52 77 22 31 1 3
v after push_heap(init[8]): 100 98 52 77 22 31 1 3 13
v after push_heap(init[9]): 100 98 52 77 40 31 1 3 13 22

v after 100 popped from heap
98 77 52 22 40 31 1 3 13 100
v after 98 popped from heap
77 40 52 22 13 31 1 3 98 100
v after 77 popped from heap
52 40 31 22 13 3 1 77 98 100
v after 52 popped from heap
40 22 31 1 13 3 52 77 98 100
v after 40 popped from heap
31 22 3 1 13 40 52 77 98 100
v after 31 popped from heap
22 13 3 1 31 40 52 77 98 100
v after 22 popped from heap
13 1 3 22 31 40 52 77 98 100
v after 13 popped from heap
3 1 13 22 31 40 52 77 98 100
v after 3 popped from heap
1 3 13 22 31 40 52 77 98 100
v after 1 popped from heap
1 3 13 22 31 40 52 77 98 100
```

Fig. 16.12 | Algorithms push_heap, pop_heap, make_heap and sort_heap. (Part 3 of 3.)

### make_heap Algorithm

Line 20 uses the **make_heap** algorithm to take a sequence of values in the range from `a.begin()` up to, but not including, `a.end()` and create a heap that can be used to produce a sorted sequence. The two iterator arguments must be *random-access iterators*, so this algorithm will work only with arrays, vectors and deques. A second version of this algorithm takes as a third argument a *binary predicate function for comparing values*.

### sort_heap Algorithm

Line 24 uses the **sort_heap** algorithm to sort a sequence of values in the range from `a.begin()` up to, but not including, `a.end()` that are already arranged in a heap. The two iterator arguments must be *random-access iterators*. A second version of this algorithm takes as a third argument a *binary predicate function for comparing values*.

### push_heap Algorithm

Line 40 uses the `push_heap` algorithm to add a new value into a heap. We take one element of an array `init` at a time, append it to the end of vector `v` and perform the `push_heap` operation. If the appended element is the only element in the vector, the vector is already a heap. Otherwise, `push_heap` rearranges the vector elements into a heap. Each time `push_heap` is called, it assumes that the last element currently in the vector (i.e., the one that's appended before the `push_heap` call) is the element being added to the heap and that all other elements in the vector are already arranged as a heap. The two iterator arguments to `push_heap` must be *random-access iterators*. A second version of this algorithm takes as a third argument a *binary predicate function* for comparing values.

### pop_heap Algorithm

Line 51 uses the `pop_heap` algorithm to remove the *top* heap element. This algorithm assumes that the elements in the range specified by its two *random-access iterator* arguments are already a heap. Repeatedly removing the *top* heap element results in a sorted sequence of values. Algorithm `pop_heap` swaps the first heap element (`v.begin()`) with the last heap element (the element before `v.end() - 1`), then ensures that the elements up to, but not including, the last element still form a heap. Notice in the output that, after the `pop_heap` operations, the vector is *sorted* in ascending order. A second version of this algorithm takes as a third argument a *binary predicate function* for comparing values.

### C++11: is_heap and is_heap_until Algorithms

In addition to the `make_heap`, `sort_heap`, `push_heap` and `pop_heap` algorithms presented in Fig. 16.12, C++11 now includes the new algorithms `is_heap` and `is_heap_until`. The `is_heap` algorithm returns `true` if the elements in the specified range represent a heap. A second version of this algorithm takes as a third argument a *binary predicate function* for comparing values.

The `is_heap_until` algorithm checks the specified range of values and returns an iterator pointing to the last item in the range for which the elements up to, but not including, that iterator represent a heap.

## 16.3.13 min, max, minmax and minmax_element

Figure 16.13 demonstrates algorithms `min`, `max`, `minmax` and `minmax_element`.

```cpp
// Fig. 16.13: fig16_13.cpp
// Algorithms min, max, minmax and minmax_element.
#include <iostream>
#include <array>
#include <algorithm>
using namespace std;

int main()
{
    cout << "The minimum of 12 and 7 is: " << min(12, 7);
    cout << "\nThe maximum of 12 and 7 is: " << max(12, 7);
    cout << "\nThe minimum of 'G' and 'Z' is: " << min('G', 'Z');
```

**Fig. 16.13** | Algorithms min, max, minmax and minmax_element. (Part 1 of 2.)
