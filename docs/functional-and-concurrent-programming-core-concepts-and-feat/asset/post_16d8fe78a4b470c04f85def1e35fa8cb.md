
## 3.7 Functional Lists

The most widely used persistent data structure in functional programming is the functional list. Either a list is empty (no elements) or it consists of a first value (called the *head*), potentially followed by more values (the *tail*). Every list can be built from two primitives: the empty list and an operator that combines a head element with an existing list. Traditionally, the empty list is called “nil,” and the operator is called “cons.” This terminology dates back to the days of Lisp, with the list [1,2,3] being built as follows:

```lisp
(cons 1 (cons 2 (cons 3 nil)))
```

The nested expression starts with the empty list nil, uses cons to build the list (cons 3 nil), which is the list [3], then uses cons again to add 2, then 1, in front of the list. The head of the final list is 1; its tail is the list (cons 2 (cons 3 nil)).

Languages of the ML family popularized the use of the infix operator “::” to represent cons. It is also being used in more recent languages like F# and Scala. The Lisp code just given can be written in Scala as follows:

```scala
1 :: 2 :: 3 :: Nil
```

Again the head of the list is 1, and its tail is 2 :: 3 :: Nil.

For convenience, languages define factory functions to build lists. You can build the list [1,2,3] in Lisp as (list 1 2 3) and in Scala as List(1, 2, 3). Scala also defines a function List.empty that returns Nil; I sometimes use this version for clarity and better type inference. However, it is essential to keep in mind the nil/cons structure of functional lists for at least two reasons.

First, building a new list from an existing list does not, in general, require a full copy of the original list. This is because different lists can often share data. As an illustration, consider the three lists a, b, and c defined as follows:

```scala
val a = List(1, 2, 3)   // the list [1,2,3]
val b = 0 :: a           // the list [0,1,2,3]
val c = a.tail           // the list [2,3]
```

The memory allocation of these three lists looks something like Figure 3.1. Although the three lists together contain nine values, there are only four cells allocated in memory, thanks to data sharing between a, b, and c. Because lists are immutable, this sharing is harmless. The same is true, to some degree, of other persistent data structures. The method “+” used earlier on an immutable set does not make a full copy of the set. If largeSet contains 1 million elements, largeSet + x is a new set that contains 1 million and one elements, but the two sets share the vast majority of the memory allocated to implement them.

![](img/74309e2bdd93f68d2e94338a3d73517f_70_0.png)

Figure 3.1 Functional lists memory sharing.

Another consequence of this data sharing is that, on functional lists, both the head and the tail methods are efficient, constant-time operations—typically, a single pointer dereference. As long as you can express an algorithm in terms of head and tail, lists make a reasonable implementation choice. Be aware, however, that other list operations may not be as fast. Methods such as last and length, for instance, require a computing time that is proportional to the length of the list, and methods such as appended or concat need to copy the entire list.

The second reason the head/tail structure of functional lists is important is that the tail of a non-empty list is itself a list. In consequence, many computations on lists can be implemented efficiently using recursion. Chapter 7 is dedicated to recursive programming with lists.

## 3.8 Hybrid Designs

In a purely functional programming approach, all functions are pure, and all values are immutable. There is nothing wrong with that—and plenty that is good—but sometimes programmers prefer a more hybrid approach that combines pure functions and values with actions and mutable objects. If you are used to an imperative programming style, you can start using some functional programming features without committing to a fully functional design. In particular, there are some benefits from relying on immutable values when building mutable objects, and vice versa.

In a hybrid application that combines pure functions, impure functions, and actions, you need to worry about possible side effects when calling functions that are not under your control. The beauty of immutable values is that they can be shared safely, knowing that no unexpected side effect can modify them.

As an illustration, consider an application that keeps track of registered users in a mutable set:

```scala
type Directory = mutable.Set[String]

def register(dir: Directory, user: String): Unit = dir += user
```

Listing 3.4: A directory as a mutable set; contrast with List. 3.5.

Users are added via a register action, which modifies the set.

Now suppose that you need to call a function that is not under your control—say, newRegistrations, which calculates the set of newly registered users, given an earlier directory:

```scala
val yesterdayDir: Directory = ...
val todayDir: Directory = ...
register(todayDir, "new user 1")
register(todayDir, "new user 2")
val todayReg = newRegistrations(todayDir, yesterdayDir)
```

The problem here is that function newRegistrations is not necessarily pure. It could be implemented as follows:

```scala
def newRegistrations(newDir: Directory, oldDir: Directory): Directory =
    newDir.subtractAll(oldDir)
```

This implementation removes from the set newDir every user already in the set oldDir, and returns newDir. The return value is correct, but the set newDir has been modified.

Because you worry that newRegistrations could be implemented like this, you need to make sure that the directories you pass as arguments will not be modified. So, you end up calling newRegistrations on copies of your directories:

```scala
val todayReg = newRegistrations(todayDir.clone(), yesterdayDir.clone())
```

Unless you know for sure that **newRegistrations** does not modify its arguments,⁶ you cannot dispense with the calls to **clone**, sometimes known as *defensive copies*. The sad part of this story is that it is also possible—likely, even—that **newRegistrations** is implemented as a pure function. In that case, the defensive copies are entirely wasted.

Wasted defensive copies are actually quite common⁷ in large applications that depend on a multitude of libraries. You can avoid them by using immutable directories instead:

```scala
type Directory = Set[String]

def register(dir: Directory, user: String): Directory = dir + user
```

Listing 3.5: A directory as an immutable set; contrast with List. 3.4.

Registration relies on a pure function that produces a new set of registered users, but does not modify its input. You can use an immutable directory in an application as follows:

```scala
val yesterdayDir: Directory = ...
var todayDir: Directory      = ...
todayDir = register(todayDir, "new user 1")
todayDir = register(todayDir, "new user 2")
val todayReg = newRegistrations(todayDir, yesterdayDir)
```

Function **newRegistrations** can be called on directories directly, without cloning—immutable sets do not even have a public **clone** method in Scala. There is no danger of a side effect inside **newRegistrations** modifying them: They are immutable!

Note that the application is not written in a functional style: It uses assignment statements as side effects and sequential composition to chain modifications. Still, the imperative code benefits from using immutable directories by avoiding unnecessary defensive copies.

You might argue that no one in their right mind would implement the function **newRegistrations** by modifying the input set. Maybe. But can you rely on a stance that all libraries should use reasonable code? In an ideal world, you would depend on documentation to confirm that **newRegistrations** has no side effects. But how often have you found library documentation to be deficient?

⁶This includes tomorrow’s implementation of the function. So, if the function is not under your control, checking the source code is not enough. You need some guarantees, typically in the documentation, that the function not only *is* but *will remain* pure.

⁷It can also be the case that you are calling a method that stores its arguments and makes its own defensive copies because it worries that the arguments might be modified after the call. In the worst case, you may end up cloning objects both on the calling side and inside the code that is called. Paradoxically, sharing immutable objects often results in less memory allocation, not more.
