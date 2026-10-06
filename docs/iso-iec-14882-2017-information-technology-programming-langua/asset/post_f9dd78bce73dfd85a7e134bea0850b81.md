
# ISO/IEC 14882:2017(E)

+   in each definition of D, a default argument used by an (implicit or explicit) function call is treated as if its token sequence were present in the definition of D; that the default argument is subject to the requirements described in this paragraph (and, if the default argument has subexpressions with default arguments, this requirement applies recursively);

+   if D is a class with an implicitly-declared constructor (15.1), it is as if the constructor is implicitly defined in every translation unit unless it is od-r, and the implicit definition in every translation unit shall call the same constructor for a subobject of D. [Example:

```
// translation unit 1:
struct X {
    X(int);
    X(int, int, int);
};
X::X(int, int = 0) { }
class D {
    X x = 0;
};
D d1;
```

```
// translation unit 2:
struct X {
    X(int);
    X(int, int);
};
X::X(int, int = 0, int = 0) { }
class D {
    X x = 0;
};
D d2;
```

end example |
If D is a template and defined in more than one translation unit, the preceding requirements shall apply to both names from names the template’s scope used in the template definition (17.6.3), and also to dependent names at the point of instantiation (17.6.2). If the definitions of D satisfy all these requirements, the behavior is as if there were a single definition of D. If the definitions of D do not satisfy these requirements, the behavior is undefined.

## 6.3 Scope [basic.scope.declarative]

### 6.3.1 Declaration regions and scopes

Every name is introduced in some portion of program text called a declarative region, which is the largest part of the program in that name is valid, in that name may be used as an unqualified name to refer to the same entity. In general, each particular declaration is valid within some possibly discontinuous portion of program text called its scope. To determine the scope of a declaration, it is sometimes necessary to refer to the potential scope of a declaration. The scope of a declaration is the same as its potential scope unless that scope contains another declaration of the name. In that case, the potential scope of the declaration in the inner (containing) declarative region is excluded from the scope of the declaration in the outer (containing) region.

Example:

```
int j = 24;
```

11.3.6 describes how default argument names are looked up.

# ISO/IEC 14882:2017(E)

```
int main() {
    int i = j, j;
    j = 42;
}
```

the identifier j declared as a name (and used twice). The declarative region of the first j includes the entire example. The potential scope of the first j begins immediately after j and extends to the end of the program, but its (actual) scope excludes the text between the ',' and the '.'. The declarative region of the second declaration of j (the j immediately before the semicolon) includes all the text between { and }; but its potential scope excludes the declaration of j. The scope of the second declaration of j is the same as its potential scope. — end example

The names declared as a class are introduced into the scope which the declaration occurs, except the presence of a friend identifier (14.3), certain uses of the elaborated-type-specifier (10.1.7.3), and using-directives (10.3.4) after this general.

+   Given a set of declarations in a single declaration region, each of which the same name unqualified,
(4.1) exactly one declaration shall declare a class or enumeration name that is not a typedef name
and the other declarations shall refer to the same variable, non-static data member, or enumerator; or refer to functions and templates; in this case the class name or enumeration name is hidden (6.3.10). [Note: A namespace or a class name must be unique in its declaration region (10.3.2). Else, — end note]

> Note: These restrictions apply to the declaration region which is introduced, which is not necessarily the same as the region where the declaration occurs. In particular, elaborated-type-specifier (10.1.7.3) and friend declarations (14.3) may introduce a (possibly not) name into an enclosing namespace; these restrictions apply to both regions. Local declarations (6.5) may introduce a name into the declaration region where the declaration appears and also introduce a (possibly not) name into an enclosing namespace; these restrictions apply to both regions. — end note

+   5 Note: The name lookup rules are summarized in 6.4. — end note

### 6.3.2 Point of declaration

```
[basic.scope.pdecl]
```

The point of declaration for a name is immediately after its complete declar (Clause 11) and before its initializer (if any), except noted below. [Example]:

```
unsigned x = 12;
{ unsigned x = x; }
```

Here the second x is initialized with its (indeterminate) value. — end example

+   Note: A name from an outer scope remains visible up to the point of declaration of the name hides it. [Example]:

```
const int i = 2;
{ int i = 1 };
```

declares a block-scope array of two integers. — end

The point of declaration for a class or template is immediately after the identifier-specifier (if any) in its scope. The point of declaration for a class or template is immediately after the identifier-specifier (if any) in its scope. The point of declaration for a class or template is immediately after the identifier-specifier (if any) in its scope. The point of declaration for a class or template is immediately after the identifier-specifier (if any) in its scope. The point of declaration for a class or template is immediately after the identifier-specifier (if any) in its scope. (10.2) The point of declaration of an alias immediately follows the using-declarator to which the alias refers.

+   4 The point of declaration of a using-declarator that does not have a constructor is immediately after the using-declarator (10.3). § 6.3.2 ISO/IEC 14882:2017(E)

5 The point of declaration for an enumerator is immediately after its *enumerator-definition*. [Example:

```
const int x = 12;
enum E { x };
```

Here the enumerator x is initialized as a class member, the value of the constant. — end example

6 After the point of declaration of a class member, the member name can be looked up in the scope of its class. [Note: This is true even if the class is incomplete. For example,

```
struct X {
enum E { x };
};
int b[x]; // OK
``` — end note

7 The point of declaration of an elaborated-type-specifier is as follows:

+   (7.1) — for a declaration of the form

class-key attribute-specifier-seq-opt identifier;
the *identifier* is declared to be a *class-name* in the scope that contains the declaration; except as a friend, the *identifier* is declared in the smallest namespace or block that [Note: Other forms of elaborated-type-specifier do not declare a new name, and must refer to an enclosing type. See 6.4.4 and 10.1.7.3. — end note]

8 The point of declaration for an injected-class-name (Clause 12) is immediately following the opening brace of the class definition.

9 The point of declaration for a function-local variable (11.4) is immediately before the *function-body* of a function.

10 The point of declaration for a template parameter is immediately after its *template-parameter*. [Example:

```
typedef unsigned char T;
template<class T>
// lookup the typedef name of unsigned char
T = O struct A };
```— end example]

11 Note: Declaration refers to functions or classes that are members of the nearest enclosing namespace, but they do not introduce new names into that namespace (10.3.2). Function declarations at block scope and variables with the *extern* at block scope refer to declarations that are members of an enclosing namespace, but they do not introduce new names into that scope. — end note

12 Note: For point of instantiation of a template, see 17.6.4.1. — end note

### 6.3.3 Block scope

1 A name declared in a block (9.3) refers to that block; it has block scope. Its potential scope begins at its point of declaration (6.3.2) and ends at the end of its block. A variable declared block scope is a *local variable*.
