and such code stands out like the sore thumb it is.

Use of unions can be essential for compactness of data and through that for performance. However, most programs don’t improve much from the use of unions and unions are rather error-prone. Consequently, I consider unions an overused feature; avoid them when you can.

# Section 8.3.1 Unions and Classes 215

# 8.3.1 Unions and Classes

Many nontrivial unions have a member that is much larger than the most frequently used members. Because the size of a union is at least as large as its largest member, space is wasted. This waste can often be eliminated by using a set of derived classes (§3.2.2, Chapter 20) instead of a union.

Technically, a union is a kind of a struct (§8.2) which in turn is a kind of a class (Chapter 16). However, many of the facilities provided for classes are not relevant for unions, so some restrictions are imposed on unions:

+   [1] A union cannot have virtual functions.
+   [2] A union cannot have members of reference type.
+   [3] A union cannot have base classes.
+   [4] If a union has a member with a user-defined constructor, a copy operation, a move operation, or a destructor, then that special function is deleted (§3.3.4, §17.6.4) for that union; that is, it cannot be used for an object of the union type.
+   [5] At most one member of a union can have an in-class initializer (§17.4.4). [6] A union cannot be used as a base class.

These restrictions prevent many subtle errors and simplify the implementation of unions. The latter is important because the use of union is often an optimization and we won’t want “hidden costs” imposed to compromise that.

The rule that delete constructors (etc.) from a union with a member that has a constructor (etc.) keeps simple unions simple and forces the programmer to provide complicated operations if they are needed. For example, since Entry has no member with constructors, destructors, or assignments, we can create and copy Entry freely. For example:

```
void f(Entry a)
{
Entry b = a;
};
```

Doing so with a more complicated union would cause implementation difficulties or errors:

```
union U {
int m1;
complex<double> m2; // complex has a constructor
string m3; // string has a constructor (maintaining a serious invariant)
};
```