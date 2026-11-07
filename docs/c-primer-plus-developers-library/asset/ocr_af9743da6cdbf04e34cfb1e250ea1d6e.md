# Note to Instructors

One of the goals of this edition of C++ *Primer Plus* is to provide a book that can be used as either a teach-yourself book or as a textbook. Here are some of the features that support using C++ *Primer Plus*, Sixth Edition, as a textbook:

+   - This book describes generic C++, so it isn’t dependent on a particular implementation.
+   - The contents track the ISO/ANSI C++ standards committee’s work and include discussions of templates, the STL, the `string` class, exceptions, RTTI, and namespaces.
+   - It doesn’t assume prior knowledge of C, so it can be used without a C prerequisite. (Some programming background is desirable, however.)
+   - Topics are arranged so that the early chapters can be covered rapidly as review chapters for courses that do have a C prerequisite.
+   - Chapters include review questions and programming exercises. Appendix J provides the answers to the review questions.
+   - The book introduces several topics that are appropriate for computer science courses, including abstract data types (ADTs), stacks, queues, simple lists, simulations, generic programming, and using recursion to implement a divide-and-conquer strategy.
+   - Most chapters are short enough to cover in a week or less.
+   - The book discusses *when* to use certain features as well as *how* to use them. For example, it links public inheritance to *is-a* relationships and composition and private inheritance to *has-a* relationships, and it discusses when to use virtual functions and when not to.

# Conventions Used in This Book

This book uses several typographic conventions to distinguish among various kinds of text:

+   - Code lines, commands, statements, variables, filenames, and program output appear in a computer typeface:

```
```cpp
#include <iostream>
int main()
{
    using namespace std;
    cout << "What's up, Doc!\n";
    return 0;
}
```
```