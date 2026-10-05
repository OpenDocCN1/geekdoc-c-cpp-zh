# 20.5 Smart Pointers

The standard library includes a small family of pointer types that are smarter than raw pointers. They are full-fledged classes and, among other things, have a constructor that takes a raw pointer. Most importantly, they have a destructor that relieves you of the most critical task when dealing with raw pointers: calling delete.

The family is gathered in the <memory> header and includes the following members:

+   * unique_ptr
Owns the raw pointer. Not copyable, because then multiple instances would own it, but movable—for example, as a return value.

+   * shared_ptr
Owns the raw pointer, but not necessarily alone. When copied, you get two shared_ptr instances managing the same raw pointer; the raw pointer is only removed when the last copy is removed.

+   * weak_ptr
A little brother of shared_ptr, which you need in some situations when shared_ptr instances contain each other.

+   * auto_ptr
Deprecated since C++11; use unique_ptr instead. auto_ptr cannot be moved; if you copy it, you alter the