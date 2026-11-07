
Listing 16.16 incorporates some of the recent examples into a short program.

### Listing 16.16 funadap.cpp

```
    // funadap.cpp -- using function adapters
    #include <iostream>
    #include <vector>
    #include <iterator>
    #include <algorithm>
    #include <functional>

    void Show(double);
    const int LIM = 6;
    int main()
    {
        using namespace std;
        double arr1[LIM] = {28, 29, 30, 35, 38, 59};
        double arr2[LIM] = {63, 65, 69, 75, 80, 99};
        vector<double> gr8(arr1, arr1 + LIM);
        vector<double> m8(arr2, arr2 + LIM);
        cout.setf(ios_base::fixed);
        cout.precision(1);
        cout << "gr8:\t";
        for_each(gr8.begin(), gr8.end(), Show);
        cout << endl;
        cout << "m8: \t";
        for_each(m8.begin(), m8.end(), Show);
        cout << endl;

        vector<double> sum(LIM);
        transform(gr8.begin(), gr8.end(), m8.begin(), sum.begin(),
                  plus<double>());
        cout << "sum:\t";
        for_each(sum.begin(), sum.end(), Show);
        cout << endl;

        vector<double> prod(LIM);
        transform(gr8.begin(), gr8.end(), prod.begin(),
                  bind1st(multiplies<double>(), 2.5));
        cout << "prod:\t";
        for_each(prod.begin(), prod.end(), Show);
        cout << endl;

        return 0;
    }

    void Show(double v)
    {
        std::cout.width(6);
        std::cout << v << ' ';
    }
```

Here is the output of the program in Listing 16.16:

```
    gr8:    28.0   29.0   30.0   35.0   38.0   59.0
    m8:     63.0   65.0   69.0   75.0   80.0   99.0
    sum:    91.0   94.0   99.0  110.0  118.0  158.0
    prod:   70.0   72.5   75.0   87.5   95.0  147.5
```

C++11 provides an alternative to function pointers and functors. It's called a *lambda expression*, another topic discussed in Chapter 18.

## Algorithms

The STL contains many nonmember functions for working with containers. You've seen a few of them already: `sort()`, `copy()`, `find()`, `for_each()`, `random_shuffle()`, `set_union()`, `set_intersection()`, `set_difference()`, and `transform()`. You've probably noticed that they feature the same overall design, using iterators to identify data ranges to be processed and to identify where results are to go. Some also take a function object argument to be used as part of the data processing.

There are two main generic components to the algorithm function designs. First, they use templates to provide generic types. Second, they use iterators to provide a generic representation for accessing data in a container. Thus, the `copy()` function can work with a container that holds type double values in an array, with a container that holds string values in a linked list, or with a container that stores user-defined objects in a tree structure, such as is used by `set`. Because pointers are a special case of iterators, STL functions such as `copy()` can be used with ordinary arrays.

The uniform container design allows meaningful relationships between containers of different kinds. For example, you can use `copy()` to copy values from an ordinary array to a vector object, from a vector object to a list object, and from a list object to a `set` object. You can use `==` to compare different kinds of containers—for example, `deque` and `vector`. This is possible because the overloaded `==` operator for containers uses iterators to compare contents, so a `deque` object and a `vector` object test as equal if they have the same content in the same order.

### Algorithm Groups

The STL divides the algorithm library into four groups:

- Nonmodifying sequence operations
- Mutating sequence operations
- Sorting and related operations
- Generalized numeric operations

The first three groups are described in the algorithm (formerly algo.h) header file, and the fourth group, being specifically oriented toward numeric data, gets its own header file, called numeric. (Formerly, they, too, were in algo.h.)

Nonmodifying sequence operations operate on each element in a range. These operations leave a container unchanged. For example, find() and for_each() belong to this category.

Mutating sequence operations also operate on each element in a range. As the name suggests, however, they can mutate, or change, the contents of a container. The change could be in values or in the order in which the values are stored. The transform(), random_shuffle(), and copy() functions fall into this category.

Sorting and related operations include several sorting functions (including sort()) and a variety of other functions, including the set operations.

The numeric operations include functions to sum the contents of a range, calculate the inner product of two containers, calculate partial sums, and calculate adjacent differences. Typically, these are operations that are characteristic of arrays, so vector is the container most likely to be used with them.

Appendix G provides a complete summary of these functions.

### General Properties of Algorithms

As you've seen again and again in this chapter, STL functions work with iterators and iterator ranges. The function prototype indicates the assumptions made about the iterators. For example, the copy() function has this prototype:

```
template<class InputIterator, class OutputIterator>
OutputIterator copy(InputIterator first, InputIterator last,
                    OutputIterator result);
```

Because the identifiers InputIterator and OutputIterator are template parameters, they just as easily could have been T and U. However, the STL documentation uses the template parameter names to indicate the concept that the parameter models. So this declaration tells you that the range parameters must be input iterators or better and that the iterator indicating where the result goes must be an output iterator or better.

One way of classifying algorithms is on the basis of where the result of the algorithm is placed. Some algorithms do their work in place, and others create copies. For example, when the sort() function is finished, the result occupies the same location that the original data did. So sort() is an in-place algorithm. The copy() function, however, sends the result of its work to another location, so it is a copying algorithm. The transform() function can do both. Like copy(), it uses an output iterator to indicate where the results go. Unlike copy(), transform() allows the output iterator to point to a location in the input range, so it can copy the transformed values over the original values.

Some algorithms come in two versions: an in-place version and a copying version. The STL convention is to append _copy to the name of the copying version. The latter version takes an additional output iterator parameter to specify the location to which to copy the outcome. For example, there is a replace() function that has this prototype:

```
template<class ForwardIterator, class T>
void replace(ForwardIterator first, ForwardIterator last,
             const T& old_value, const T& new_value);
```

It replaces each instance of old_value with new_value. This occurs in place. Because this algorithm both reads from and writes to container elements, the iterator type has to be ForwardIterator or better. The copying version has this prototype:

```
template<class InputIterator, class OutputIterator, class T>
OutputIterator replace_copy(InputIterator first, InputIterator last,
                            OutputIterator result,
                            const T& old_value, const T& new_value);
```

This time the resulting data is copied to a new location, given by result, so the read-only input iterator is sufficient for specifying the range.

Note that replace_copy() has an OutputIterator return type. The convention for copying algorithms is that they return an iterator pointing to the location one past the last value copied.

Another common variation is that some functions have a version that performs an action conditionally, depending on the result of applying a function to a container element. These versions typically append _if to the function name. For example, replace_if() replaces an old value with a new value if applying a function to the old value returns the value true. Here's the prototype:

```
template<class ForwardIterator, class Predicate, class T>
void replace_if(ForwardIterator first, ForwardIterator last,
                Predicate pred, const T& new_value);
```

(Recall that a predicate is a unary function that returns a bool value.) There's also a version called replace_copy_if(). You can probably figure out what it does and what its prototype is like.

As with InputIterator, Predicate is a template parameter name and could just as easily be called T or U. However, the STL chooses to use Predicate to remind the user that the actual argument should be a model of the Predicate concept. Similarly, the STL uses terms such as Generator and BinaryPredicate to identify arguments that should model other function object concepts. Keep in mind that although the documentation can remind you what the iterator or functor requirements are, these names are not something the compiler can check. If you use the wrong sort of iterator, you can expect to see a long list of error messages as the compiler tries to instantiate the template.
