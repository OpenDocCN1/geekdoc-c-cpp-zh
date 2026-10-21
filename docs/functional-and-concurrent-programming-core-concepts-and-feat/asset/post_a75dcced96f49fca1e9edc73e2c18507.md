
through another call to function processCollection, and so on. The computation that processes the entire list is processOne(processOne(processOne(...))), which is of the form f(f(f(x))), not f(x); f(x); f(x). No mutable variable is involved.

You can always replace code that uses loops and mutable variables with code that uses recursion and immutable variables instead. Function composition combined with recursion has the same expressive power as sequential composition combined with loops. Anything that can be computed using one of these approaches can be computed using the other.

## 6.2 Recursive Algorithms

In textbooks and tutorials, factorial is the most widely used example of a recursive function. Since no book that discusses recursive programming would be complete without it, here it is, in Scala:

```
def factorial(n: Int): Int = if n == 0 then 1 else n * factorial(n - 1)
```

Listing 6.2: Recursive implementation of factorial; contrast with Lis. 6.11.

This code is certainly elegant. It is shorter and uses fewer variables than a loop-based alternative. However, I do not believe it makes a very good motivation for the use of recursion. You can easily implement a factorial function with a loop, and the resulting code is likely to be more efficient. The same can be said of many other typical textbook illustrations of recursion, such as the greatest common divisor.² So, if you have seen the factorial example in the past, and it has left you unimpressed, no worries. This book contains dozens of examples of recursive functions, and ideally you will find later illustrations more persuasive.

The Tower of Hanoi is another classic teaching example, which is a more effective example than the factorial or greatest common divisor problem. It represents a puzzle, in which discs of assorted sizes are stacked on three pegs. Initially, all the discs are stacked on the leftmost peg, in decreasing order of size. The objective of the game is to move all the discs to the rightmost peg, using the middle peg for intermediate storage, and while adhering to the following rules:

- You can move only one disc at a time.
- Only the topmost discs can be moved.
- No disc can rest on top of a smaller disc.

Figure 6.1 shows the seven steps required to move a three-disc tower from left to right.

You can solve the Tower of Hanoi problem with a recursive algorithm: To move n discs from peg L to peg R using peg M, if n > 0, first move n − 1 discs from L to M

using R; then move one disc from L to R; then move n-1 discs from M to R using L. If n = 0, there is nothing to do. This strategy can be translated into a recursive function that prints all the steps needed to move a given number of discs:

```
def hanoi[A](n: Int, from: A, middle: A, to: A): Unit =
  if n > 0 then
    hanoi(n - 1, from, to, middle)
    println(s"$from -> $to")
    hanoi(n - 1, middle, from, to)
```

# Listing 6.3: Recursive solution to the Tower of Hanoi problem.

![](img/74309e2bdd93f68d2e94338a3d73517f_104_0.png)

## 6.3 Key Principles of Recursive Algorithms

This function does nothing if n = 0. Otherwise, a first recursive call is used to move n–1 discs from the left peg to the middle peg, using the right peg as temporary storage. The effect of this call is to leave the nth disc free (position 3 in Figure 6.1). The print statement then moves this disc from left to right (position 4 in Figure 6.1). A second recursive call moves n–1 disc from their storage peg (middle) to the right peg, using the left peg as storage. When called as hanoi(3, 'L', 'M', 'R') this function produces the same sequence of steps as Figure 6.1:

```
L -> R
L -> M
R -> M
L -> R
M -> L
M -> R
L -> R
```

What makes the Tower of Hanoi a compelling example is that there is no straight-forward loop-based equivalent that implements the same algorithm.³ One reason for this is that function hanoi makes two recursive calls to itself, compared to the single call needed in the factorial or greatest common divisor examples.

## 6.3 Key Principles of Recursive Algorithms

The core idea behind recursive algorithms is to reduce a problem to one or more smaller instances of the same problem and to use the solutions to these subproblems to derive a solution to the original problem. The Tower of Hanoi function in Section 6.2 solves the problem of moving n discs by combining the solutions to two subproblems of moving n – 1 discs. Think of this strategy as a special case of the divide and conquer approach in which the subtasks are homologous with the original task.

When writing a recursive function, you need to pay attention to three major concerns:

- At least one branch of the computation should not be recursive. If the evaluation of your function always triggers a recursive call, the function keeps re-executing itself and cannot possibly terminate. In the Tower of Hanoi example, the case n = 0 does not require a recursive call.

> There are iterative solutions to the Tower of Hanoi that can be easily implemented in terms of loops, but their correctness is harder to justify, and even the simplest loop-based program is still more complex than the recursive function presented here.

Keep this principle in mind to help catch mistakes quickly. For instance, consider this incorrect attempt to define a function to extract the last element of a list:

```
// DON'T DO THIS!
def last[A](list: List[A]): A = list match
  case Nil      => throw NoSuchElementException("last(empty)")
  case _ :: tail => last(tail)
```

Listing 6.4: Incorrect implementation of last; fixed in Lis. 6.10.

The algorithm is based on the idea that the empty list has no last element and that the last element of a non-empty list is the last element of its tail. However, the function cannot possibly work as written because it does not have a value-returning, non-recursive branch: The function either throws an exception or continues to run. Indeed, the intuition that the last element of a non-empty list is the last element of its tail is not valid on a list of size 1.

- All the subproblems solved recursively must be smaller than the original problem in some way. This is again necessary to guarantee termination. Common patterns include a list function applied to a shorter list; a number function applied to a smaller positive number (as in the case of hanoi); a tree function applied to a subtree; and so on.

As an illustration of a failure to adhere to this principle, consider this incorrect implementation of merge-sort (function merge is omitted):

```
// DON'T DO THIS!
def mergeSort[A](list: List[A]): List[A] =
  if list.isEmpty then list
  else
    val (left, right) = list.splitAt(list.length / 2) // split in the middle
    merge(mergeSort(left), mergeSort(right))
```

Listing 6.5: Incorrect merge sort; fixed in Lis. 7.18.

Method splitAt splits a list as a given point: List(A,B,C,D).splitAt(2) is the pair (List(A,B), List(C,D)). This method is used to split a non-empty list into two halves. Each half is sorted recursively, and the two sorted halves are merged into a sorted list.

The issue here is that mergeSort(right) is not guaranteed to be a recursive call on a smaller list. If you split a list that contains exactly one element, you get two lists: One is empty, and the other is the original list unchanged. In the case of function mergeSort, this means that right could be the same as list, and

the function is applied recursively to a sorting problem that is not smaller. This `mergeSort` function is incorrect: It does not terminate when called on a non-empty list.

When a problem has multiple parameters, it is sometimes enough that one of them, or a combination of them, becomes smaller. For example, a pair that consists of a positive number and a list can become smaller by the number getting smaller, the list getting shorter, or the sum of the number plus the length of the list getting smaller, among other ways.

Some cases are more complicated and necessitate more refined notions of “smaller.” For instance, in this classic example (sometimes known as the *Ackermann function*),⁴ the computation is guaranteed to terminate because the pair (x,y) decreases in lexicographic ordering: Either x decreases, or x stays unchanged and y decreases:

```
def a(x: BigInt, y: BigInt): BigInt = (x, y) match
  case (0, _) => y + 1
  case (_, 0) => a(x - 1, 1)
  case _      => a(x - 1, a(x, y - 1))
```

Listing 6.6: Ackermann function.

- *Your focus as a programmer should be on using the solutions to the smaller problems, not on how these smaller problems are themselves solved by the recursive calls.* This point is crucial and is key to effective recursive thinking. One common beginner’s mistake is to try to unfold recursive calls to follow their computations. Except for the simplest functions, diving into the recursive calls quickly becomes intractable. (Try it on `hanoi`.) Instead, you must take the solutions to the smaller problems for granted—given to you by the “magic” of recursion—and focus on using these values to build a solution to the original problem.

## 6.4 Recursive Structures

As mentioned in Chapter 5, some algebraic data types present recursive structures, which can be handled quite naturally by recursive functions. Indeed, the processing of recursive structures is one of the major uses of recursive programming.

Trees are one of the most common recursive structures used in programming. Listing 5.9 used trees to represent expressions and a recursive function to evaluate a tree. As another example, consider binary trees. A non-empty binary tree consists of a root

⁴Although the function is guaranteed to terminate in theory, its complexity is huge, and its recursive evaluation will run out of stack space on most inputs. The Ackermann function was defined for the theoretical study of recursive functions and has no practical purpose.
