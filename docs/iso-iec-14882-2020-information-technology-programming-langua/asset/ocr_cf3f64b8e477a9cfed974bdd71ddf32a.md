# ISO/IEC 14882:2020(E)

(1.3) — Containers, iterators, and algorithms that meet an interface convention or model a concept

2 The string and iostream components use an explicit representation of operations required of template arguments. They use a class template char_traits to define these constraints.

3 Interface convention requirements are stated as generally as possible. Instead of stating “class X has to define a member function operator++()”, the interface requires “for any object x of class X, ++x is defined”. That is, whether the operator is a member is unspecified.

4 Requirements are stated in terms of well-defined expressions that define valid terms of the types that meet the requirements. For every set of well-defined expression requirements there is either a named concept or a table that specifies an initial set of the valid expressions and their semantics. Any generic algorithm (Clause 25) that uses the well-defined expression requirements is described in terms of the valid expressions for its template type parameters.

5 The library specification uses a typographical convention for naming requirements. Names in italic type that begin with the prefix Cpp17 refer to sets of well-defined expression requirements typically presented in tabular form, possibly with additional prose semantic requirements. For example, Cpp17Destructible (Table 32) is such a named requirement. Names in constant width type refer to library concepts which are presented as a concept definition (Clause 13), possibly with additional prose semantic requirements. For example, destructible (18.4.10) is such a named requirement.

6 Template argument requirements are sometimes referenced by name. See 16.3.3.3.

7 In some cases the semantic requirements are presented as C++ code. Such code is intended as a specification of equivalence of a construct to another construct, not necessarily as the way the construct must be implemented.157

8 Required operations of any concept defined in this document need not be total functions; that is, some arguments to a required operation may result in the required semantics failing to be met.

> [Example 1: The required < operator of the totally_ordered concept (18.5.4) does not meet the semantic requirements of that concept when operating on NaNs. — end example]

This does not affect whether a type models the concept.

9 A declaration may explicitly impose requirements through its associated constraints (13.5.3). When the associated constraints refer to a concept (13.7.9), the semantic constraints specified for that concept are additionally imposed on the use of the declaration.

# 16.3.2.4 Detailed specifications [structure.specifications]

1 The detailed specifications each contain the following elements:

+   (1.1) — name and brief description
+   (1.2) — synopsis (class definition or function declaration, as appropriate)
+   (1.3) — restrictions on template arguments, if any
+   (1.4) — description of class invariants
+   (1.5) — description of function semantics

2 Descriptions of class member functions follow the order (as appropriate):158

+   (2.1) — constructor(s) and destructor
+   (2.2) — copying, moving & assignment functions
+   (2.3) — comparison operator functions
+   (2.4) — modifier functions
+   (2.5) — observer functions
+   (2.6) — operators and other non-member functions

3 Descriptions of function semantics contain the following elements (as appropriate):159