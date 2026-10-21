problem without using first. It is important that the second recursive call only takes place if the first one fails to produce a solution. This behavior is guaranteed here by the fact that the argument to orElse is passed by name and is evaluated only if the first option is empty.

As a side note, notice that the implementation is simplified by the fact that lists are immutable. In particular, even though the recursive calls are conceptually digging into the list of numbers, the same list others is used as an argument in both recursive calls. If lists were mutated, you would need to “undo” changes from the first computation before reusing the list in a second call.

Subset-sum problems may have multiple solutions. For instance, 18 can also be reached as 3 − 6 + 11 + 7 + 3 = 18 using the numbers from the example set. To compute all the solutions, you can modify findSum to always make the second recursive call, even if the first call succeeds:

```
def findAllSums(target: Int, numbers: List[Int]): Set[List[Int]] =
  if target == 0 then Set(List.empty)
  else
    numbers match
      case Nil => Set.empty
      case first :: others =>
        (findAllSums(target - first, others).map(first :: _)
         union findAllSums(target, others))
```

Listing 12.11: All the solutions to subset-sum; contrast with Lis. 12.10 and 12.12.

The differences between findSum and findAllSums are minimal. Options are replaced with sets, and orElse is replaced with union. Contrary to orElse, method union always evaluates both of its arguments.

Given how similar they are, is there a way to avoid having to write both functions? If you have all the solutions to a problem, you can always pick one, so you could be tempted to implement findSum in terms of findAllSums:

```
// DON'T DO THIS!
def findSum(target: Int, numbers: List[Int]): Option[List[Int]] =
  findAllSums(target, numbers).headOption
```

The problem with this approach is that findSum now calculates all the solutions even though it needs only one. By contrast, the function in Listing 12.10 stops once a solution has been found. This can be remedied by writing a lazily evaluated variant of findAllSums:

```
def lazyFindAllSums(target: Int, numbers: List[Int]): LazyList[List[Int]] =
  if target == 0 then LazyList(List.empty)
  else
```