
sample case, this parameter N was the number of array elements to be searched. Not surprisingly, it takes longer to search a larger number of array elements than it does to search a smaller number of array elements. Big-O running-time estimates are always expressed as a function of the size of the problem. In this chapter, all our algorithms will involve a range of values in some container. In all cases N will be the number of elements in that range.

> The following is an alternative, pragmatic way to think about big-O estimates:
> Only look at the term with the highest exponent and do not pay attention to constant multiples.

For example, all of the following are O(N²):

N² + 2N + 1,  3N² + 7,  100N² + N

All of the following are O(N³):

N³ + 5N² + N + 1,  8N³ + 7,  100N³ + 4N + 1

These big-O running-time estimates are admittedly crude, but they do contain some information. They will not distinguish between a running time of 5N + 5 and a running time of 100N, but they do let us distinguish between some running times and so determine that some algorithms are faster than others. Look at the graphs in Display 19.15 and notice that all the graphs for functions that are O(N) eventually fall below the graph for the function 0.5N². The result is inevitable: An O(N) algorithm will always run faster than any O(N²) algorithm, provided we use large enough values of N. Although an O(N²) algorithm could be faster than an O(N) algorithm for the problem size you are handling, programmers have found that, in practice, O(N) algorithms perform better than O(N²) algorithms for most practical applications that are intuitively “large.” Similar remarks apply to any other two different big-O running times.

Some terminology will help with the descriptions of generic algorithm running times. Linear running time means a running time of T(N) = aN + b. A linear running time is always an O(N) running time. Quadratic running time means a running time with a highest term of N². A quadratic running time is always an O(N²) running time. We will also occasionally have logarithms in running-time formulas. Those normally are given without any base, since changing the base is just a constant multiple. If you see log N, think log base 2 of N, but it would not be wrong to think log base 10 of N. Logarithms are very slow growing functions. So, a O(log N) running time is very fast.

In many cases, our running-time estimates will be better than big-O estimates. In particular, when we specify a linear running time, that is a tight upper bound and you can think of the running time as being exactly T(N) = cN, although the c is still not specified.

## Display 19.15  **Comparison of Running Times**

![](img/9505fd46e120aa9c1406715936ff6251_814_0.png)

## ■  CONTAINER ACCESS RUNNING TIMES

Now that we know about big-O notation, we can express the efficiency of some of the accessing functions for container classes which we discussed in Section 19.2. Insertions at the back of a vector (push_back), the front or back of a deque (push_back and push_front), and anywhere in a list (insert) are all $O(1)$ (that is, a constant upper bound on the running time that is independent of the size of the container). Insertion or deletion of an arbitrary element for a vector or deque is $O(N)$ where $N$ is the number of elements in the container. For a set or map, finding (find) is $O(\log N)$ where $N$ is the number of elements in the container.

## Self-Test Exercises

- 17. Show that a running time \(T(N)=aN+b\) is an \(O(N)\) running time. (Hint: The only issue is the plus. Assume \(N\) is always at least 1.)
- 18. Show that for any two bases \(a\) and \(b\) for logarithms, if \(a\) and \(b\) are both greater than 1, then there is a constant \(c\) such that \(\log_a N \le c(\log_b N)\). Thus, there is no need to specify a base in \(O(\log N)\). That is, \(O(\log_a N)\) and \(O(\log_b N)\) mean the same thing.

## NONMODIFYING SEQUENCE ALGORITHMS

This section describes template functions that operate on containers but do not modify the contents of the container in any way. A good simple and typical example is the generic find function.

The generic find function is similar to the find member function of the set template class but is a different function. The generic find function can be used with any of the STL sequence container classes. Display 19.16 shows a sample use of the generic find function used with the class vector<char>. The function in Display 19.16 would behave exactly the same if we replaced vector<char> by list<char> throughout, or if we replaced vector<char> by any other sequence container class. That is one of the reasons why the functions are called generic: One definition of the find function works for a wide selection of containers.

If the find function does not find the element it is looking for, it returns its second iterator argument, which need not be equal to some end() as it is in Display 19.16. Sample Dialogue 2 in that display shows the situation when find does not find what it is looking for.

Does find work with absolutely any container? No, not quite. To start with, it takes iterators as arguments, and some containers, such as stack, do not have iterators. To use the find function, the container must have iterators, the elements must be stored in a linear sequence so that the ++ operator moves iterators through the container, and the elements must be comparable using ==. In other words, the container must have forward iterators (or some stronger kind of iterators, such as bidirectional iterators).

When presenting generic function templates, we will describe the iterator type parameter by using the name of the required kind of iterator as the type parameter name. So, ForwardIterator should be replaced by a type that is a type for some kind of forward iterator, such as the iterator type in a list, vector, or other container template class. Remember, a bidirectional iterator is also a forward iterator, and a random-access iterator is also a bidirectional iterator. Thus, the type name ForwardIterator can be used with any iterator type that is a bidirectional or random-access iterator type as well as a plain-old forward iterator type. In some cases when we specify ForwardIterator, you

can use an even simpler iterator kind, namely, an input iterator or output iterator. Because we have not discussed input and output iterators, however, we do not mention them in our function template declarations.

Remember that the names *forward iterator*, *bidirectional iterator*, and *random-access iterator* refer to kinds of iterators, not type names. The actual type names will be something like `std::vector<int>::iterator`, which in this case happens to be a random-access iterator.

Display 19.17 gives a sample of some nonmodifying generic functions in the STL. Display 19.17 uses a notation that is common when discussing container iterators. The iterator locations encountered in moving from an iterator first to, but not including, an iterator last are called the **range [first, last)**. For example, the following for loop outputs all the elements in the range [first, last):

```
for (iterator p = first; p != last; p++)
    cout << *p << endl;
```

Note that when two ranges are given, they need not be in the same container or even the same type of container. For example, for the search function, the ranges [first1, last1) and [first2, last2) may be in the same or different containers.

## Display 19.16  **The Generic find Function (part 2 of 2)**

### SAMPLE DIALOGUE 1

> ```text
> Enter a line of text
> A line of text.
> You entered the following before you entered your first e:
> A lin
> You entered the following after that:
> e of text.
> End of demonstration.
> ```

### SAMPLE DIALOGUE 2

> ```text
> Enter a line of text
> I will not!
> You entered the following before you entered your first e:
> I will not!
> You entered the following after that:
> 
> End of demonstration.
> ```
> 
> *If find does not find what it is looking for, it returns `line.end()`.*
