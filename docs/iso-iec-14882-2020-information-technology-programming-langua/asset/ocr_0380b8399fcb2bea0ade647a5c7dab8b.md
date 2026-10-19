(1.8) — pointers to non-static class members,45 which identify members of a given type within objects of a given class, 9.3.4.4. Pointers to data members and pointers to member functions are collectively called pointer-to-member types.

2 These methods of constructing types can be applied recursively; restrictions are mentioned in 9.3.4. Constructing a type such that the number of bytes in its object representation exceeds the maximum value representable in the type std::size_t (17.2) is ill-formed.

3 The type of a pointer to cv void or a pointer to an object type is called an object pointer type.
[Note 1: A pointer to void does not have a pointer-to-object type, however, because void is not an object type. — end note]

The type of a pointer that can designate a function is called a function pointer type. A pointer to an object of type T is referred to as a “pointer to T”.
[Example 1: A pointer to an object of type int is referred to as “pointer to int” and a pointer to an object of class X is called a “pointer to X”. — end example]

Except for pointers to static members, text referring to “pointers” does not apply to pointers to members. Pointers to incomplete types are allowed although there are restrictions on what can be done with them (6.7.6). Every value of pointer type is one of the following:

+   (3.1) — a pointer to an object or function (the pointer is said to point to the object or function), or
+   (3.2) — a pointer past the end of an object (7.6.6), or
+   (3.3) — the null pointer value for that type, or
+   (3.4) — an invalid pointer value.

A value of a pointer type that is a pointer to or past the end of an object represents the address of the first byte in memory (6.7.1) occupied by the object46 or the first byte in memory after the end of the storage occupied by the object, respectively.
[Note 2: A pointer past the end of an object (7.6.6) is not considered to point to an unrelated object of the object’s type, even if the unrelated object is located at that address. A pointer value becomes invalid when the storage it denotes reaches the end of its storage duration; see 6.7.5. — end note]

For purposes of pointer arithmetic (7.6.6) and comparison (7.6.9, 7.6.10), a pointer past the end of the last element of an array x of n elements is considered to be equivalent to a pointer to a hypothetical array element n of x and an object of type T that is not an array element is considered to belong to an array with one element of type T. The value representation of pointer types is implementation-defined. Pointers to layout-compatible types shall have the same value representation and alignment requirements (6.7.6).
[Note 3: Pointers to over-aligned types (6.7.6) have no special representation, but their range of valid values is restricted by the extended alignment requirement. — end note]

4 Two objects a and b are pointer-interconvertible if:

+   (4.1) — they are the same object, or
+   (4.2) — one is a union object and the other is a non-static data member of that object (11.5), or
+   (4.3) — one is a standard-layout class object and the other is the first non-static data member of that object, or, if the object has no non-static data members, any base class subobject of that object (11.4), or
+   (4.4) — there exists an object c such that a and c are pointer-interconvertible, and c and b are pointer-interconvertible.

If two objects are pointer-interconvertible, then they have the same address, and it is possible to obtain a pointer to one from a pointer to the other via a reinterpret_cast (7.6.1.10).
[Note 4: An array object and its first element are not pointer-interconvertible, even though they have the same address. — end note]

5 A pointer to cv void can be used to point to objects of unknown type. Such a pointer shall be able to hold any object pointer. An object of type cv void* shall have the same representation and alignment requirements as cv char*.