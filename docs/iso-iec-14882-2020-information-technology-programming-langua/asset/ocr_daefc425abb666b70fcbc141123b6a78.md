```
extern "C" void f5() {
    extern void f4();
}

extern void f4();

void f6() {
    extern void f4();
}
— end example]
```

A C language linkage is ignored in determining the language linkage of the names of class members and the function type of class member functions.

[Example 3:

```
extern "C" typedef void FUNC_c();

class C {
    void mf1(FUNC_c*);
    // the name of the function mf1 and the member function's type have
    // C++ language linkage; the parameter has type "pointer to C function"

    FUNC_c mf2;
    // the name of the function mf2 and the member function's type have
    // C++ language linkage

    static FUNC_c* q;
    // the name of the data member q has C++ language linkage and
    // the data member's type is "pointer to C function"
};

extern "C" {
    class X {
        void mf();
        // the name of the function mf and the member function's type have
        // C++ language linkage

        void mf2(void(*)());
        // the name of the function mf2 has C++ language linkage;
        // the parameter has type "pointer to C function"
    };
}
— end example]
```

6 If two declarations declare functions with the same name and parameter-type-list (9.3.4.6) to be members of the same namespace or declare objects with the same name to be members of the same namespace and the declarations give the names different language linkages, the program is ill-formed; no diagnostic is required if the declarations appear in different translation units. Except for functions with C++ linkage, a function declaration without a linkage specification shall not precede the first linkage specification for that function. A function can be declared without a linkage specification after an explicit linkage specification has been seen; the linkage explicitly specified in the earlier declaration is not affected by such a function declaration.

7 At most one function with a particular name can have C language linkage. Two declarations for a function with C language linkage with the same function name (ignoring the namespace names that qualify it) that appear in different namespace scopes refer to the same function. Two declarations for a variable with C language linkage with the same name (ignoring the namespace names that qualify it) that appear in different namespace scopes refer to the same variable. An entity with C language linkage shall not be declared with the same name as a variable in global scope, unless both declarations denote the same entity; no diagnostic is required if the declarations appear in different translation units. A variable with C language linkage shall not be declared with the same name as a function with C language linkage (ignoring the namespace names that qualify the respective names); no diagnostic is required if the declarations appear in different translation units.

> [Note 4: Only one definition for an entity with a given name with C language linkage can appear in the program (see 6.3); this implies that such an entity must not be defined in more than one namespace scope. — end note]