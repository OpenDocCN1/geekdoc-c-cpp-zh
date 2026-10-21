```
def length[A](list: List[A]): Int =
  @tailrec
  def addLength(theList: List[A], len: Int): Int = theList match
    case Nil => len
    case _ :: tail => addLength(tail, len + 1)

  addLength(list, 0)
```

Listing 7.4: List length, using tail recursion; contrast with Lis. 7.3.

Function addLength is tail recursive. The whole length function can now be compiled as a loop, which will avoid stack overflow issues.

# 7.3 Returning Lists

So far, we have considered only functions that extract information from a list: last returns an element, contains returns a Boolean value, and length returns an integer. Some functions, however, process lists by building and returning other lists.

![](bbox=[0.27, 0.49, 0.7, 0.58])

Figure 7.1 Recursive strategy for function drop.

As a first example, consider the standard function drop, which is used to remove the first n elements from a list: drop(List(A,B,C,D), 2) is List(C,D). Its recursive equality follows from the fact that, to remove n elements from a list, you need to first remove the head of the list, and then remove n − 1 elements from the tail (Figure 7.1):

```
drop(list, n) = drop(tail(list), n - 1)
```

For the equality to be valid, the list needs to have a tail, and n − 1 cannot be a negative number, since negative numbers make no sense in this context. From this observation, two special cases follow, one for the empty list and one for n = 0:

```
@tailrec
def drop[A](list: List[A], n: Int): List[A] =
  if n == 0 then list
  else list match
```