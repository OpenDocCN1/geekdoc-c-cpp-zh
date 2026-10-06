# ISO/IEC 14882:2017(E)

```
X a(1);
X b = f(X(2));
Y c = g(Y(3));
a = f(a);
```

X(2) is constructed in the space used to hold f()'s argument and Y(3) is constructed in the space used to hold g()'s argument. Likewise, f()'s result is constructed in b and g()'s result is constructed directly in c. On the other hand, the expression a = f(a)operator(const A&) can bind to. it is materialized using only the reference object of type A: — example

+   3 When an object of type X is passed or returned from a function, if X is deleted or if at least one non-deleted copy or move constructor exists, implementations are permitted to create a copy to hold the function parameter or result object. The object shall be constructed from the function argument or reference, respectively, and if the non-deleted trivial constructor is inaccessible or not selected by overload resolution to perform the copy or move of the object, its lifetime is granted to be passed to returned from functions in registers. — note

+   4 When an implementation introduces an object of a class that has a non-trivial constructor (15.1, 15.8), it shall be called for a parameter with a non-trivial destructor (15.4). Temporary objects are destroyed as the last step in evaluating the full-expression (4.6) that contains the points where they are created. This is true even if evaluation ends throwing an exception. The temporary values are associated only with the full-expression, not any specific sub-expression. There are three contexts in which a temporary is destroyed before the end of the full-expression. The first context is when a temporary is called to initialize an element of an array with no corresponding initializer (11.6). The second context is when a copy constructor is called to copy an element of an array where the entire array is copied (15.2, 15.8). In either case, if the constructor has one or more default arguments, the destruction of every temporary created in a default argument is sequenced before the construction of next array element, if any.

+   6 The third context is when a reference is bound to a temporary.¹¹¹⁶ The temporary to which the reference is bound or the temporary shall be the complete object of class type to which the reference persists for the lifetime of the reference except

+   (6.1) A temporary object bound to a reference parameter in a function call (8.2.2) persists until the completion of the full-expression containing the call.

+   (6.2) The lifetime of a temporary bound to the returned value in a function return statement (9.6.3) is not extended; the temporary is destroyed at the end of the full-expression in the return statement.

+   (6.3) A temporary bound to a reference in a new-initializer (8.3.4) persists until the completion of the full-expression containing the new-initializer. [Example]:

```
struct S { int mi; const std::pair<int,int>& m; };nS a {1, {2, 3}};
S* p = new S(1, 2); // dangling reference
```

— example [Note]: This may introduce a dangling reference, and implementations should include a warning in such a case. — note

7 The destruction of a temporary whose lifetime is not extended by being bound to a reference is sequenced before the destruction of every temporary created earlier in the full-expression. The lifetime of two or more temporaries whose references are bound ends at the same point, these temporaries

¹¹¹⁶ The same rules apply to initialization of an initializer_list object (11.6.4) with its underlying temporary array.

§ 15.2 ©ISO/IEC 2017 – All rights reserved 282