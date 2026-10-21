Unless you know for sure that **newRegistrations** does not modify its arguments,⁶ you cannot dispense with the calls to **clone**, sometimes known as *defensive copies*. The sad part of this story is that it also possible—likely, even—that **newRegistrations** is implemented as a pure function. In that case, the defensive copies are entirely wasted.

Wasted defensive copies are actually quite common⁷ in large applications that depend on a multitudes of libraries. You can avoid them by using immutable directories instead:

```
```scala
type Directory = Set[String]

def register(dir: Directory, user: String): Directory = dir + user
```
Listing 3.5: A directory as an immutable set; contrast with Lis. 3.4.
```

Registration relies on a pure function that produces a new set of registered users, but does not modify its input. You can use an immutable directory in an application as follows:

```
```scala
val yesterdayDir: Directory = ...
var todayDir: Directory      = ...
todayDir = register(todayDir, "new user 1")
todayDir = register(todayDir, "new user 2")
val todayReg = newRegistrations(todayDir, yesterdayDir)
```
```

Function **newRegistrations** can be called on directories directly, without cloning—immutable sets do not even have a public **clone** method in Scala. There is no danger of a side effect inside **newRegistrations** modifying them: They are immutable!

Note that the application is not written in a functional style: It uses assignment statements as side effects and sequential composition to chain modifications. Still, the imperative code benefits from using immutable directories by avoiding unnecessary defensive copies.

You might argue that no one in their right mind would implement the function **newRegistrations** by modifying the input set. Maybe. But can you rely on a stance that all libraries should use reasonable code? In an ideal world, you would depend on documentation to confirm that **newRegistrations** has no side effects. But how often have you found library documentation to be deficient?

⁶This includes tomorrow’s implementation of the function. So, if the function is not under your control, checking the source code is not enough. You need some guarantees, typically in the documentation, that the function not only *is* but *will remain* pure.

⁷It can also be the case that you are calling a method that stores its arguments and makes its own defensive copies because it worries that the arguments might be modified after the call. In the worst case, you may end up cloning objects both on the calling side and inside the code that is called. Paradoxically, sharing immutable objects often results is less memory allocation, not more.