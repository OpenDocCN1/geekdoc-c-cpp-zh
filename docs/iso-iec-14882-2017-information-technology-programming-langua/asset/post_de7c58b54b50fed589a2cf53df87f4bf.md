
# ISO/IEC 14882:2017(E)

## 17.6.2.3 Value-dependent expressions

Except as described below, an expression used in a context where a constant expression is required is value-dependent if any subsequence is value-dependent.

An id-expression is value-dependent if:

- (2.1) it is type-dependent,
- (2.2) it is the name of a non-type template parameter,
- (2.3) it names a static data member that is a dependent member of the current instantiation and is initialized in a member-declarator;
- (2.4) it names a static member function that is a dependent member of the current instantiation, or
- (2.5) it is a constant literal that is initialized with an expression that is value-dependent.

Expressions of the following form are value-dependent if the unary-expression or expression is type-dependent:

```
sizeof unary-expression
sizeof ( type-id )
typeid ( expression )
typeid ( type-id )
alignof ( expression )
noexcept ( expression )
```

> Note: For the standard library offsetof, see 21.2. — end note

Expressions of the following form are value-dependent if either the type-id or simple-type is dependent or the expression or cast-expression is value-dependent:

```
simple-type-specifier ( expression-list_opt )
static_cast < type-id > ( expression )
const_cast < type-id > ( expression )
reinterpret_cast < type-id > ( expression )
( type-id ) cast-expression
```

Expressions of the following form are value-dependent:

```
sizeof ... ( identifier )
fold-expression
```

An expression of the form &qualified-id where the qualified-id names a dependent member of the current instantiation is value-dependent. evaluating cast-expression as a constant expression (8.20) succeeds and the result of the evaluation refers to a templated entity that is an object with static or thread storage or a member function.

## 17.6.2.4 Dependent template arguments

- A template-argument is dependent if its type is dependent or the constant expression it specifies
- A non-type template-argument is dependent if the corresponding non-type template-parameter value-dependent.
- Furthermore, a non-type template-argument-the template-argument designates or points to a member of the current instantiation or a member of a dependent type.
- A template-argument is dependent if it names a template-parameter or a qualified-id that refers to a member of an unknown specialization.

# ISO/IEC 14882:2017(E)

## 17.6.3 Non-dependent names

Non-dependent names used in a template definition follow the same name lookup and bound at the point they are used. {Example:

```
void g(double);
void g();

template<class T> class Z {
public:
    void f() {
        g(1); // calls(double)
        h++; // ill-formed: cannot increment function; this could be diagnosed
             // either or at the point of instantiation
    }

    void g(int); // not in scope at the point of the template definition, not considered for the call g(1)
};
```

## 17.6.4 Dependent name resolution

In resolving dependent names, from the following sources of definition are considered:

- (1.1) Declarations that are visible at the point of definition of the template.
- (1.2) Declarations from namespaces associated with the types of the function arguments both from the instantiation context (17.6.4.1) and from the definition context.

### 17.6.4.1 Point of instantiation

1 For a template specialization, a member function specialization, or a specialization for a member function or static member of a class template, if the specialization is implicitly instantiated because it is referenced within another template specialization and the context from which it is referenced is template parameter, the point of instantiation of the specialization is the point of instantiation of the enclosing template. Otherwise, the point of instantiation for such a specialization immediately follows the namespace declaration or definition that refers to the specialization.

2 If a non-specifier or member function of a class template is called in a way which needs the use of a default argument of the function template, the point of instantiation is the point of instantiation of that function template or member function, member function specialization.

3 For a non-specifier-specifier of a template specialization or member function of a class template, if the non-specifier-specifier is implicitly instantiated because it is needed by another template specialization and the context that it depends on a template parameter, the point of instantiation of the non-specifier-specifier is the point of instantiation that it requires. Otherwise, the point of instantiation of the non-specifier-specifier immediately follows the namespace declaration or definition that requires the specialization.

4 For a class specialization, a class member specialization, or a specialization for a class member of class template, if the specialization is implicitly instantiated because it is referenced within another template specialization, if the context from which the specialization depends on a template parameter, and if the specialization is not instantiated previously to the point of instantiation of the enclosing template, the point of instantiation is immediately before the point of instantiation of the enclosing template. Otherwise, the point of instantiation for such a specialization immediately precedes the namespace declaration or definition that refers to the specialization.

5 If a virtual function is implicitly instantiated, its point of instantiation is immediately following the point of instantiation of its enclosing class template specialization.

An explicit instantiation definition is an instantiation point for the specialization or specializations specified by the explicit instantiation.

The instantiation context of an expression that depends on the template arguments is the set of declarations with external link declared prior to the point of instantiation of template specialization in the same translation unit.

A specialization for a function template, a member function, or of static member of a class template may have multiple instantiations within a translation unit, and in addition to the points of instantiation described above, for any specialization that has a point of instantiation within the translation unit, the end of that translation unit is also considered a point of instantiation. A specialization for a class template has at most one point of instantiation in multiple units. If points of instantiation give a template specialization different meanings according to the one-definition rule (6.2), the program is ill-formed, no diagnostic is required.

## 17.6.4 Candidate functions [temp.candidate]

- For a call where the proper-expression is a name, for a call where the proper-expression is a name, the candidate functions are found using the usual lookup rules (6.4.1, 6.4.2) except:

- For the part of the lookup unqualified name lookup (6.4.1), only function declarations from the template definition are found
- For the part of the lookup in associated namespaces (6.4.2), only function declarations found in the template definition context or the template instantiation context are found

If the call would be ill-formed or would find a better match the lookup within the associated namespaces considered all function declarations found in translation units, not just those declarations found in the template definition and instantiation contexts, then the program has undefined behavior.

## 17.6.5 Friend names declared within a class template [temp.inject]

Friend classes or functions can be declared within a class template. When a template is instantiated, the names of its friends are treated as if the specialization had been explicitly declared at its point of instantiation.

With non-template classes, the names of namespace-scope friends of a class template specialization are not visible during an ordinary lookup unless explicitly declared at namespace scope may be found under the rules for associated classes (6.4.2).^{140} (14.3) Example:

```
template<typename T> struct number {
number(int);
 friend gcd(number x, number y) { return 0 };
};

void gcd() {
  number<double> a(3), b(4);
  a = gcd(a,b); // finds gcd because number<double> is an associated class,
  b = gcd(3,4); // making gcd visible in its namespace (global scope)
} // ill-formed: gcd is not visible
```

140) Friend declarations do not introduce new names into any scope, either when the template is declared or when it is instantiated.
