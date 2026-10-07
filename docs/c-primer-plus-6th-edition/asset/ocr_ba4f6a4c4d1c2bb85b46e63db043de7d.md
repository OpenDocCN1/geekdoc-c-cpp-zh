# for_each()

```
template<class InputIterator, class Function>
Function_for_each(InputIterator first, InputIterator last,
                    Function f);
```

The for_each() function applies function f to each element in the range [first, last). It also returns f.

# find()

```
template<class InputIterator, class T>
InputIterator find(InputIterator first, InputIterator last,
                    const T& value);
```

The find() function returns an iterator to the first element in the range [first, last) that has the value; it returns last if the item is not found.

# find_if()

```
template<class InputIterator, class Predicate>
InputIterator find_if(InputIterator first, InputIterator last,
                    Predicate pred);
```

The find_if() function returns an iterator to the first element in the range [first, last) for which the function object calls pred(*i) is true; it returns last if the item is not found.

# find_if_not()

```
template<class InputIterator, class Predicate>
InputIterator find_if_not(InputIterator first, InputIterator last,
                    Predicate pred);
```

The find_if_not() function returns an iterator, to the first element in the range [first, last] for which the function object calls pred(*i) is false; it returns last if the item is not found.

# find_end()

```
template<class ForwardIterator1, class ForwardIterator2>
ForwardIterator1 find_end(ForwardIterator1 first1, ForwardIterator1 last1,
                    ForwardIterator2 first2, ForwardIterator2 last2);
```

```
template<class ForwardIterator, class BinaryPredicate>
ForwardIterator find_end(ForwardIterator first1, ForwardIterator1 last1,
                    ForwardIterator2 first2, ForwardIterator2 last2,
                    BinaryPredicate pred);
```