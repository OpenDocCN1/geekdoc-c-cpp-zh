# 13. Statements

# 13.1 General

C# provides a variety of statements.

> *Note:* Most of these statements will be familiar to developers who have programmed in C and C++.
> *end note*

```
statement
: labeled_statement
| declaration_statement
| embedded_statement
;
```

```
embedded_statement
: block
| empty_statement
| expression_statement
| selection_statement
| iteration_statement
| jump_statement
| try_statement
| checked_statement
| unchecked_statement
| lock_statement
| using_statement
| yield_statement
| unsafe_statement    // unsafe code support
| fixed_statement    // unsafe code support
;
```

*unsafe_statement* (§23.2) and *fixed_statement* (§23.7) are only available in unsafe code (§23).

The *embedded_statement* nonterminal is used for statements that appear within other statements. The use of *embedded_statement* rather than *statement* excludes the use of declaration statements and labeled statements in these contexts.

*Example:* The code

```
void F(bool b)
{
    if (b)
        int i = 44;
}
```

results in a compile-time error because an *if* statement requires an *embedded_statement* rather than a *statement* for its *if* branch. If this code were permitted, then the variable *i* would be declared, but it could never be used. Note, however, that by placing *i*'s declaration in a block, the example is valid.

*end example*