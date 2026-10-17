
```c
double fmod(double x, double y);
float fmod(float x, float y);
long double fmod(long double x, long double y);
double remainder(double x, double y);
float remainder(float x, float y);
long double remainder(long double x, long double y);
double copysign(double x, double y);
float copysign(float x, float y);
long double copysign(long double x, long double y);
double nan(const char *ptr);
float nanf(const char *ptr);
long double nanl(const char *ptr);
double nextafter(double x, double y);
float nextafterf(float x, float y);
long double nextafterl(long double x, long double y);
double nextard(double x, double y);
float nextardf(float x, float y);
long double nextardl(long double x, long double y);
double fmax(double x, double y);
float fmaxf(float x, float y);
long double fmaxl(long double x, long double y);
double fmin(double x, double y);
float fminf(float x, float y);
long double fminl(long double x, long double y);
double fma(double x, double y, double z);
float fmaf(float x, float y, float z);
long double fmal(long double x, long double y, long double z);
```

## B.12 Nonlinear jumps `<setjmp.h>`
```c
jmp_buf
int setjmp(jmp_buf env);
long int longjmp(jmp_buf env, int val);
```

## B.13 Signal handling `<signal.h>`
```c
sig_atomic_t SIG_IGN SIGILL SIGTERM
SIG_DFL SIGABRT SIGINT
SIG_ERR FPE SIGSEGV
void (*signal(int sig, void (*func)(int)) (int);
int raise(int sig);
```

## B.14 Alignment `<stdalign.h>`
```c
alignas
__alignas_is_defined
```

## B.15 Variable arguments `<stdarg.h>`
```c
va_list
type va_arg(va_list ap, type);
void va_copy(va_list dest, va_list src);
void va_end(va_list ap);
void va_start(va_list ap, ...);
```

## B.16 Atoms `<stdatomic.h>`
```c
ATOMIC_BOOL_LOCK_FREE atomic_uint
ATOMIC_CHAR_LOCK_FREE atomic_long
ATOMIC_CHAR16_T_LOCK_FREE atomic_ulong
ATOMIC_CHAR32_T_LOCK_FREE atomic_llong
ATOMIC_WCHAR_T_LOCK_FREE atomic_ullong
ATOMIC_SHORT_LOCK_FREE atomic_char16_t
ATOMIC_INT_LOCK_FREE atomic_char32_t
ATOMIC_LONG_LOCK_FREE atomic_wchar_t
ATOMIC_LLONG_LOCK_FREE atomic_int8_t
ATOMIC_POINTER_LOCK_FREE atomic_uint8_t
ATOMIC_FLAG_INIT atomic_int16_t
memory_order atomic_int16_t
atomic_flag atomic_int32_t
memory_order_relaxed atomic_uint32_t
memory_order_consume atomic_int64_t
memory_order_acquire atomic_uint64_t
memory_order_release atomic_int8_t
memory_order_acq_rel atomic_uint8_t
memory_order_seq_cst atomic_int16_t
atomic_bool atomic_uint_fast16_t
atomic_char atomic_int_fast32_t
atomic_schar atomic_uint_fast32_t
atomic_uchar atomic_int_fast64_t
atomic_short atomic_uint_fast64_t
atomic_ushort atomic_intptr_t
atomic_int atomic_uintptr_t
atomic_size_t
atomic_intmax_t
atomic_ptrdiff_t
atomic_uintmax_t
```
```c
#define ATOMIC_VAR_INIT(value)
void atomic_init(volatile atomic *obj, type value);
type kill_dependency(type y);
void atomic_thread_fence(memory_order order);
void atomic_signal_fence(memory_order order);
_Bool atomic_is_lock_free(const volatile atomic *obj);
void atomic_store(volatile atomic *object, type desired);
void atomic_store_explicit(volatile atomic *object, type desired, memory_order order);
type atomic_load(volatile atomic *object);
type atomic_load_explicit(volatile atomic *object, memory_order order);
type atomic_exchange(volatile atomic *object, type desired);
type atomic_exchange_explicit(volatile atomic *object, type desired, memory_order order);
_Bool atomic_compare_exchange_strong(volatile atomic *object, type *expected, type desired);
_Bool atomic_compare_exchange_strong_explicit(volatile atomic *object, type *expected, type desired, memory_order order);
_Bool atomic_compare_exchange_weak(volatile atomic *object, type *expected, type desired);
_Bool atomic_compare_exchange_weak_explicit(volatile atomic *object, type *expected, type desired, memory_order order);
type atomic_fetch_add(volatile atomic *object, type arg);
type atomic_fetch_add_explicit(volatile atomic *object, type arg, memory_order order);
type atomic_fetch_sub(volatile atomic *object, type arg);
type atomic_fetch_sub_explicit(volatile atomic *object, type arg, memory_order order);
type atomic_fetch_and(volatile atomic *object, type arg);
type atomic_fetch_and_explicit(volatile atomic *object, type arg, memory_order order);
type atomic_fetch_or(volatile atomic *object, type arg);
type atomic_fetch_or_explicit(volatile atomic *object, type arg, memory_order order);
type atomic_fetch_xor(volatile atomic *object, type arg);
type atomic_fetch_xor_explicit(volatile atomic *object, type arg, memory_order order);
int atomic_wait(volatile atomic *object, type expected);
int atomic_wait_explicit(volatile atomic *object, type expected, memory_order order);
void atomic_notify(volatile atomic *object);
void atomic_notify_explicit(volatile atomic *object, memory_order order);
```

# B.20 输入/输出 `stdio.h`
```c
int remove(const char *filename);
int rename(const char *old, const char *new);
FILE *tmpfile(void);
char *tmpnam(char *s);
int fclose(FILE *stream);
int fflush(FILE *stream);
FILE *fopen(const char *restrict filename,
const char *restrict mode);
FILE *freopen(const char *restrict filename,
const char *restrict mode,
FILE *restrict stream);
void setbuf(FILE *restrict stream,
char * restrict buf);
int setvbuf(FILE *restrict stream,
char * restrict buf,
int mode, size_t size);
int fprintf(FILE * restrict stream,
const char *restrict format, ...);
int fscanf(FILE *restrict stream,
const char *restrict format, ...);
int vprintf(const char *restrict format, ...);
int scanf(const char *restrict format, ...);
int snprintf(char *restrict s, size_t n,
const char *restrict format, ...);
int sprintf(char *restrict s,
const char *restrict format, ...);
intcanf(char *restrict s,
const char *restrict format, ...);
int vprintf(FILE *restrict stream,
const char *restrict format, va_list arg);
int vsprintf(FILE *restrict stream,
const char *restrict format, va_list arg);
int vprintf(const char *restrict format, va_list arg);
int vscanf(const char *restrict format, va_list arg);
```
```c
int vsnprintf(char * restrict s, size_t n,
const char * restrict format, va_list arg);
int vsprintf(char *restrict s,
const char *restrict format, va_list arg);
int vscanf(const char *restrict s,
const char *restrict format, va_list arg);
int fgetc(FILE *stream);
char * fgets(char *restrict s, int n,
FILE *restrict stream);
int fputc(int c, FILE *stream);
int fputs(const char *restrict s,
FILE *restrict stream);
int getc(FILE *void);
int getc(int c, FILE *stream);
int putchar(int c);
int puts(const char *s);
int ungetc(int c, FILE *stream);
size_t fread(void *restrict ptr,
size_t size, size_t nmemb,
FILE *restrict stream);
size_t fwrite(const void *restrict ptr,
size_t size, size_t nmemb,
FILE *restrict stream);
int getpos(FILE *restrict pos,
fpos_t * restrict pos);
int fseek(FILE *stream, long int offset, int whence);
int fsetpos(FILE *stream, const fpos_t *pos);
long ftell(FILE *stream);
void rewind(FILE *stream);
void clearerr(FILE *stream);
int eof(FILE *stream);
int error(FILE *stream);
void perror(const char *s);
__STDC_WANT_EXT1__
size_t tmpnam_t TMP_MAX errno_t rsize_t
errno_t tmpfile_s(FILE *restrict *restrict streamptr);
errno_t tmpnam_s(char *s, size_t maxsize);
```
