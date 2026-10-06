# ISO/IEC 14882:2017(E)

```
template void N::<double>::mf();
// OK: explicit instantiation in namespace N
// end example
```

9 A trailing-argument can be left unspecified in an explicit instantiation of a template specialization or of a member template specialization it can be deduced from the type of the function parameter (17.8.2). [Example:

```
template<class T> class Array{ /* ... */ };
template<class T> void sort(array<T>&) { /* ... */ };

// instantiate sort(array<int>); - template-argument deduced
template void sort(array<int>);
// end example
```

8 An explicit instantiation names a class template specialization is also an explicit instantiation of the same declaration (or definition) of each members (including members inherited from base classes and other templates) that has not been previously specialized in the translation unit containing the explicit instantiation, as described. [Note: In addition, it will typically be an explicit instantiation of certain implementation-data about the class. — end note

9 An explicit instantiation defines that a class template specialization instantiates the class template specialization and is an explicit instantiation of only those members that have been defined at the point of instantiation.

10 Except for inline variables and declarations, variables deduced from their initializer or value (10.7.4), const variables of type, and class specializations, explicit declarations have the effect of suppressing the implicit instantiation of the entity in the same translation unit. [Note: The intent is that an inline function that is subject of an explicit instantiation will be used in a way that would otherwise cause an implicit instantiation when used out (6.2) so that the body may be considered for inlining, but that no out-of-line code of the inline function would be generated in the translation unit. — end note]

11 If an entity is subject of both an explicit instantiation declaration and an explicit instantiation definition, the definition shall follow the declaration. An entity that is subject of an explicit instantiation declaration and is used also (17.7.3) in the translation unit which is the subject of an explicit instantiation definition in the program is inline by default. [Note: This rule applies only to inline functions and has no other normative effect. This is needed to ensure that if the address of an inline function is in a translation unit in which the implementation chooses to suppress the out-of-line body, another translation unit will supply the body. — end note] An explicit instantiation shall not name a specialization of the template

12 The access checking rules do not apply to names used to specify explicit instantiations. [Note: In particular, the template parameters and names used in the function declator (parameter types, return type, exception specifications) may be private types or objects which would normally not be accessible and the template may be a member template or member function which would normally not be accessible. — end note]

13 An explicit instantiation does not constitute a use of a default argument, so default instantiation is not done. [Example:

```
char* p =;
template<class T> T g(T x, &p) { return x; }
template int g<int>(int);
// OK even though p isn't an int.
// end example
```