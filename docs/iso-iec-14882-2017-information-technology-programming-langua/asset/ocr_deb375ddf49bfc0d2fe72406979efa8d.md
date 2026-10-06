# ISO/IEC 14882:2017(E)

```
noexcept-specifier:
    noexcept ( constant-expression )
    noexcept
    throw ()
```

# A.14 Preprocessing directives [gram.cpp]

```
preprocessing-file:
    preprocessing_opt
    group:
        group-part
            group group-part
    group-part:
        control-line
        if-section
            text-line
                # conditionally-supported-directive
```

```
control-line:
    # include pp-tokens new-line
    # define identifier replacement-list-new-line
    # define identifier (parern identifier-list_opt ) replacement-list-new-line
    # define identifier (parern ... ) replacement-list-new-line
    # define identifier (parern identifier-list , ... ) replacement-list-new-line
    # identifier new-line
    # line pp-tokens new-line
    # error pp-tokens_opt new-line
    # pragma new-line
    # new new-line
```

```
if-section:
    if-group elif-groups_opt else-group_opt endif-line
```

```
if-group:
    # if constant-expression new-line group_opt
    # ifdef identifier new-line group_opt
```

```
elif-group:
    elif-group identifier new-line group_opt
```

```
elif-group:
    # elif constant-expression new-line group_opt
```

```
else-group:
    # else new-line group_opt
```

```
endif-line:
    # endif new-line
```

```
text-line:
    pp-tokens_opt new-line
    conditionally-supported-directive:
    pp-tokens new-line
```

```
lparen:
    a ( character not immediately preceded by whitespace
```