# ISO/IEC 14882:2017(E)

object (since the function is called, the object is discarded). [Note: No actual type is established for the implicit object of a static member function, and no attempt will be made to determine a conversion sequence for parameter (16.3.3). — end note]

+   5 During overload resolution, the implicit object is indistinguishable from other arguments. The implicit object parameter, retains its identity since user-defined conversions can be applied to achieve a match with it. For non-static member functions declared without a ref-qualifier, an additional rules:
    (5.1) even if the implicit object parameter is not const-qualified, an alias can be bound to the parameter as long as all other arguments can be converted to the type of the implicit object parameter. [Note: that such an argument is an alias does not affect the ranking of implicit conversion sequences (16.3.2). — end note]

+   6 Because than in list-initialization only one user-defined conversion is allowed in an implicit conversion sequence, special rules apply when selecting the best user-defined conversion (16.3.3, 16.3.3). [Example:

```
class T {
public:
    O();
}
class C : T {
public:
    C(int);
}
T a = 1; // ill-formed: T(ci) not tried
// end example]
```

+   7 In case where a candidate is a function template argument, function template specializations are generated using template argument deduction (17.8.3, 17.8.2). Those candidates are then handled as candidates in the usual way.¹¹²⁴ A given name can refer to one or more function templates and also to a set of overloaded non-template functions. In such a case, the candidates generated from each function template are combined with the set of non-template candidate functions.

+   8 A de novo constructor or assignment operator (15.8) that is defined later is excluded from the set of candidate functions in all contexts.

# 16.3.1.1 Function call syntax [over.match.call]

+   1 In a function call (8.2.2)
postfix-expression (expression-list-opt)

if the postfix-expression resolves to a set of overloaded functions and/or templates, overload resolution is applied as in 16.3.1.1. The postfix-expression of an object of class type, overload resolution is applied as in 16.3.1.2.

+   2 If the postfix-expression detects the address of a set of overloaded functions and/function templates, overload resolution is applied using that as described above. If the function selected by overload resolution is a non-static member function, the program is ill-formed. [Note: The resolution of the address of an overload in other contexts is described in 16.4. — end note]

¹⁴ The process of argument deduction fully determines the parameter types of the function template specializations, i.e., the parameters of function template specializations contain no template parameters. Therefore, except where specified otherwise, function template specializations and non-template functions (11.3.5) are treated equivalently for the remainder of overload resolution.

§ 16.3.1.1