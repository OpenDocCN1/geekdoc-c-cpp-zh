```
}
case 5:
    h();
case 4:                         // implementation may warn on fallthrough
    i();
    [[fallthrough]];              // error
}

— end example]
```

# 9.12.6  Likelihood attributes                                      [dcl.attr.likelihood]

The *attribute-tokens* likely and unlikely may be applied to labels or statements. The *attribute-tokens* likely and unlikely shall appear at most once in each *attribute-list* and no *attribute-argument-clause* shall be present. The *attribute-token* likely shall not appear in an *attribute-specifier-seq* that contains the *attribute-token* unlikely.

*Recommended practice:* The use of the likely attribute is intended to allow implementations to optimize for the case where paths of execution including it are arbitrarily more likely than any alternative path of execution that does not include such an attribute on a statement or label. The use of the unlikely attribute is intended to allow implementations to optimize for the case where paths of execution including it are arbitrarily more unlikely than any alternative path of execution that does not include such an attribute on a statement or label. A path of execution includes a label if and only if it contains a jump to that label.

> [*Note 1:* Excessive usage of either of these attributes is liable to result in performance degradation. — *end note*]

```
[*Example 1:*

    void g(int);
    int f(int n) {
        if (n > 5) [[unlikely]] {       // n > 5 is considered to be arbitrarily unlikely
            g(0);
            return n * 2 + 1;
        }

        switch (n) {
        case 1:
            g(1);
            [[fallthrough]];

        [[likely]] case 2:               // n == 2 is considered to be arbitrarily more
            g(2);                         // likely than any other value of n
            break;
        }
        return 3;
    }

— end example]
```

# 9.12.7  Maybe unused attribute                                      [dcl.attr.unused]

The *attribute-token* maybe_unused indicates that a name or entity is possibly intentionally unused. It shall appear at most once in each *attribute-list* and no *attribute-argument-clause* shall be present.

The attribute may be applied to the declaration of a class, a *typedef-name*, a variable (including a structured binding declaration), a non-static data member, a function, an enumeration, or an enumerator.

A name or entity declared without the maybe_unused attribute can later be redeclared with the attribute and vice versa. An entity is considered marked after the first declaration that marks it.

*Recommended practice:* For an entity marked maybe_unused, implementations should not emit a warning that the entity or its structured bindings (if any) are used or unused. For a structured binding declaration not marked maybe_unused, implementations should not emit such a warning unless all of its structured bindings are unused.