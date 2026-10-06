# ISO/IEC 14882:2017(E)

```
namespace N {
    template<class T1, class T2> class A {}; // primary template
}

using N::A; // refers to the primary template
namespace N {
    template<class T> class A<T, T> {}; // partial specialization
}

A<int,int> a; // uses the partial specialization, which is found through the using-declaration
                               // refers to the primary template

    // end example
```

+   7 A non-type argument is non-specialized if it is the name of a non-type argument. All other non-type arguments are specialized.

+   8 Within the argument list of class template partial specialization, the following restrictions apply:
(8.1) The type of template corresponding to a non-type argument should not be dependent on a parameter of the specialization. [Example:

```
    template<class T, T> struct C {};
    template<class T> struct C<T> {}; // error

    template<int X, int (*array_ptr)[X]> class A {
    int array[5];
    template<int X> class A<X,xray>; // error

    // end example
```

+   (8.2) The specialization should be more specialized than the primary template (17.5.5.2).

+   (8.3) The template parameter list of specialization should not contain default argument values¹138 the template argument list.

+   (8.4) An argument should not contain an unexpaced parameter pack. If an argument is an expansion (17.5.3,1), it should be the last argument in the template argument list.

# 17.5.5.1 Matching of class template partial specializations [temp.class.spec.match]

When a class template is used in a context that requires an instantiation of the class, it is necessary to determine whether the instantiation is to be generated using the primary template or one of the partial specializations. This is done by matching the template arguments of the class template specialization with the template argument list of the partial specializations.

+   (1.1) If exactly one matching specialization is found, the instantiation is generated from that specialization.

+   (1.2) If more than one matching specialization is found, the partial order (17.5.5.2) are used to determine whether one of the specializations is more specialized than the others. If none of the specializations is more specialized than all of the other specializations, then the use of the class template is ambiguous and compilation is ill-formed.

+   (1.3) If no matches are, the instantiation is generated from the primary template.

+   2 A partial specialization matches a class template if the template arguments of the partial specialization can be deduced from the actual template argument list (17.8.2). [Example:

```
template<class T1, class T2, int I> class A {}; // #1
template<class T1, int I> class A<T1, T*, I> {}; // #2
template<class T1, class T2, int I> class A<T1*, T2, I> {}; // #3
```

138 There is no way in which they could be used.

§ 17.5.5.1 ©ISO/IEC 2017 - All rights reserved 365