![](bbox=[0.15, 0.045, 0.85, 0.335])

Figure 9.1: Private data and public interface functions of the class Person, using byte-by-byte assignment

Now a potentially dangerous situation has been created. The actual values in *person* are pointers, pointing to allocated memory. After the assignment this memory is addressed by two objects: *person* and *tmp*.

+   - The potentially dangerous situation develops into an acutely dangerous situation once the function `tmpPerson` terminates: *tmp* is destroyed. The destructor of the class Person releases the memory pointed to by the fields `d_name`, `d_address` and `d_phone`: unfortunately, this memory is also pointed at by *person*....

This problematic assignment is illustrated in Figure 9.1.

Having executed `tmpPerson`, the object referenced by *person* now contains pointers to deleted memory.

This is undoubtedly not a desired effect of using a function like `tmpPerson`. The deleted memory is likely to be reused by subsequent allocations. The pointer members of *person* have effectively become *wild pointers*, as they don't point to allocated memory anymore. In general it can be concluded that

> > *every class containing pointer data members is a potential candidate for trouble.*

Fortunately, it is possible to prevent these troubles, as discussed next.

# ### 9.3.1 Overloading the assignment operator

Obviously, the right way to assign one Person object to another, is **not** to copy the contents of the object bytewise. A better way is to make an equivalent object. One having its own allocated memory containing copies of the original strings.

The way to assign a Person object to another is illustrated in Figure 9.2. There are several ways to assign a Person object to another. One way would be to define a special member function to handle the assignment. The purpose of this member function would be to create a copy of an object having its own *name*, *address* and *phone* strings. Such a member function could be:

```
```cpp
void Person::assign(Person const &other)
```
```