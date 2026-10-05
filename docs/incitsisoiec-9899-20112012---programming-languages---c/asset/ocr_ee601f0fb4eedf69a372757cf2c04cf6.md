# B.14 Alignment <stdalign.h>

alignas
__alignas_is_defined

# B.15 Variable arguments <stdarg.h>

va_list
type va_arg(va_list ap, type);
void va_copy(va_list dest, va_list src);
void va_end(va_list ap);
void va_start(va_list ap, parmN)

# B.16 Atoms <datomic.h>

```
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
```