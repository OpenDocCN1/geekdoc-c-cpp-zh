# ISO/IEC 14882:2017(E)

unknown or of incomplete element type, is an incompletely-defined object type.46 Incompletely-defined object types and void are incomplete types (6.9.1). Objects should not be defined to be an incomplete type.

+   A class type (as "class X") might be incomplete at one point in a translation unit and complete later; the type "class X" is the same at both points. The declared type of an array object might be an array of incomplete class type and therefore incomplete; if the class is incomplete later in the translation unit, the array becomes complete; the array at two points is the same type. The declared type of an array object might be an array of unknown bound and therefore incomplete at one point in a translation unit and complete later; the array at two points ("array of NT") are the same type. A pointer to unknown bound, or of a type defined by a typedef of unknown bound, cannot be completed. [Example:

```
class X;
extern X x;
int arr[];
typedef int UNKA;
UNKA*;
UNKA** arr;

void foo() {
px++;
arr++;
arr++;
}

struct { int i; };nint arr[10];

X;
void bar() {
px = &x;
arr = &arr;
px++;
arr++;
}

-- example --
```

+   [Note: The rules for declarations and expressions describe in which contexts incomplete types are prohibited;
-- end note]

+   An object type is a (possibly cv-qualified) type that is not a function type, not a reference, and not void.

+   Arithmetic types (6.9.1), enumeration types, pointer to member types (6.9.2), std::null_ptr, and cv-qualified (6.9.3) versions of these types are collectively called scalar types. Scalar types, POD classes (Clause 12), arrays of such types and cv-qualified versions of these are collectively called POD types. Cv-qualified scalar types, trivially copyable class types (Clause 12), arrays of such types, and cv-qualified versions of these are collectively called trivially copyable types. Scalar types, trivial class types (Clause 12), arrays of such types and cv-qualified versions of these types are collectively called trivial types. Scalar types, standard-layout class types (Clause 12), arrays of such types and cv-qualified versions of these types are collectively called standard-layout types.

+   A type is a literal type if it is:

> 46 The size and layout of an instance of an incomplete-defined object type is unknown.