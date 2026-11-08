```
```cpp
    auto find(Book& book) { /* Shelf number/Book number */
        catalog.findBookBy(book.getTitle(), book.getAuthor());
    }
};
```
```

**Listing 19.3** The changes of an actor usually only take place in one class.

The BookFinder class is now the one that is interesting for the librarian. The Book class is the one for the reader. Of course, the *find* method can be implemented in various ways—here, for simplicity, only using title and author. However, it is important that if the requirements for library management change, this mainly concerns the BookFinder class; the Book class should not be affected. On the other hand, if a method for content summary for the reader is added, then this change probably does not affect BookFinder.

# ## Open/Closed Principle

The creed of this principle is that an extension of functionality should not require a *change* to existing source code, but rather we should only write additional code that uses the existing one.

This can happen on at least two levels in modern languages like Java, C#, and C++:

+   - Source code that is combined by the compiler into a complete executable program
+   - A module dynamically loaded at runtime—in Java interchangeable `*.jar` files, in C++ dynamic libraries in the form of dynamic-link libraries (DLLs) or `*.so` files

The latter is particularly useful when it allows us to handle the program possibly even without a restart or redeployment from scratch (*redeploy*). Adding new DLLs at runtime is also conceivable, meaning that you can do so without having to completely replace any existing part.

Theoretically speaking, OCP is very simple. A simple relationship between two User and Logic classes, which are in the direct relationship "User uses Logic," violates the OCP. If we need a second Logic class, from which User should be able to use either one or the other, there is no way around the fact that both User and Logic must be adjusted, because the connection is direct here.

This problem can be addressed with cleanly defined and separately implemented interfaces: Define a LogicInterface interface, which the User class then uses and interacts with. The interface is now concretely implemented by the two Logic classes, and each User instance can choose one of the two concrete implementations via pointer or reference.

The following example is not bad at first glance and is indeed often handled this way in practice. However, it can be easily improved in open/closed terms with inheritance and interfaces.