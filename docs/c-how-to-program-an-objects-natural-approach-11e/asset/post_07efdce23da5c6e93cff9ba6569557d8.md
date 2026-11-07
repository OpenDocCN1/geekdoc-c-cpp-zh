
weak_ptrs “to break cycles of shared_ptrs.” [^6] As we’ll demonstrate later in this section, this helps avoid memory leaks caused by circular references.

A weak_ptr cannot directly access the resource it points to—you must create a shared_ptr from the weak_ptr to access the resource. This enables a program to determine whether the resource still exists. There are two ways to create a shared_ptr from a weak_ptr:

- You can pass the weak_ptr to the shared_ptr constructor, which creates a shared_ptr to the resource pointed to by the weak_ptr and properly increases the reference count. If the resource has already been deleted, the shared_ptr constructor will throw a bad_weak_ptr exception.
- You can also call the weak_ptr member function lock, which returns a shared_ptr to the weak_ptr’s resource. [^7] If the weak_ptr does not currently point to a resource, lock returns an empty shared_ptr (i.e., a shared_ptr with its internal pointer set to nullptr). You should use lock if an empty shared_ptr isn’t considered an error in the context of your application.

One typical use-case of weak_ptrs is in circularly referential data—a situation in which two objects refer to each other internally, as the example in Figs. 20.2–20.5 demonstrates. Another use-case is avoiding dangling pointers[^8]—that is, pointers to dynamically allocated objects that are subsequently deleted. Using such a pointer is undefined behavior that often crashes a program. Because a weak_ptr cannot directly access the resource it points to, the resource can be deleted. If the program subsequently attempts to use the weak_ptr’s lock function to get a shared_ptr, lock returns nullptr to indicate that the resource no longer exists.

## Class Definitions for Classes Author and Book

We’ll demonstrate weak_ptrs using classes Author and Book (Figs. 20.2–20.5). Each class contains pointers to an object of the other class. We also use public data members here only to simplify the code. This creates a circular type reference between the class definitions:

- class Author defines a weak_ptr and a shared_ptr to a Book (lines 20–21 in Fig. 20.2), and
- class Book defines a weak_ptr and a shared_ptr to an Author (lines 20–21 in Fig. 20.3).

To declare these pointers, each class needs to know that the other exists, which you usually accomplish by including the corresponding class’s header. However, we cannot do that here because class Author depends on class Book, which, in turn, depends on class Author. Including Book.h in Author.h and including Author.h in Book.h causes compilation errors. Interestingly, declaring a pointer does not require a complete type definition—it simply requires knowing that the type exists. This is the purpose of the forward class declarations in line 8 of Figs. 20.2 and 20.3. To use a pointer to interact with an object, the full class definition must be available, as you’ll see in the .cpp files for classes Author (Fig. 20.4) and Book (Fig. 20.5).

```cpp
// Fig. 20.2: Author.h
// Author class definition.
#pragma once
#include <memory>
#include <string>
#include <string_view>

class Book; // forward declaration of class Book

// Author class definition
class Author {
public:
    explicit Author(std::string_view authorName);
    ~Author();

    // print the title of the Book this Author wrote
    void printBookTitle();

    std::string name; // name of the Author
    std::weak_ptr<Book> weakBookPtr; // Book the Author wrote
    std::shared_ptr<Book> sharedBookPtr; // Book the Author wrote
};
```

**Fig. 20.2** | Author class definition.

```cpp
// Fig. 20.3: Book.h
// Book class definition.
#pragma once
#include <memory>
#include <string>
#include <string_view>

class Author; // forward declaration of class Author

// Book class definition
class Book {
public:
    explicit Book(std::string_view bookTitle);
    ~Book();

    // print the name of this Book's Author
    void printAuthorName();

    std::string title; // title of the Book
    std::weak_ptr<Author> weakAuthorPtr; // Author of the Book
    std::shared_ptr<Author> sharedAuthorPtr; // Author of the Book
};
```

**Fig. 20.3** | Book class definition.

```cpp
// Fig. 20.5: Book.cpp
// Book member-function definitions.
#include <format>
#include <iostream>
#include <memory>
#include <string>
#include <string_view>
#include "Author.h"
#include "Book.h"

Book::Book(std::string_view bookTitle) : title{bookTitle} {}

Book::~Book() {
    std::cout << std::format("Destroying Book: {}\n", title);
}

// print the name of this Book's Author
void Book::printAuthorName() {
    // if weakAuthorPtr.lock() returns a non-empty shared_ptr
    if (std::shared_ptr<Author> authorPtr{weakAuthorPtr.lock()}) {
        // show the reference count increase and print the Author's name
        std::cout << std::format("Reference count for Author {} is {}\n",
            authorPtr->name, authorPtr.use_count());
        std::cout << std::format("The book {} was written by {}\n",
            title, authorPtr->name);
    }
    else { // weakAuthorPtr points to NULL
        std::cout << "This Book has no Author.\n";
    }
}
```

**Fig. 20.5** | Book member-function definitions.

Both classes define destructors that display a message to indicate when an object of either class is destroyed (Figs. 20.4 and 20.5, lines 13–15). Class Author's printBookTitle function (Fig. 20.4, lines 18–30) displays its Book's title and reference count (lines 22–23), then shows that the Author wrote that Book (lines 24–25). Similarly, class Book's printAuthorName function (Fig. 20.5, lines 18–30) displays its Author's name and reference count (lines 22–23), then shows that the Book was written by that Author (lines 24–25).

Recall that you can't access a resource directly through a weak_ptr. For printBookTitle and printAuthorName to perform the tasks in lines 22–25 of each, these functions must first create a shared_ptr from the weak_ptr data member by calling the weak_ptr's lock function (line 20 in each figure). If the weak_ptr does not reference a resource, the lock function returns a shared_ptr containing nullptr, which evaluates to false in line 20. Otherwise, the new shared_ptr contains a valid pointer to the weak_ptr's resource, the condition in line 20 evaluates to true, and lines 22–25 of each figure can access the corresponding resource. Lines 22–23 of each function displayed the shared_ptr's reference count to show that creating the new shared_ptr increased the reference count for the corresponding Book (Fig. 20.4) or Author (Fig. 20.5). The new shared_ptr created in line 20 of each figure is a local object, so it's destroyed when its enclosing block ends. At that point, the corresponding reference count decreases by one.

## main Function

Figure 20.6 demonstrates the **memory leak caused by the circular reference** between Author and Book. Lines 11–14 create shared_ptrs to an object of each class. Line 17 sets the Book’s weak_ptr data member to point to the Author, and line 18 sets the Author’s weak_ptr data member to point to the Book. Similarly, lines 21–22 set the shared_ptr data members of each object. The Author and Book objects now reference each other.

![](img/7b5e2088e71c7f78681d4ddbcf104c06_1210_0.png)

```cpp
// fig20_06.cpp
// Demonstrate use of weak_ptr.
#include <format>
#include <iostream>
#include <memory>
#include "Author.h"
#include "Book.h"

int main() {
   // create a Book and an Author
   std::shared_ptr<Book> bookPtr{
      std::make_shared<Book>("C++ How to Program")};
   std::shared_ptr<Author> authorPtr{
      std::make_shared<Author>("Deitel & Deitel")};

   // reference the Book and Author to each other
   bookPtr->weakAuthorPtr = authorPtr;
   authorPtr->weakBookPtr = bookPtr;

   // set the shared_ptr data members to create the memory leak
   bookPtr->sharedAuthorPtr = authorPtr;
   authorPtr->sharedBookPtr = bookPtr;

   // reference count for bookPtr and authorPtr is two
   std::cout << std::format("Reference count for Book {} is {}\n",
      bookPtr->title, bookPtr.use_count());
   std::cout << std::format("Reference count for Author {} is {}\n\n",
      authorPtr->name, authorPtr.use_count());

   // access the cross references to print the data they point to
   std::cout << "Access Author name and Book title via weak_ptrs:\n";
   bookPtr->printAuthorName();
   std::cout << "\n";
   authorPtr->printBookTitle();

   // reference count for each shared_ptr is two
   std::cout << std::format("Reference count for Book {} is {}\n",
      bookPtr->title, bookPtr.use_count());
   std::cout << std::format("Reference count for Author {} is {}\n\n",
      authorPtr->name, authorPtr.use_count());

   // the shared_ptrs go out of scope, the Book and Author are not destroyed
   std::cout << "End of main, shared_ptrs going out of scope.\n";
}
```

**Fig. 20.6** | shared_ptrs cause a memory leak in circularly referential data. (Part 1 of 2.)

[^6]: C++ Core Guidelines, “R.24: Use std::weak_ptr to break cycles of shared_ptrs.” Accessed April 18, 2023. https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#Rr-weak_ptr.

[^7]: “std::weak_ptr::lock.” Accessed April 18, 2023. https://en.cppreference.com/w/cpp/memory/weak_ptr/lock.

[^8]: “When is std::weak_ptr useful?” Accessed April 18, 2023. https://stackoverflow.com/questions/12030650/when-is-stdweak-ptr-useful.
