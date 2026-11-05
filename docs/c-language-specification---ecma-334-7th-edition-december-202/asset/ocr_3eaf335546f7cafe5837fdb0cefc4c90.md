```
#define B
#if B
    class Class1 {}
#endif
}
```

*end example*

A #define may define a conditional compilation symbol that is already defined, without there being any intervening #undef for that symbol.

*Example:* The example below defines a conditional compilation symbol A and then defines it again.

```
#define A
#define A
```

For compilers that allow conditional compilation symbols to be defined as compilation options, an alternative way for such redefinition to occur is to define the symbol as a compiler option as well as in the source.

*end example*

A #undef may “undefine” a conditional compilation symbol that is not defined.

*Example:* The example below defines a conditional compilation symbol A and then undefines it twice; although the second #undef has no effect, it is still valid.

```
#define A
#undef A
#undef A
```

*end example*

# 6.5.5 Conditional compilation directives

The conditional compilation directives are used to conditionally include or exclude portions of a compilation unit.

```
fragment PP_Conditional
  : PP_If_Section
  | PP_Elif_Section
  | PP_Else_Section
  | PP_Endif
  ;

fragment PP_If_Section
  : 'if' PP_Whitespace PP_Expression
  ;

fragment PP_Elif_Section
  : 'elif' PP_Whitespace PP_Expression
  ;

fragment PP_Else_Section
  : 'else'
  ;

fragment PP_Endif
```