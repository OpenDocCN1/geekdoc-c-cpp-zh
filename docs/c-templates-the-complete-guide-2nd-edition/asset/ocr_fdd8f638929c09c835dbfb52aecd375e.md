| Classification | Explanation and Notes |
|---|---|
| Qualified name | This term is not defined in the standard, but we use it to refer to names that undergo *qualified lookup*. Specifically, this is a qualified-id or an unqualified-id that is used after an explicit member access operator (`.` or `->`). Examples are `S::x`, `this->f`, and `p->A::m`. However, just `Class_mem` in a context that is implicitly equivalent to `this->class_mem` is not a qualified name: The member access must be explicit. |
| Unqualified name | An unqualified-id that is not a qualified name. This is not a standard term but corresponds to names that undergo what the standard calls *unqualified lookup*. |
| Name | Either a qualified or an unqualified name. |

*Table 13.1. Name Taxonomy (Part 1)*

| Classification | Explanation and Notes |
|---|---|
| Dependent name | A name that depends in some way on a template parameter. Typically, a qualified or unqualified name that explicitly contains a template parameter is dependent. Furthermore, a qualified name that is qualified by a member access operator (`.` or `->`) is typically dependent if the type of the expression on the left of the access operator is *type-dependent*, a concept that is discussed in Section 13.3.6 on page 233. In particular, `b` in `this->b` is generally a dependent name when it appears in a template. Finally, a name that is subject to argument-dependent lookup (described in Section 13.2 on page 217), such as `ident` in a call of the form `ident(x, y)` or `+` in the expression `x + y`, is a dependent name if and only if any of the argument expressions is type-dependent. |
| Nondependent name | A name that is not a dependent name by the above description. |

*Table 13.2. Name Taxonomy (Part 2)*

It is useful to read through the tables to gain some familiarity with the terms that