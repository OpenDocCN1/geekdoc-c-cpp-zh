+   14.3 It is not possible to declare a structure without a structure tag.
+   14.4 The assignment `struct movie s1 = s2;` is legal only if s1 and s2 are based on the same template.
+   14.5 An uninitialized structure has all of its members set to zeroes.
+   14.6 The size of a structure is not always equal to the sum of the sizes of its members.
+   14.7 It is possible to have the same name for a structure tag, structure variable and a member variable.
+   14.8 A function argument can be a structure but not its pointer.
+   14.9 It is not possible to create a separate variable of an inner structure.
+   14.10 It is possible for a function to copy an array when it is passed as a member of a structure.
+   14.11 The name of a structure represents a pointer to the first member.
+   14.12 It is not possible to simultaneously access all members of a union.
+   14.13 A union uses more memory that its corresponding structure.
+   14.14 A member of a structure cannot be a bit field.
+   14.15 It is not possible to change the value of an enumerator.

# A2. FILL IN THE BLANKS

+   14.1 A structure is meant to store ______ data.
+   14.2 A structure is a ______ data type.
+   14.3 The int data type can be abbreviated to INT using ______.
+   14.4 A member of a ______ structure contains a reference to another identical structure.
+   14.5 The members of a ______ share the same region of memory.
+   14.6 Multiple instances of a structure are conveniently stored in an ______.
+   14.7 The size of a union is determined by the member having the ______ _________.
+   14.8 A member of a structure containing one or more bits is known as a ______ ________.
+   14.9 The ______ keyword is used to create a set of named constants.

# A3. MULTIPLE-CHOICE QUESTIONS

14.1 Definition of a structure (A) allocates memory for a structure variable, (B) creates a template, (C) A and B, (D) none of these.

14.2 The following declaration is (A) valid, (B) valid but doesn’t allow creation of a second variable, (C) valid but doesn’t allocate memory, (D) not valid.

```
struct {
    char x;
} x;
```