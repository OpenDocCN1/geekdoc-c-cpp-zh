| Macro | Description |
|---|---|
| char p_sign_posn | Set to a value indicating the positioning of a positive_sign string; 0 means parentheses surround the quantity and currency symbol, 1 means the string precedes the quantity and currency symbol, 2 means the string follows the quantity and currency symbol, 3 means the string immediately precedes the currency symbol, and 4 means the string immediately follows the currency symbol. |
| char n_sign_posn | Set to a value indicating the positioning of a negative_sign string; the meaning is the same as for char p_sign_posn. |
| char int_p_cs_precedes | Set to 1 or 0 depending on whether int_currency_symbol precedes or follows the value of a non-negative formatted monetary quantity. |
| char int_p_sep_by_space | Set to 1 or 0 depending on whether int_currency_symbol is separated by a space from the value of a non-negative formatted monetary quantity. |
| char int_n_cs_precedes | Set to 1 or 0 depending on whether int_currency_symbol precedes or follows the value of a negative formatted monetary quantity. |
| char int_n_sep_by_space | Set to 1 or 0 depending on whether int_currency_symbol is separated by a space from the value of a negative formatted monetary quantity. |
| char int_p_sign_posn | Set to a value indicating the positioning of the positive_sign for a non-negative internationally formatted monetary quantity. |
| char int_n_sign_posn | Set to a value indicating the positioning of negative_sign for a negative internationally formatted monetary quantity. |

# Math Library: math.h

With C99, the math.h header file defines two types:

```
float_t
double_t
```

These types are at least as wide as float and double, respectively, and double_t is at least as wide as float_t. These are intended to be the most efficient types for doing float and double calculations, respectively.

This header file also defines several macros, as described in Table RS.V.15; all but HUGE_VAL are C99 additions. Some of these are discussed in more detail in Section VIII, “C99 Numeric Computational Enhancements.”