# ISO/IEC 14882:2020(E)

```
f(0);
 f((int*)0);
 g(true);
 g(0);
```

// selects #1
// selects #2
// selects #3 because C1<bool> is not satisfied
// selects #4

— end example]

# 13.6 Type equivalence [temp.type]

1 Two template-ids are the same if

+   (1.1) — their template-names, operator-function-ids, or literal-operator-ids refer to the same template, and
+   (1.2) — their corresponding type template-arguments are the same type, and
+   (1.3) — their corresponding non-type template-arguments are template-argument-equivalent (see below) after conversion to the type of the template-parameter, and
+   (1.4) — their corresponding template template-arguments refer to the same template.

Two template-ids that are the same refer to the same class, function, or variable.

2 Two values are template-argument-equivalent if they are of the same type and

+   (2.1) — they are of integral type and their values are the same, or
+   (2.2) — they are of floating-point type and their values are identical, or
+   (2.3) — they are of type std::nullptr_t, or
+   (2.4) — they are of enumeration type and their values are the same,136 or
+   (2.5) — they are of pointer type and they have the same pointer value, or
+   (2.6) — they are of pointer-to-member type and they refer to the same class member or are both the null member pointer value, or
+   (2.7) — they are of reference type and they refer to the same object or function, or
+   (2.8) — they are of array type and their corresponding elements are template-argument-equivalent,137 or
+   (2.9) — they are of union type and either they both have no active member or they have the same active member and their active members are template-argument-equivalent, or
+   (2.10) — they are of class type and their corresponding direct subobjects and reference members are template-argument-equivalent.

3 [Example 1:

```
template<class E, int size> class buffer { /* ... */ };
buffer<char,2*512> x;
buffer<char,1024> y;
```

declares x and y to be of the same type, and

```
template<class T, void(*err_fct)()> class list { /* ... */ };
list<int,&error_handler1> x1;
list<int,&error_handler2> x2;
list<int,&error_handler2> x3;
list<char,&error_handler2> x4;
```

declares x2 and x3 to be of the same type. Their type differs from the types of x1 and x4.

```
template<class T> struct X { };
template<class> struct Y { };
template<class T> using Z = Y<T>;
X<Y<int> > y;
X<Z<int> > z;
```

declares y and z to be of the same type. — end example]

4 If an expression e is type-dependent (13.8.3.3), decltype(e) denotes a unique dependent type. Two such decltype-specifiers refer to the same type only if their expressions are equivalent (13.7.7.2).

> [Note 1: However, such a type can be aliased, e.g., by a typedef-name. — end note]

136) The identity of enumerators is not preserved.
137) An array as a template-parameter decays to a pointer.