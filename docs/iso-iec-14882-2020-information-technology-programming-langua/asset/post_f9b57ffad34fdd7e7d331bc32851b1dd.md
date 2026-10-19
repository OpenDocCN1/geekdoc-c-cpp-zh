
6 A declaration of a name with internal linkage is permitted within a header unit despite all declarations being implicitly exported (10.2).

> [Note 5: A definition that appears in multiple translation units cannot in general refer to such names (6.3). — end note]

A header unit shall not contain a definition of a non-inline function or variable whose name has external linkage.

7 When a module-import-declaration imports a translation unit T, it also imports all translation units imported by exported module-import-declarations in T; such translation units are said to be exported by T. Additionally, when a module-import-declaration in a module unit of some module M imports another module unit U of M, it also imports all translation units imported by non-exported module-import-declarations in the module unit purview of U.102 These rules can in turn lead to the importation of yet more translation units.

8 A module implementation unit shall not be exported.

> [Example 1:
Translation unit #1:
```
module M:Part;
```
Translation unit #2:
```
export module M;
export import :Part;    // error: exported partition :Part is an implementation unit
```
> — end example]

9 A module implementation unit of a module M that is not a module partition shall not contain a module-import-declaration nominating M.

> [Example 2:
```
module M;
import M;            // error: cannot import M in its own unit
```
> — end example]

10 A translation unit has an interface dependency on a translation unit U if it contains a declaration (possibly a module-declaration) that imports U or if it has an interface dependency on a translation unit that has an interface dependency on U. A translation unit shall not have an interface dependency on itself.

> [Example 3:
Interface unit of M1:
```
export module M1;
import M2;
```
Interface unit of M2:
```
export module M2;
import M3;
```
Interface unit of M3:
```
export module M3;
import M1;            // error: cyclic interface dependency M3 → M1 → M2 → M3
```
> — end example]

## 10.4 Global module fragment [module.global.frag]

global-module-fragment:
    module-keyword ; declaration-seqopt

> 1 [Note 1: Prior to phase 4 of translation, only preprocessing directives can appear in the declaration-seq (15.1). — end note]

2 A global-module-fragment specifies the contents of the global module fragment for a module unit. The global module fragment can be used to provide declarations that are attached to the global module and usable within the module unit.

3 A declaration D is decl-reachable from a declaration S in the same translation unit if:
(3.1) — D does not declare a function or function template and S contains an id-expression, namespace-name, type-name, template-name, or concept-name naming D, or
(3.2) — D declares a function or function template that is named by an expression (6.3) appearing in S, or
(3.3) — S contains an expression E of the form
    postfix-expression ( expression-list_opt )
whose postfix-expression denotes a dependent name, or for an operator expression whose operator denotes a dependent name, and D is found by name lookup for the corresponding name in an expression synthesized from E by replacing each type-dependent argument or operand with a value of a placeholder type with no associated namespaces or entities, or
(3.4) — S contains an expression that takes the address of an overloaded function (12.5) whose set of overloads contains D and for which the target type is dependent, or
(3.5) — there exists a declaration M that is not a namespace-definition for which M is decl-reachable from S and either
(3.5.1) — D is decl-reachable from M, or
(3.5.2) — D redeclares the entity declared by M or M redeclares the entity declared by D, and D is neither a friend declaration nor a block-scope declaration, or
(3.5.3) — D declares a namespace N and M is a member of N, or
(3.5.4) — one of M and D declares a class or class template C and the other declares a member or friend of C, or
(3.5.5) — one of D and M declares an enumeration E and the other declares an enumerator of E, or
(3.5.6) — D declares a function or variable and M is declared in D,103 or
(3.5.7) — one of M and D declares a template and the other declares a partial or explicit specialization or an implicit or explicit instantiation of that template, or
(3.5.8) — one of M and D declares a class or enumeration type and the other introduces a typedef name for linkage purposes for that type.
In this determination, it is unspecified
(3.6) — whether a reference to an alias-declaration, typedef declaration, using-declaration, or namespace-alias-definition is replaced by the declarations they name prior to this determination,
(3.7) — whether a simple-template-id that does not denote a dependent type and whose template-name names an alias template is replaced by its denoted type prior to this determination,
(3.8) — whether a decltype-specifier that does not denote a dependent type is replaced by its denoted type prior to this determination, and
(3.9) — whether a non-value-dependent constant expression is replaced by the result of constant evaluation prior to this determination.
4 A declaration D in a global module fragment of a module unit is discarded if D is not decl-reachable from any declaration in the declaration-seq of the translation-unit.
[Note 2: A discarded declaration is neither reachable nor visible to name lookup outside the module unit, nor in template instantiations whose points of instantiation (13.8.5.1) are outside the module unit, even when the instantiation context (10.6) includes the module unit. — end note]
5 [Example 1:
const int size = 2;
int ary1[size];                 // unspecified whether size is decl-reachable from ary1
constexpr int identity(int x) { return x; }
int ary2[identity(2)];         // unspecified whether identity is decl-reachable from ary2

template<typename> struct S;
template<typename, int> struct S2;
constexpr int g(int);
103) A declaration can appear within a lambda-expression in the initializer of a variable.

## ISO/IEC 14882:2020(E)

- (2.1) — the point by which the definition of an exported inline function is required (9.2.8),
- (2.2) — the point by which the definition of an exported function with a placeholder return type is required (9.2.9.6),
- (2.3) — whether a declaration is required not to be an exposure (6.6),
- (2.4) — where definitions for inline functions and templates must appear (6.3, 9.2.8, 13.1),
- (2.5) — the instantiation contexts of templates instantiated before it (10.6), and
- (2.6) — the reachability of declarations within it (10.7).

— end note]

3 [Example 1:
```
export module A;
export inline void fn_e();    // error: exported inline function fn_e not defined
                              // before private module fragment
inline void fn_m();           // OK, module-linkage inline function
static void fn_s();
export struct X;
export void g(X *x) {
    fn_s();                   // OK, call to static function in same translation unit
    fn_m();                   // OK, call to module-linkage inline function
}
export X *factory();          // OK

module :private;
struct X {};
                       // definition not reachable from importers of A
X *factory() {
    return new X();
}
void fn_e() {}
void fn_m() {}
void fn_s() {}
```
— end example]

## 10.6 Instantiation context [module.context]

1 The instantiation context is a set of points within the program that determines which names are visible to argument-dependent name lookup (6.5.3) and which declarations are reachable (10.7) in the context of a particular declaration or template instantiation.

2 During the implicit definition of a defaulted function (11.4.4, 11.11.1), the instantiation context is the union of the instantiation context from the definition of the class and the instantiation context of the program construct that resulted in the implicit definition of the defaulted function.

3 During the implicit instantiation of a template whose point of instantiation is specified as that of an enclosing specialization (13.8.5.1), the instantiation context is the union of the instantiation context of the enclosing specialization and, if the template is defined in a module interface unit of a module M and the point of instantiation is not in a module interface unit of M, the point at the end of the declaration-seq of the primary module interface unit of M (prior to the private-module-fragment, if any).

4 During the implicit instantiation of a template that is implicitly instantiated because it is referenced from within the implicit definition of a defaulted function, the instantiation context is the instantiation context of the defaulted function.

5 During the instantiation of any other template specialization, the instantiation context comprises the point of instantiation of the template.

6 In any other case, the instantiation context at a point within the program comprises that point.

7 [Example 1:
Translation unit #1:
```
export module stuff;
export template<typename T, typename U> void foo(T, U u) { auto v = u; }
export template<typename T, typename U> void bar(T, U u) { auto v = *u; }
```
