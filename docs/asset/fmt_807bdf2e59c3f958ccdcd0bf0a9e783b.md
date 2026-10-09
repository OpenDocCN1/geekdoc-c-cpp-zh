
`h-preprocessing-token`

`h-pp-tokens` `h-preprocessing-token`

`header-name-tokens`:
`string-literal`

`< h-pp-tokens >`

`has-include-expression`:
`__has_include ( header-name )`
`__has_include ( header-name-tokens )`

`has-embedded-expression`:
`__has_embedded ( header-name-embedded-parameter-sequence_opt )`
`__has_embedded ( header-name-tokens pp-balanced-token-sequence_opt )`

`has-c-attribute-expression`:
`__has_c_attribute ( pp-tokens )`

`va-opt-replacement`:
`__va_OPT_ ( pp_tokens )`

```
(6.10.8) on-switch-pragma:
# pragma STDC FP_CONTRACT on-off-switch
# pragma STDC FENV_ACCESS on-off-switch
# pragma STDC FENV_DEC_ROUND dec-direction
# pragma STDC FENV_ROUND direction
# pragma STDC CK_LIMITED_RANGE on-off-switch
```

`(6.10.8) on-switch`: 以下之一

`OFF` `DEFAULT`

`(6.10.8) direction`: 属于

`FE__DOWNWARD` `FE__TONAREST` `FE__TONEARESTFROMZERO`

`FE__TWARDZERO` `FE__UPWARD` `FE__DYNAMIC`

`(6.10.8) dec-direction`: 属于

`FE__DEC_DOWNWARD` `FE__DEC_TONAREST` `FE__DEC_TONEARESTFROMZERO`

`FE__DEC_TWARDZERO` `FE__DEC_UPWARD` `FE__DEC_DYNAMIC`

# A.5 浮数对象序列

`(7.2.6) n-char-sequence`:
`digit`
`nondigit`
`n-char-sequence`

# A.5.2 wchar_t 序列

`(7.3.2) n-char-sequence`:
`digit`
`nondigit`
`n-char-sequence`

# A.6 进制浮点序列

`(7.2.7) n-char-sequence`:
`digit`
`nondigit`
`n-char-sequence`

# A.6.2 wchar_t 序列

`(7.3.3) n-char-sequence`:
`digit`
`nondigit`
`n-char-sequence`

# 附录 B

信息性库摘要

# B.1 诊断 <assert.h>

```
__STDC_ASSERT_H NDEBUG
void assert(scalar expression);
```

# B.2 复数 <complex.h>

```
__STDC_NO_COMPLEX
__STDC_COMPLEX_H _Imaginary
complex _Complex_I
```

`#pragma STDC_CX_LIMITED_RANGE on-off-switch`

`double complex(double z);`

`float complex acos(float z);`

`long double complex acos(long double z);`

`double complex casin(double z);`

`float complex casin(float z);`

`long double complex casin(long double z);`

`double complex catan(double z);`

`float complex catan(float z);`

`long double complex catan(long double z);`

`double complex cos(double z);`

`float complex cos(float z);`

`long double complex cos(long double z);`

`double complex casin(double z);`

`float complex casin(float z);`

`long double complex casin(long double z);`

`double complex ctan(double z);`

`float complex ctan(float z);`

`long double complex ctan(long double z);`

`double complex acosh(double z);`

`float complex acosh(float z);`

`long double complex acosh(long double z);`

`double complex asinh(double z);`

`float complex asinh(float z);`

`long double complex asinh(long double z);`

`double complex cis(double z);`

`float complex cis(float z);`

`long double complex cis(long double z);`

`double complex sinh(double z);`

`float complex sinh(float z);`

`long double complex sinh(long double z);`

`double complex tanh(double z);`

`float complex tanh(float z);`

`long double complex tanh(long double z);`

`double complex cexp(double z);`

`float complex cexp(float z);`

`long double complex cexp(long double z);`
