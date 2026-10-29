
we know that no matter what the exact running time of each different operation may turn out to be, there will always be some constant factor c such that the real running time is less than or equal to
c (6N + 5)

Under these circumstances, we say that the code (or program or algorithm) runs in time O(6N + 5). This is usually read as "big-O of 6N + 5." We need not know what the constant c will be. In fact, it will undoubtedly be different for different computers, but we must know that there is one such c for any reasonable computer system. If the computer is very fast, the c might be less than 1—say, 0.001. If the computer is very slow, the c might be very large—say, 1000. Moreover, since changing the units (say from nanosecond to second) involves only a constant multiple, there is no need to give any units of time.

Be sure to notice that a big-O estimate is an upper-bound estimate. We always approximate by taking numbers on the high side rather than the low side of the true count. Also notice that when performing a big-O estimate, we need not determine an exact count of the number of operations performed. We need only an estimate that is correct up to a constant multiple. If our estimate is twice as large as the true number, that is good enough.

An order-of-magnitude estimate, such as the previous 6N + 5, contains a parameter for the size of the task solved by the algorithm (or program or piece of code). In our sample case, this parameter N was the number of array elements to be searched. Not surprisingly, it takes longer to search a larger number of array elements than it does to search a smaller number of array elements. Big-O running-time estimates are always expressed as a function of the size of the problem. In this chapter, all our algorithms will involve a range of values in some container. In all cases, N will be the number of elements in that range.

The following is an alternative, pragmatic way to think about big-O estimates:

> Look only at the term with the highest exponent and do not pay attention to constant multiples.

For example, all of the following are O(N²):
N² + 2N + 1, 3N² + 7, 100N² + N

All of the following are O(N³):
N³ + 5N² + N + 1, 8N³ + 7, 100N³ + 14N + 1

These big-O running-time estimates are admittedly crude, but they do contain some information. They will not distinguish between a running time of 5N + 5 and a running time of 100N, but they do let us distinguish between some running times and so determine that some algorithms are faster than others. Look at the graphs in Display 19.16 and notice that all the graphs for functions that are O(N) eventually fall below the graph for the function 0.5N². The result is inevitable: An O(N) algorithm will always run faster than any O(N²) algorithm, provided we use large enough values of N. Although an O(N²) algorithm could be faster than an O(N) algorithm for the problem size you are handling, programmers have found that, in practice, O(N) algorithms perform better than O(N) algorithms for most practical applications that are intuitively "large." Similar remarks apply to any other two different big-O running times.

## Display 19.16 Comparison of Running Times

![](img/c76bba8c1d927f399768ffe2ab5f5bee_932_0.png)

Some terminology will help with our descriptions of generic algorithm running times. Linear running time means a running time of T(N) = aN + b. A linear running time is always an O(N) running time. Quadratic running time means a running time with a highest term of N². A quadratic running time is always an O(N²) running time.

We will also occasionally have logarithms in running-time formulas. Those normally are given without any base, since changing the base is just a constant multiple. If you see log N, think log base 2 of N, but it would not be wrong to think log base 10 of N. Logarithms are very slow-growing functions. So, an O(log N) running time is very fast.

In many cases, our running-time estimates will be better than big-O estimates. In particular, when we specify a linear running time, that is a tight upper bound; you can think of the running time as being exactly T(N) = cN, although the c is still not specified.

## Container Access Running Times

Now that we know about big-O notation, we can express the efficiency of some of the accessing functions for container classes that we discussed in Section 19.2. Insertions at the back of a vector (push_back), the front or back of a deque (push_back and

linear running time

quadratic running time

## Display 19.17　The Generic find Function (part 2 of 2)

```
cout << "Enter a line of text:\n";
char next;
cin.get(next);
while (next != '\n')
{
    line.push_back(next);
    cin.get(next);
}

vector<char>::const_iterator where;
where = find(line.begin(), line.end(), 'e');
//where is located at the first occurrence of 'e' in v.

vector<char>::const_iterator p;
cout << "You entered the following before you" 
     << " entered your first line:\n";
for (p = line.begin(); p != where; p++)
    cout << *p;
cout << endl;

cout << "You entered the following after that:\n";
for (p = where; p != line.end(); p++)
    cout << *p;
cout << endl;

cout << "End of demonstration.\n";
return 0;
}
```

## Sample Dialogue 1

> ```text
> Enter a line of text
> A line of text.
> You entered the following before you entered your first e:
> A lin
> You entered the following after that:
> e of text.
> End of demonstration.
> ```

## Sample Dialogue 2

> ```text
> Enter a line of text
> I will not!
> You entered the following before you entered your first e:
> I will not!
> You entered the following after that:
> 
> End of demonstration.
> ```

## Range [first, last)

The movement from some iterator first, often container.begin(), up to but not including some location last, often container.end(), is so common that it has come to have a special name, range [first, last). For example, the following code outputs all elements in the range [c.begin(), c.end()), where c is some container object, such as a vector:

```
for (iterator p = c.begin(); p != c.end(); p++)
    cout << *p << endl;
```

Note that with the binary_search function, you are guaranteed that the implementation will use the binary search algorithm, which was discussed in Chapter 13. The importance of using the binary search algorithm is that it guarantees a very fast running time, O(log N). If you have not read Chapter 13 and have not otherwise heard of a binary search, just think of it as a very efficient search algorithm that requires that the elements be sorted. Those are the only two points about binary searches that are relevant to the material in this chapter.

## Display 19.18   Some Nonmodifying Generic Functions (part 1 of 2)

```
These functions all work for forward iterators, which means they also work for bidirectional and random-access iterators. (In some cases, they even work for other kinds of iterators that we have not covered in any detail.)

template <class ForwardIterator, class T>
ForwardIterator find(ForwardIterator first, ForwardIterator last,
                     const T& target);
//Traverses the range [first, last) and returns an iterator located at
//the first occurrence of target. Returns second if target is not found.
//Time complexity: linear in the size of the range (first, last).

template <class ForwardIterator, class T>
int count(ForwardIterator first, ForwardIterator last, const T& target);
//Traverse the range [first, last) and returns the number
//of elements equal to target.
//Time complexity: linear in the size of the range (first, last).

template <class ForwardIterator1, class ForwardIterator2>
bool equal(ForwardIterator1 first1, ForwardIterator1 last1,
           ForwardIterator2 first2);
//Returns true if [first1, last1) contains the same elements in the same
//order as the first last1-first1 elements starting at first2.
//Otherwise, returns false.
//Time complexity: linear in the size of the range (first, last).
```

> ⁴The actual return type is an integer type that we have not discussed, but the returned value should be assignable to a variable of type int.
