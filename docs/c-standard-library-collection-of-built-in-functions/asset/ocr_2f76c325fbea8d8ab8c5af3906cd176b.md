```
Decimal Point = .
```

# Library Structure

```
```c
typedef struct {
    char *decimal_point;
    char *thousands_sep;
    char *grouping;
    char *int_curr_symbol;
    char *currency_symbol;
    char *mon_decimal_point;
    char *mon_thousands_sep;
    char *mon_grouping;
    char *positive_sign;
    char *negative_sign;
    char int_frac_digits;
    char frac_digits;
    char p_cs_precedes;
    char p_sep_by_space;
    char n_cs_precedes;
    char n_sep_by_space;
    char p_sign_posn;
    char n_sign_posn;
} lconv
```
```

Following is the description of each of the fields:

| S.N. | Field & Description |
|------|---------------------|
| 1 | **decimal_point**
Decimal point character used for non-monetary values. |
| 2 | **thousands_sep**
Thousands place separator character used for non-monetary values. |
| 3 | **grouping** |