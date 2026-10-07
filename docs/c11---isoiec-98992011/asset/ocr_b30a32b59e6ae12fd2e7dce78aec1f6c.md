© ISO/IEC 2011 – All rights reserved
ISO/IEC 9899:2011 (E)

```
errno_t strerror_s(char *s, rsize_t maxsize,
errno_t errno);
size_t strerror_s(errno_t errno);
size_t strnlen_s(const char *s, size_t maxsize);
```

# B.24 Type-generic math <math.h>

| acos sqrt nextafter |
| asin fabs frexp nexttoward |
| atan atan2 hypot remainder |
| acosh cbrt ilogb remquo |
| asinh ceil ldexp rint |
| atanh copysign l round |
| cos erf l1rint scalbn |
| sin erfc l1round scalbln |
| tan exp2 log10 tgamma |
| cosh explm log2 trunc |
| sinh fdim logb carg |
| tanh floor lrint cimag |
| exp fma lround conj |
| log fmax lround cproj |
| pow fmin nearby creal |

# B.25 Threads <threads.h>

| thread_local once_flag |
| ONCE_FLAG_INIT mtx_plain |
| TTS_DTOR_ITERATIONS mtx_recursive |
| cnd_t mtx_timed |
| thrd_t thrd_timed success |
| t_t thrd_busy |
| mtx_t thread error |
| ss_dtor_t mtx_nomem |
| thrd_start_t |

```
void call_once(once_flag *flag, void (*func)(void));
int cnd_broadcast(cnd_t *cond);
void cnd_destroy(cnd_t *cond);
int cnd_init(cnd_t *cond);
int cnd_signal(cnd_t *cond);
int cnd_timedwait(cnd_t *restrict cond,
mtx_t *restrict ts);
const struct timespec *restrict ts);
int cnd_wait(cnd_t *cond, mtx_t *mtx);
```

§B.25 Library summary 495