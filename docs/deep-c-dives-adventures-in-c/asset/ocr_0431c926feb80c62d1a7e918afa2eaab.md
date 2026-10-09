So, using precise types our previous program would be:

```
```
#include <stdio.h>
#include <stdlib.h>
#include <stdint.h>

int main(int argc, char **argv)
{
    int_8_t a = 1, b = 2;
    int_8_t c = a + b;
    printf("%d\n", c);
}
```
```

Notice the need for the additional header file.

To provide even more flexibility C99 introduces `int_least_n_t` which has at least *n* bits and `int_fastn_t` which is the fastest number of bits with at least *n* bits. Notice that in both cases you may get storage allocated with more bits than you specify and this alters when overflow occurs.

Notice that:

+   - `char` = `int_least_8_t`
- `short` = `int_least_16_t`
- `int` = `int_least_16_t`
- `long` = `int_least_32_t`
- `long long` = `int_least_64_t`

There are also two additional types that are occasionally useful:

+   - `int_max_t` the largest integer type available
- `intptr_t` gives enough bits to hold a pointer

The only use of `intptr_t` is if you need to cast a pointer to an integer to find out the address. In most cases you would be better off casting to `void*` unless you want to perform arithmetic or logical operations, i.e. integer operations on the address.

# ## Char Type

All languages have to provide some way of converting a bit pattern into something that can be printed or displayed and C is no exception. However, C is, as you might expect, a little more low-level than most. It sets aside the `char` type as the smallest collection of bits that can represent the characters that can be displayed on the machine's peripherals. This is conventionally just eight bits and in most cases we can regard a `char` as a byte. By today's standards this is hopelessly out-dated because of the now almost universal use of Unicode which needs 21 bits per character or code point. To store raw Unicode you would need a `char` to be 32-bits, but this never happens. There is a `wchar_t` type but this varies in size from 16-bits to 32-bits and makes no mention of what encoding UTF-16 or UTF-32 should be used. In practice it is better to avoid `wchar_t` if possible and use UTF-8 – see later.