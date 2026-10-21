
## 7.7 Building Lists in Reverse Order

As mentioned in the discussion of function append, appending to a list takes time proportional to the length of the list, while prepending is a constant-time operation. This point is essential to keep in mind if you want to avoid writing list-based code that is grossly inefficient.

Consider the case of list reversal. To implement the function recursively, you could be tempted to use a recursive call to reverse the tail of a list and then append the head of the list at the end of the reversed tail:

```
reverse(list) = append(reverse(tail(list)), head(list))
```

While this equality is indeed valid on a non-empty list, using it results in an unacceptable reverse function:

```
Scala
// DON'T DO THIS!
def reverse[A](list: List[A]): List[A] = list match
  case Nil          => list
  case head :: tail => append(reverse(tail), head)
```

Although this function correctly produces a list in reverse order, it suffers from two major flaws. First, it is not tail recursive and will run out of stack space when applied to large lists. Second, and most importantly, its performance is unsatisfactory, even for those lists that fit in the execution stack.

If the list being reversed contains n elements, the length of reverse(tail) is n − 1, and the evaluation of append necessitates n − 1 operations. But inside the reverse(tail) computation, there is another call to append on a list with n − 2 elements; and inside the next nested computation is another call to append on a list of length n − 3; and so forth. Overall, (n − 1) + (n − 2) + ⋯ + 1 = (n × (n − 1))/2 operations are needed. As a result, the computing time of this reverse function is proportional to the square of the length of the list being reversed.

To avoid this, introduce a second list argument:

```
Scala
def reverse[A](list: List[A]): List[A] =
  @tailrec
  def addToStack(rem: List[A], rev: List[A]): List[A] = rem match
    case Nil          => rev
    case top :: bottom => addToStack(bottom, top :: rev)

  addToStack(list, Nil)

Listing 7.15: Linear, tail recursive implementation of list reversal.
```

This function proceeds by repeatedly adding the head of the list being reversed to the front of an accumulator list `rev`. You can think of it as peeling cards from a deck and putting them onto the table: In the end, the resulting deck of cards is the reverse of the original deck.

Contrary to the previous attempt, this implementation only uses “::” directly to build the resulting list, and is linear in complexity. As a simple experiment on the desktop computer used to typeset this book, it took approximately 75 milliseconds to reverse a list of 5000 numbers using the first implementation. This time decreased to 0.027 millisecond when the improved variant was used, a more than 1/2000 reduction. Incidentally, this implementation has also become tail recursive, and can handle lists of arbitrary length.

There may be situations where you are tempted to append to a list because prepending would not produce a list in the right order. Don’t do it. Instead, build the list in the wrong order, efficiently, and then reverse it. For instance, to extract space-separated tokens from a stream of characters, it would feel natural to use append to add a character to the current token, then append again to add a token to a list of tokens. Instead, you can use a combination of prepending and reversing:

```
```scala
def tokenize(stream: List[Char]): List[String] =
  def addToken(token: List[Char], tokens: List[String]): List[String] =
    if isEmpty(token) then tokens else reverse(token).mkString :: tokens

  @tailrec
  def loop(stream: List[Char], token: List[Char], tokens: List[String]): List[String]=
    stream match
      case w :: chars if w.isWhitespace => loop(chars, Nil, addToken(token, tokens))
      case c :: chars                  => loop(chars, c :: token, tokens)
      case Nil                          => addToken(token, tokens)

  reverse(loop(stream, Nil, Nil))
```
```

Characters are processed one at a time in function `loop`. A non-whitespace character (c) is added to the current token, and the computation proceeds recursively. Upon encountering a whitespace character (w), the current token is added to a list of tokens, and a new token (Nil) is started. The last token, which is not necessarily followed by whitespace, is added at the end.

Note how characters are added to tokens using constant-time operation “::”. As a result, tokens are built in reverse order. In function `addToken`, each token is reversed one time when it is added to the list. (The function skips empty tokens and uses standard method `mkString` to convert a list of characters into a string.) Similarly, tokens are added to a list of tokens using “::”, and the list is reversed at the end. Since reversal was implemented in linear time, the entire tokenization time remains proportional to the lengths and number of tokens.

## 7.8 Illustration: Sorting

### NOTE

Efficient sorting is typically not performed directly on lists. Instead, list values can be stored in a temporary array, the array sorted, and the list reconstructed. Furthermore, practical sorting functions should be parameterized by the type of the elements being sorted and the criterion used to order them. This section focuses on direct sorting of lists of integers because it offers a good illustration of recursive patterns. The resulting functions suffer from limitations and inefficiencies that would likely be unacceptable in production code.

Consider the problem of sorting a list of integers in increasing order. You can decompose a non-empty list into a head and a tail and apply recursion to sort the tail. You are then left with a single value (the head) and a sorted list (the sorted tail). All that is needed to complete the sorting function is to insert this value at the right place into the sorted list. This strategy results in a form of insert-sort:

```
def insertInSorted(x: Int, sorted: List[Int]): List[Int] = sorted match
  case Nil => List(x)
  case min :: others =>
    if x < min then x :: sorted else min :: insertInSorted(x, others)

def insertSort(list: List[Int]): List[Int] = list match
  case Nil => list
  case h :: t => insertInSorted(h, insertSort(t))
```

Listing 7.17: Insertion sort.

The sorting function uses a function insertInSorted to insert the head of a list into its sorted tail. In this auxiliary function, you insert an element x into an empty list by creating a one-element list List(x). Otherwise, x is compared to the head of the sorted list, min, which is its smallest element. If x is smaller than the minimum, it is also smaller than all the other values and therefore belongs at the front of the list. Otherwise, the smallest value in the list is still min, and you need to insert x somewhere in the tail of the list, which is achieved through a recursive call.

Insert-sort is known to have poor performance—computation time proportional to the square of the length of the list—and better strategies have been devised based on splitting a list into two halves instead of a head and tail. There are two classic variants of this pattern, with which you are probably familiar:

- *Merge-sort*: Split a list in the middle, sort both halves recursively, then merge the two sorted lists into one.
- • Quick-sort: Split a list into low and high values, sort both parts recursively, then concatenate the two sorted lists into one.

Merge-sort uses a simple strategy to split a list in two, but has more work to do to merge the lists after they have been sorted. Quick-sort relies on a more complicated splitting strategy, but once sorted, lists only need to be concatenated.

```
def merge(sortedA: List[Int], sortedB: List[Int]): List[Int] = (sortedA, sortedB) match
case (Nil, _) => sortedB
case (_, Nil) => sortedA
case (hA :: tA, hB :: tB) =>
if hA <= hB then hA :: merge(tA, sortedB) else hB :: merge(sortedA, tB)
```

The merging of sorted lists starts with two patterns to deal with empty lists—merging a list with an empty list results in the list itself. The last pattern then compares the heads of two non-empty lists. Whichever is smaller needs to come first in the merged list. Once this value is selected, the remainder of the two lists are merged recursively. With the merging function thus written, you implement the merge-sort by using functions length and splitAt to split a list in the middle.

An easy mistake would be to forget the case List(_) in the first pattern in mergeSort. As mentioned earlier, in the discussion of Listing 6.5, this would result in a non-terminating function. As a variant, you can apply pattern matching to the length of the list, which is needed for the split, and write the merge-sort function as follows:

```
def mergeSort(list: List[Int]): List[Int] = length(list) match
case 0 | 1 => list
case len =>
val (left, right) = splitAt(list, len / 2)
merge(mergeSort(left), mergeSort(right))
```

Again, don’t forget the case 1 for lists too short to be split.

To implement quick-sort, you need to split the list into low and high values. This is typically done by choosing one value, called the pivot, and splitting the list into values
