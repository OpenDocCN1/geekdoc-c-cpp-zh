The processing of a #define directive causes the given conditional compilation symbol to become defined, starting with the source line that follows the directive. Likewise, the processing of a #undef directive causes the given conditional compilation symbol to become undefined, starting with the source line that follows the directive.

Any #define and #undef directives in a source file must occur before the first token (§2.4) in the source file; otherwise, a compile-time error occurs. In intuitive terms, #define and #undef directives must precede any “real code” in the source file.

The example

```
#define Enterprise
#if Professional || Enterprise
    #define Advanced
#endif

namespace Megacorp.Data
{
    #if Advanced
    class PivotTable {...}
    #endif
}
```

is valid because the #define directives precede the first token (the namespace keyword) in the source file.

The following example results in a compile-time error because a #define follows real code:

```
#define A
namespace N
{
    #define B
    #if B
    class Class1 {}
    #endif
}
```

A #define may define a conditional compilation symbol that is already defined, without there being any intervening #undef for that symbol. The example below defines a conditional compilation symbol A and then defines it again.

```
#define A
#define A
```

A #undef may “undefine” a conditional compilation symbol that is not defined. The example below defines a conditional compilation symbol A and then undefines it twice; although the second #undef has no effect, it is still valid.

```
#define A
#undef A
#undef A
```