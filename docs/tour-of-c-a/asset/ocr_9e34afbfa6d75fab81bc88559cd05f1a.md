If you are explicit about some defaults, other default definitions will not be generated.

When a class has a pointer member, it is usually a good idea to be explicit about copy and move operations. The reason is that a pointer may point to something that the class needs to delete, in which case the default member would be wrong. Alternatively, one might point to something that the class needs to delete. In either case, the code would like to know. For an example, see $6.2.1.

A good rule of thumb (sometimes the rule of zero) is to either define all the essential operations or none (using the default for all). For example:

Click here to view code image

```
struct Z {
  Vector v;
  string s;
};

Z z1; // Default initialize z1.v and z1.s
Z z2 = z1; // Default copy z1.v and z1.s
```

Here, the compiler will synthesize member default construction, copy, move, and destructor as needed, and with the correct semantics.

To complement =default =delete to indicate that an operation is not to be generated. A base class in a class hierarchy is the classic example where we don't want allow a member copy. For example:

Click here to view code image

```
class Shape {
public:
  Shape(const Shape&)=delete; // No copying
  Shape& operator=(const Shape&)=delete;
  // ...
};

void copy(Shape& s1, const Shape& s2)
{
  s1 = s2; // Error: Shape copy is deleted
}
```

A =delete makes use of the deleted function a compile-time error; =delete can be used to suppress any function, not just essential member functions.

# 6.1.2 Conversions

A constructor taking a single argument defines a conversion from its argument type. For example, complex (§5.2.1) provides a constructor from a double:

Click here to view code image

```
complex z1 = 3.14; // z1 becomes (3.14,0.0)
complex z2 = *z1; // z2 becomes z1*(2.0,0) == (6.28,0.0)
```

This implicit conversion is sometimes ideal, but not always. For example, Vector (§5.2.2)