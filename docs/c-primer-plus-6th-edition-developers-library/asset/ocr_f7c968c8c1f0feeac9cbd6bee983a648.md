```
printf(" %s at %p\n", pcg, pcg);
printf(" %s at %p\n", auto_string, auto_string);
printf(" %s at %p\n", pcl, pcl);
printf("  %s at %p\n", "Quoted String", "Quoted String");
free(pi);
free(pcl);

return 0;
}
```

Here is the output for one system:

```
static_store: 30 at 00378000
  auto_store: 40 at 0049FB8C
    *pi: 35 at 008E9BA0
String Literal at 00375858
Auto char Array at 0049FB74
Dynamic String at 008E9BD0
  Quoted String at 00375908
```

As you can see, static data, including string literals occupies one region, automatic data a second region, and dynamically allocated data a third region (often called a memory heap or free store).

# ANSI C Type Qualifiers

You’ve seen that a variable is characterized by both its type and its storage class. C90 added two more properties: constancy and volatility. These properties are declared with the keywords const and volatile, which create qualified types. The C99 standard added a third qualifier, restrict, designed to facilitate compiler optimizations. And C11 adds a fourth, _Atomic. C11 provides an optional library, managed by stdatomic.h, to support concurrent programming, and _Atomic is part of that optional support.

C99 granted type qualifiers a new property—they now are idempotent! Although this sounds like a powerful claim, all it really means is that you can use the same qualifier more than once in a declaration, and the superfluous ones are ignored:

```
const const const int n = 6; // same as const int n = 6;
```

This makes it possible, for example, for the following sequence to be accepted:

```
typedef const int zip;
const zip q = 8;
```