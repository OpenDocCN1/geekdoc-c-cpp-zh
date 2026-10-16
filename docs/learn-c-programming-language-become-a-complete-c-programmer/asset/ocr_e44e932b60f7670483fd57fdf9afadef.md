```
draw_all(v); // call draw() for each element
rotate_all(v,45); // call rotate(45) for each element
}// all Shapes implicitly destroyed
```

Now the object is owned by the unique_ptr which will delete the object when it is no longer needed, that is, when its unique_ptr goes out of scope.

For the unique_ptr version of user() to work, we need versions of draw_all() and rotate_all() that accept vector<unique_ptr<Shape>>s. Writing many such _all() functions could become tedious, so §3.4.3 shows an alternative.

# 3.3 Copy and Move

By default, objects can be copied. This is true for objects of user-defined types as well as for builtin types. The default meaning of copy is memberwise copy: copy each member. For example, using complex from §3.2.1.1:

```
void test(complex z1)
{
complex z2 {z1}; // copyinitialization
complex z3;
z3 = z2; // copyassignment
// ...
}
```

Now z1, z2, and z3 have the same value because both the assignment and the initialization copied both members.

When we design a class, we must always consider if and how an object might be copied. For simple concrete types, memberwise copy is often exactly the right semantics for copy. For some sophisticated concrete types, such as Vector, memberwise copy is not the right semantics for copy, and for abstract types it almost never is.

Section 3.3.1 Copying Containers 73

# 3.3.1 Copying Containers

When a class is a resource handle, that is, it is responsible for an object accessed through a pointer, the default memberwise copy is typically a disaster. Memberwise copy would violate the resource handle’s invariant (§2.4.3.2). For example, the default copy would leave a copy of a Vector referring to the same elements as the original:

```
void bad_copy(Vector v1)
{
Vector v2 = v1; // copyv1’srepresentation into v2
v1[0] = 2; // v2[0] is nowalso 2!
v2[1] = 3; // v1[1] is nowalso 3!
}
```

Assuming that v1 has four elements, the result can be represented graphically like this: