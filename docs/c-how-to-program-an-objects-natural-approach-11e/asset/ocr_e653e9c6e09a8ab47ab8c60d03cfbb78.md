```
Books after sorting:
C How to Program
C# How to Program
C++ How to Program
Intro to Python

shared_ptr with a custom deleter.
Custom deleter for a Book, Destroying Book: Android How to Program

End of main: shared_ptr objects going out of scope.
Destroying Book: C How to Program
Destroying Book: C# How to Program
Destroying Book: C++ How to Program
Destroying Book: Intro to Python
Destroying Book: Java How to Program
```

**Fig. 20.1.** | shared_ptr example program. (Part 3 of 3.)

# Creating shared_ptrs

The program uses shared_ptrs to manage several Book instances. Lines 33—34 use the standard library function make_shared to create a shared_ptr to a dynamically allocated Book object with the title “C++ How to Program”.³ This is the recommended way to create a shared_ptr.⁴ You can simplify this statement by declaring bookPtr with auto. The shared_ptr manages the Book object and initially sets its reference count to 1—one shared_ptr currently refers to the dynamically allocated object. If a new shared_ptr is initialized with an existing one, they both share ownership of the resource and the reference count increases by 1. If you make multiple shared_ptrs with the same pointer, the shared_ptrs won’t acknowledge each other, and the reference count will be wrong. When the shared_ptrs are destroyed, they decrease the reference count by one. The shared_ptr destructor call that decrements the shared resource’s reference count to 0 also deletes the resource.

# Manipulating shared_ptrs

Lines 35—36 display the Book’s title and the number of shared_ptrs referencing that object—that is, the current reference count. We use the -> operator to access the Book’s data member title—shared_ptrs overload the pointer operators -> and *, so you can use them like raw pointers. The shared_ptr member function use_count returns the reference count.

Line 39 creates another shared_ptr to the same Book using the shared_ptr constructor that receives a shared_ptr argument—this increments the Book’s reference count by one. You also can use shared_ptr’s assignment operator (=) to create a shared_ptr to the same resource. Lines 40—41 display the Book’s title and reference count again to show that the reference count increased by one when we created the second shared_ptr.

As mentioned earlier, changes made to the resource of a shared_ptr are “seen” by all shared_ptrs to that resource. Line 44 uses bookPtr2 to change the Book’s title, then

+   3. “std::make_shared, std::make_shared_for_overwrite.” Accessed April 18, 2023. https://en.cppreference.com/w/cpp/memory/shared_ptr/make_shared.
+   4. C++ Core Guidelines, “R.22: Use make_shared() to make shared_ptrs.” Accessed April 18, 2023. https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#Rsmart-shared.