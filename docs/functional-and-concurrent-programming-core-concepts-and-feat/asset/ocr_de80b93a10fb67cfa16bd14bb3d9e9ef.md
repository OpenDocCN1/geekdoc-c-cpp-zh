# Chapter 7

# Recursion on Lists

Because functional lists are a recursive data structure—the tail of a non-empty list is a list—many list-processing functions nicely fit a recursive pattern in which recursion is applied to the tail of a list. This chapter uses this pattern to (re)implement several common list functions. The objective is twofold: It is both an exposure to standard list functions and a way to practice recursive thinking. Other patterns are also explored, in which recursion is applied to sublists other than the tail. Some performance considerations are discussed, such as the use of tail recursion or pure functions that rely internally on mutable structures.

# NOTE

The Scala collection library implements many list operations as methods of its List type. In this chapter, several are reimplemented as functions for the purpose of our discussion of recursion and recursive algorithms. The code examples deliberately rely on previously defined functions instead of the corresponding standard methods—for instance, writing head(list) where list.head could be used—so the code is closer to what it could be in another programming language with functional lists. This approach is specific to this chapter. Later parts of the book use the corresponding List methods instead for convenience and readability.

# 7.1 Recursive Algorithms as Equalities

In Chapter 6, we implemented a function last to extract the last element of a list:

```
Scala
def last[A](list: List[A]): A = list match
  case Nil          => throw NoSuchElementException("last(empty)")
  case head :: tail => if isEmpty(tail) then head else last(tail)
```

This function is based on the idea that, in general, the last element of a list is the last element of its tail. In other words, it relies on the following equality:

last(list) = last(tail(list))

Because empty lists have no last element, this equality holds only when neither list nor tail(list) is empty. These two special cases are handled non-recursively in function