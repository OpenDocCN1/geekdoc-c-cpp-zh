float complex cprojf(float complex z);
long double complex cprojl(long double complex z);
double creal(double complex z);
float crealf(float complex z);
long double creall(long double complex z);

# B.3 Character handling <ctype.h>

```
int isnalnum(int c);
int isalpha(int c);
int isblank(int c);
int iscntrl(int c);
int isdigit(int c);
int isgraph(int c);
int islower(int c);
int isprint(int c);
int ispunct(int c);
int isspace(int c);
int isupper(int c);
int isxdigit(int c);
int tolower(int c);
int toupper(int c);
```

# B.4 Errors <errno.h>

| EDOM | EISEQ | ERANGE | errno |
|| __STDC_WANT_LIB_EXT1__ | errno_t |

# B.5 Floating-point environment <fenv.h>

| fenv_t | FE_OVERFLOW | FE_TOWARDZERO |
fexcept_t | FE_UNDERFLOW | FE_UPWARD |
FE_DIVZERO | FE_ALL_EXCEPT | FE_DFL_ENV |
FE_INEXACT | FE_DOWNWARD |
FE_INVALID | FE_TONAREST |

```
#pragma STDC FENV_ACCESS on-switch
int fecleexcept(int excepts);
int fegetexceptflag(int fecept *flagp, int excepts);
int feraiseexcept(int excepts);
int fesetexceptflag(const fecept *flagp, int excepts);
int fetexcept(int excepts);
```