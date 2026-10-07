# 7.19 Common definitions <stddef.h>

The header <stddef.h> defines the macros and declares the following types. Are also defined in other headers, as noted in their respective subclauses.

The types are

```
ptrdiff_t
```

which is the signed integer type of the result of subtracting two pointers;

```
size_t
```

which is the unsigned integer type of the result of the sizeof operator;

```
max_align_t
```

which is an object type whose alignment is as great as is supported by the implementation in all contexts; and

```
char_t
```

which is an integer type whose range of values can represent distinct codes for all members of the largest extended character set specified among the supported locales; the null character shall have the code value zero. Each member of the basic character set shall have a code value equal to its value when used as the line character constant if an implementation does not define __STDC_MB_MIGHT_NEQ_WC__.

The macros are

```
NULL
```

expands to an implementation-null pointer constant; and

```
offsetof(type, member-designator)
```

expands to an integer constant expression that has type size_t, the value of which is the offset in bytes, to the structure member (designated by member-designator), from the beginning of its structure (designated by type). The type and member designator shall be that given

```
static type t;
```

then the expression &(t.member-designator) evaluates to an address constant. (If the specified member is a bit-field, the behavior is undefined.)

# Recommended practice

The types used for size_t and ptrdiff_t should not have an integer conversion greater than that of signed long unless the implementation supports objects large enough to make this necessary.