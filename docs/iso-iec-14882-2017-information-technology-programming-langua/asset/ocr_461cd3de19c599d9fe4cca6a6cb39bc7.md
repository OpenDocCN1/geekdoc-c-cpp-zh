# ISO/IEC 14882:2017(E)

4 A template-parameter P is at least specialized as a template-argument A, if the following rewrite to two function templates, the function corresponding to P is at least specialized as the function template corresponding to A according the partial ordering rules for function templates (17.5.6.2). Given an instance class X with the template list of A (including default arguments):

+   (4.1) Each of the two functions has the same template parameters, respectively, as P or A.
(4.2) Each function template has a single function parameter whose is a specialization of X with arguments corresponding to the respective function template where, for each template parameter PP in the template list of the function, a corresponding template AA is formed. If (17.5.3); otherwise, AA is the id-expression PP.

If the rewrite produces an invalid type, P is not at least specialized as A.

# 17.4 Type equivalence [temp.type]

+   1 Two template-ids refer to the same class, function, or literal if
(1.1) their template-names, operator-function-ids, or literal-oper refer to the same template and
(1.2) their corresponding type-arguments are the same type and
(1.3) their corresponding non-type template-arguments of integral or enumeration have identical values and
(1.4) their corresponding non-type template-arguments of pointer type refer to the same object or function or are both the null value
(1.5) their corresponding non-type template-arguments of pointer-to-member type refer to the same class member or are both the null member value
(1.6) their corresponding non-type template-arguments of reference type refer to the same object or function and
(1.7) their corresponding template-arguments refer to the same template.

```
Example:
template<class E, int size> class buffer { /* ... */ };
buffer<char,256> x;
buffer<char,1024> y;

declare x and y to be of the same type, and
template<class T, void (*)(error_handler)> class list { /* ... */ };
list<int,error_handler> x1;
list<int,error_handler> x2;
list<int,error_handler> x3;
list<char,error_handler> x4;

declare x2 and x3 to be of the same type. Their type differs from x1 and x4.
template<class T> struct X { };
template<class T> struct Y { };
template<class T> using Z = Y<T>;
X<int> y;
X<int> z;
```

declare y and z to be of the same type. -- end example

2 If an expression e is type-dependent (17.6.2.2), decltype(e) denotes a unique type. Two such decltype-specifiers refer to the same type only if their expressions are equivalent (17.5.6.1). [Note: However,

§ 17.4 ©ISO/IEC 2017 - All rights reserved 354