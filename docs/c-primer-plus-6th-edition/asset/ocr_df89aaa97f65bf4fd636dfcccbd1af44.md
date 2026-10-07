# STL Functions 1293

pred to compare elements. That is, elements pointed to by it1 and it2 match ifnpred(*it1, *it2) is true.

# search_n()

```
template<class ForwardIterator, class Size, class T>
ForwardIterator search_n(ForwardIterator first, ForwardIterator last,
    Size count, const T& value);
```

```
template<class ForwardIterator, class Size, class T, class BinaryPredicate>
ForwardIterator search_n(ForwardIterator first, ForwardIterator last,
    Size count, const T& value, BinaryPredicate pred);
```

The search_n() function finds the first occurrence in the range [first, last) that
matches the sequence consisting of count consecutive occurrences of value. It returns
last if no such sequence is found. The == operator for the value
type compare elements. The second version uses the binary predicate function
pred compare elements. That is, elements pointed to by it1 and it2 match if
pred(*it1, *it2) is true.

# Mutating Sequence Operations

Table G.14 summarizes the mutating sequence operations. Arguments are not shown, and
overloaded functions are listed just once. A fuller description, including the prototypes,
follows the them. You can scan the table to get an idea of what a function does and
then look up the details if you find the function appealing.

Now let's take a more detailed look at these mutating sequence operations. For each
function, the discussion shows the prototype(s), followed by a brief explanation. As you
saw earlier, pairs of iterators indicates, with the chosen parameter name
identifying the type of iterator. Using a range in the form [first, last) goes from
first up to, but not including, last. Functions passed as arguments are function objects,
which can be function pointers or objects for which the () operation is defined. As in
Chapter 16, a predicate is a Boolean function with one argument, and a binary predicate
with two arguments. (The functions need not be type bool, as
return zero for false and a nonzero value of true.) Also as in Chapter 16, a unary
function object is one that takes a single argument, and a binary function object is one
that two arguments.

# copy()

```
template<class InputIterator, class OutputIterator>
OutputIterator copy(InputIterator first, InputIterator last,
    OutputIterator result);
```

The copy() function copies the elements in the range [first, last) into the range
[result, result + (last - first)). It returns result + (last - first)—that is,