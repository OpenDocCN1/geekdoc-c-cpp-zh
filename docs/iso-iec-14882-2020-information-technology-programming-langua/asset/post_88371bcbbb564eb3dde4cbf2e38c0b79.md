
3 The following class template specializations are required in addition to those specified in 28.4.2.5. The specialization codecvt<char16_t, char, mbstate_t> converts between the UTF-16 and UTF-8 encoding forms, and the specialization codecvt<char32_t, char, mbstate_t> converts between the UTF-32 and UTF-8 encoding forms.

## D.24 Deprecated filesystem path factory functions [depr.fs.path.factory]

```
template<class Source>
  path u8path(const Source& source);
template<class InputIterator>
  path u8path(InputIterator first, InputIterator last);
```

1 Requires: The source and [first, last) sequences are UTF-8 encoded. The value type of Source and InputIterator is char or char8_t. Source meets the requirements specified in 29.11.6.4.

2 Returns:

- (2.1) If value_type is char and the current native narrow encoding (29.11.6.3.2) is UTF-8, return path(source) or path(first, last); otherwise,
- (2.2) if value_type is wchar_t and the native wide encoding is UTF-16, or if value_type is char16_t or char32_t, convert source or [first, last) to a temporary, tmp, of type string_type and return path(tmp); otherwise,
- (2.3) convert source or [first, last) to a temporary, tmp, of type u32string and return path(tmp).

3 Remarks: Argument format conversion (29.11.6.3.1) applies to the arguments for these functions. How Unicode encoding conversions are performed is unspecified.

> [Example 1: A string is to be read from a database that is encoded in UTF-8, and used to create a directory using the native encoding for filenames:
> namespace fs = std::filesystem;
> std::string utf8_string = read_utf8_data();
> fs::create_directory(fs::u8path(utf8_string));
> For POSIX-based operating systems with the native narrow encoding set to UTF-8, no encoding or type conversion occurs.
> For POSIX-based operating systems with the native narrow encoding not set to UTF-8, a conversion to UTF-32 occurs, followed by a conversion to the current native narrow encoding. Some Unicode characters may have no native character set representation.
> For Windows-based operating systems a conversion from UTF-8 to UTF-16 occurs. — end example]

> [Note 1: The example above is representative of a historical use of filesystem::u8path. To indicate a UTF-8 encoding, passing a std::u8string to path's constructor is preferred as it is consistent with path's handling of other encodings. — end note]

## D.25 Deprecated atomic operations [depr.atomics]

### D.25.1 General [depr.atomics.general]

1 The header <atomic> (31.2) has the following additions.

```
namespace std {
  template<class T>
    void atomic_init(volatile atomic<T>*, typename atomic<T>::value_type) noexcept;
  template<class T>
    void atomic_init(atomic<T>*, typename atomic<T>::value_type) noexcept;
  #define ATOMIC_VAR_INIT(value) see below
  #define ATOMIC_FLAG_INIT see below
}
```

### D.25.2 Volatile access [depr.atomics.volatile]

1 If an atomic specialization has one of the following overloads, then that overload participates in overload resolution even if atomic<T>::is_always_lock_free is false:

```
void store(T desired, memory_order order = memory_order::seq_cst) volatile noexcept;
T operator=(T desired) volatile noexcept;
```

```
T load(memory_order order = memory_order::seq_cst) const volatile noexcept;
operator T() const volatile noexcept;
T exchange(T desired, memory_order order = memory_order::seq_cst) volatile noexcept;
bool compare_exchange_weak(T& expected, T desired,
    memory_order success, memory_order failure) volatile noexcept;
bool compare_exchange_strong(T& expected, T desired,
    memory_order success, memory_order failure) volatile noexcept;
bool compare_exchange_weak(T& expected, T desired,
    memory_order order = memory_order::seq_cst) volatile noexcept;
bool compare_exchange_strong(T& expected, T desired,
    memory_order order = memory_order::seq_cst) volatile noexcept;
T fetch_add(T operand, memory_order order = memory_order::seq_cst) volatile noexcept;
T operator op=(T operand) volatile noexcept;
T* fetch_add(ptrdiff_t operand, memory_order order = memory_order::seq_cst) volatile noexcept;
```

### D.25.3 Non-member functions [depr.atomics.nonmembers]

```
template<class T>
void atomic_init(volatile atomic<T>* object, typename atomic<T>::value_type desired) noexcept;
template<class T>
void atomic_init(atomic<T>* object, typename atomic<T>::value_type desired) noexcept;
```

Effects: Equivalent to: atomic_store_explicit(object, desired, memory_order::relaxed);

### D.25.4 Operations on atomic types [depr.atomics.types.operations]

```
#define ATOMIC_VAR_INIT(value) see below
```

The macro expands to a token sequence suitable for constant initialization of an atomic variable of static storage duration of a type that is initialization-compatible with value.

> [Note 1: This operation possibly needs to initialize locks. — end note]

Concurrent access to the variable being initialized, even via an atomic operation, constitutes a data race.

[Example 1:

```
atomic<int> v = ATOMIC_VAR_INIT(5);
```

— end example]

### D.25.5 Flag type and operations [depr.atomics.flag]

```
#define ATOMIC_FLAG_INIT see below
```

Remarks: The macro ATOMIC_FLAG_INIT is defined in such a way that it can be used to initialize an object of type atomic_flag to the clear state. The macro can be used in the form:

```
atomic_flag guard = ATOMIC_FLAG_INIT;
```

It is unspecified whether the macro can be used in other initialization contexts. For a complete static-duration object, that initialization shall be static.

## Bibliography

- — ISO 4217:2015, *Codes for the representation of currencies*
- — ISO/IEC 10967-1:2012, *Information technology — Language independent arithmetic — Part 1: Integer and floating point arithmetic*
- — ISO/IEC/IEEE 60559:2011, *Information technology — Microprocessor Systems — Floating-Point arithmetic*
- — The Unicode Consortium. Unicode Standard Annex, UAX #29, *Unicode Text Segmentation* [online]. Edited by Mark Davis. Revision 35; issued for Unicode 12.0.0. 2019-02-15 [viewed 2020-02-23]. Available from: `http://www.unicode.org/reports/tr29/tr29-35.html`
- — IANA Time Zone Database. Available from: `https://www.iana.org/time-zones`
- — Bjarne Stroustrup, *The C++ Programming Language, second edition*, Chapter R. Addison-Wesley Publishing Company, ISBN 0-201-53992-6, copyright ©1991 AT&T
- — Brian W. Kernighan and Dennis M. Ritchie, *The C Programming Language*, Appendix A. Prentice-Hall, 1978, ISBN 0-13-110163-3, copyright ©1978 AT&T
- — P.J. Plauger, *The Draft Standard C++ Library*. Prentice-Hall, ISBN 0-13-117003-1, copyright ©1995 P.J. Plauger)

The arithmetic specification described in ISO/IEC 10967-1:2012 is called *LIA-1* in this document.

## Cross references

Each clause and subclause label is listed below along with the corresponding clause or subclause number and page number, in alphabetical order by label.

accumulate (25.10.3)  1145
adjacent.difference (25.10.12)  1153
adjustfield.manip (29.5.6.2)  1394
alg.adjacent.find (25.6.8)  1092
alg.all.of (25.6.1)  1087
alg.any.of (25.6.2)  1087
alg.binary.search (25.8.4)  1121
alg.binary.search.general (25.8.4.1)  1121
alg.c.library (25.12)  1160
alg.clamp (25.8.10)  1139
alg.copy (25.7.1)  1099
alg.count (25.6.9)  1093
alg.equal (25.6.11)  1095
alg.fill (25.7.6)  1106
alg.find (25.6.5)  1089
alg.find.end (25.6.6)  1090
alg.find.first.of (25.6.7)  1091
alg.foreach (25.6.4)  1088
alg.generate (25.7.7)  1107
alg.heap.operations (25.8.8)  1132
alg.heap.operations.general (25.8.8.1)  1132
alg.is.permutation (25.6.12)  1096
alg.lex.comparison (25.8.11)  1139
alg.merge (25.8.6)  1126
alg.min.max (25.8.9)  1135
alg.modifying.operations (25.7)  1099
alg.move (25.7.2)  1101
alg.none.of (25.6.3)  1087
alg.nonmodifying (25.6)  1087
alg.nth.element (25.8.3)  1120
alg.partitions (25.8.5)  1123
alg.permutation.generators (25.8.13)  1141
alg.random.sample (25.7.12)  1113
alg.random.shuffle (25.7.13)  1114
alg.remove (25.7.8)  1108
alg.replace (25.7.5)  1104
alg.req (23.3.7)  946
alg.req.general (23.3.7.1)  946
alg.req.ind.cmp (23.3.7.5)  947
alg.req.ind.copy (23.3.7.3)  947
alg.req.ind.move (23.3.7.2)  946
alg.req.ind.swap (23.3.7.4)  947
alg.req.mergeable (23.3.7.7)  948
alg.req.permutable (23.3.7.6)  947
alg.req.sortable (23.3.7.8)  948
alg.reverse (25.7.10)  1111
alg.rotate (25.7.11)  1112
alg.search (25.6.13)  1097
alg.set.operations (25.8.7)  1127
alg.set.operations.general (25.8.7.1)  1127
alg.shift (25.7.14)  1115
alg.sort (25.8.2)  1116
alg.sorting (25.8)  1115
alg.sorting.general (25.8.1)  1115
alg.swap (25.7.3)  1102
alg.three.way (25.8.12)  1140
alg.transform (25.7.4)  1103
alg.unique (25.7.9)  1110
algorithm.stable (16.4.6.8)  502
algorithm.syn (25.4)  1049
algorithms (Clause 25)  1044
algorithms.general (25.1)  1044
algorithms.parallel (25.3)  1046
algorithms.parallel.defns (25.3.1)  1046
algorithms.parallel.exceptions (25.3.4)  1048
algorithms.parallel.exec (25.3.3)  1047
algorithms.parallel.overloads (25.3.5)  1049
algorithms.parallel.user (25.3.2)  1047
algorithms.requirements (25.2)  1044
algorithms.results (25.5)  1084
alloc.errors (17.6.4)  527
allocator.adaptor (20.13)  680
allocator.adaptor.cnstr (20.13.3)  682
allocator.adaptor.members (20.13.4)  683
allocator.adaptor.syn (20.13.1)  680
allocator.adaptor.types (20.13.2)  682
allocator.globals (20.10.10.3)  648
allocator.members (20.10.10.2)  647
allocator.requirements (16.4.4.6)  491
allocator.requirements.completeness (16.4.4.6.2)  496
allocator.requirements.general (16.4.4.6.1)  491
allocator.tag (20.10.7)  642
allocator.traits (20.10.9)  645
allocator.traits.general (20.10.9.1)  645
allocator.traits.members (20.10.9.3)  646
allocator.traits.types (20.10.9.2)  645
allocator.uses (20.10.8)  643
allocator.uses.construction (20.10.8.2)  643
allocator.uses.trait (20.10.8.1)  643
alt.headers (16.4.5.4)  499
any (20.8)  622
any.assign (20.8.4.3)  624
any.bad.any.cast (20.8.3)  622
any.class (20.8.4)  623
any.class.general (20.8.4.1)  623
any.cons (20.8.4.2)  623
any.general (20.8.1)  622
any.modifiers (20.8.4.4)  625
any.nonmembers (20.8.5)  626
