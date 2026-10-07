# A.2.4 External definitions

(6.9) translation-unit:

external-declaration
translation-unit external-declaration

(6.9) external-declaration:

function-definition
declaration

(6.9.1) function-definition:

declaration-specifiers declarator declaration-listopt compound-statement

(6.9.1) declaration-list:

declaration
translation-list declaration

# A.3 Preprocessing directives

(6.10) preprocessing-file:

group-opt

(6.10) group:

group-part
group group-part

(6.10) group-part:

if-section
control-line
# non-directive

(6.10) if-section:

if-group elif-groupsopt else-groupopt opt endif-line

(6.10) if-group:

```
# if constant-expression new-line groupopt
# ifdef identifier new-line groupopt
# ifndef identifier new-line groupopt
```

(6.10) elif-groups:

elif-group
group-groups elif-group

(6.10) elif-group:

```
# elif constant-expression new-line groupopt
```