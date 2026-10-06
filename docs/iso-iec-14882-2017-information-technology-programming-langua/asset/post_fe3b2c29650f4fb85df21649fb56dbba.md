
# ISO/IEC 14882:2017(E)

GENERALIZED_NONCOMMUTATIVE_SUM(
  unary_op, init,
  unary_op*(first + 0), unary_op*(first + 1), ..., unary_op*(first + K - 1))

3 Returns: The end of the range beginning at result.

4 Complexity: O(last - first) applications of each unary_op and binary_op.

6 Remarks: result may be equal to first.
[Note: The difference between transform_exclusive_scan and transform_inclusive_scan is that transform_exclusive_scan excludes the ith element from the ith sum. If binary_op is not mathematically associative, the behavior of transform_inclusive_scan may be nondeterministic, transform_exclusive_scan does not apply unary_op to init. -- end note]

## 29.8.10 Transform inclusive scan [transform_inclusive_scan]

```cpp
template<class InputIterator, class OutputIterator, class BinaryOperation, class UnaryOperation>
OutputIterator transform_inclusive_scan(InputIterator first, InputIterator last,
OutputIterator result,
BinaryOperation binary_op,
UnaryOperation unary_op);
```

```cpp
template<class ExecutionPolicy,
class ForwardIterator1, class ForwardIterator2,
class BinaryOperation, class UnaryOperation>
ForwardIterator2 transform_inclusive_scan(ExecutionPolicy&& exec,
ForwardIterator1 first, ForwardIterator1 last,
ForwardIterator2 result,
BinaryOperation binary_op,
UnaryOperation unary_op);
```

```cpp
template<class InputIterator, class BinaryOperation, class UnaryOperation, class T>
OutputIterator transform_inclusive_scan(InputIterator first, InputIterator last,
OutputIterator result,
BinaryOperation binary_op,
UnaryOperation unary_op,
T init);
```

```cpp
template<class ExecutionPolicy,
class ForwardIterator1, class ForwardIterator2,
class BinaryOperation, class UnaryOperation, class T>
ForwardIterator2 transform_inclusive_scan(ExecutionPolicy&& exec,
ForwardIterator1 first, ForwardIterator1 last,
ForwardIterator2 result,
BinaryOperation binary_op,
UnaryOperation unary_op,
T init);
```

Requires:

- If init is provided, T shall be MoveConstructible (Table 23); otherwise, ForwardIterator1’s value type must be MoveConstructible.
- If init is provided, all of binary_op(init, init); binary_op(init, unary_op*(first)), and binary_op(unary_op*(first), unary_op*(first)) shall be convertible to T; otherwise, binary_op(unary_op*(first), unary_op*(first)) shall be convertible to ForwardIterator's value type.
- (1.3) Neither unary_op nor binary_op shall invalidate iterators or subranges, nor modify elements in the ranges [first, last] or [result, result + (last - first)].

2 Effects: for each integer K in [0, last - first) assigns through result + K of the value:

(2.1) GENERALIZED_NONCOMMUTATIVE_SUM(
  unary_op, init,
  unary_op*(first + 0), unary_op*(first + 1), ..., unary_op*(first + K))
  if init is provided,

(2.2) GENERALIZED_NONCOMMUTATIVE_SUM(
  binary_op,
  unary_op*(first + 0), unary_op*(first + 1), ..., unary_op*(first + K))

3 Returns: The result of the range ending between.

4 Complexity: O(last - first) applications of unary_op and binary_op.

5 Remarks: result may be equal to first.
6 [Note: The difference between transform_exclusive_scan and transform_inclusive_scan is that transform_inclusive_scan includes the Nth element in the Nth sum. If binary_op is not mathematically associative, the behavior of transform_inclusive_scan may be non-deterministic. transform_inclusive_scan does not apply unary_op to init. — note]

## 29.8.11 Adjacent [adjacent.difference]

```cpp
template<class InputIterator, class OutputIterator>
OutputIterator adjacent_difference(InputIterator first, InputIterator last, OutputIterator result);
template<class ExecutionPolicy, class ForwardIterator1, class ForwardIterator2>
ForwardIterator2 adjacent_difference(ExecutionPolicy&& exec, ForwardIterator1 first, ForwardIterator1 last, ForwardIterator2 result);
template<class InputIterator, class OutputIterator, class BinaryOperation>
OutputIterator adjacent_difference(InputIterator first, InputIterator last, OutputIterator result, BinaryOperation binary_op);
template<class ExecutionPolicy, class ForwardIterator1, class ForwardIterator2, class BinaryOperation>
ForwardIterator2 adjacent_difference(ExecutionPolicy&& exec, ForwardIterator1 first, ForwardIterator1 last, ForwardIterator2 result, BinaryOperation binary_op);
```

Requires:
- (1.1) For overloads with no ExecutionPolicy, Iterator's value type must be MoveAssignable (Table 25) and constructible from *first. The result of the expression *first - *first, is writable to the output iterator.
- (1.2) For overloads with ExecutionPolicy, the value type of ForwardIterator1 must be CopyConstructible (Table 24), constructible from the expression *first - *first, and assignable to the value type of ForwardIterator2.
- (1.3) For all overloads, the ranges [first, last] and [result, result + (last - first)] may not invalidate iterators or subranges.

Effects: For overloads with no ExecutionPolicy and a non-empty range, the function creates an accumulator value whose type is InputIterator's value, initializes it with *first, and assigns to *result. For every iterator in [first + 1, last), in order, creates an object value whose type is InputIterator's value type, initializes it with *(first + d), computes binary_op(*(first + d), *(first + d - 1)), and assigns to *(result + d).

Returns: result.
Complexity: O(last - first) applications of binary operation.
Remarks: for overloads with no ExecutionPolicy, result may be equal to first.

## 29.8.12 Iota [numeric.iota]

```cpp
template<class ForwardIterator, class T>
void iota(ForwardIterator first, ForwardIterator last, T value);
```

Requires: T must be convertible to ForwardIterator's value type. The expression ++val, where val has type T, must be well formed.

Effects: For each element i in the range [first, last), assigns *i = value and increments i by ++value.

Complexity: O(last - first) increments and assignments.

## 29.8.13 Greatest common divisor [numeric.gcd]

```cpp
template<class M, class N>
constexpr common_type_t<M, N> gcd(M m, N n);
```

Requires: |m| and |n| should be representable as a value of common_type_t<M, N>. [Note: These are valid if gcd(m, m) = |m| is representable as a value of type M. — end note]

Remarks: If either M or N is not an integer, or if either is a bool, the program is ill-formed.

Returns: Zero when m and n are both zero. Otherwise, returns the greatest common divisor of |m| and |n|.
Throws: Nothing.

## 29.8.14 Least common multiple [numeric.lcm]

```cpp
template<class M, class N>
constexpr common_type_t<M, N> lcm(M m, N n);
```

Requires: |m| and |n| should be representable as a value of common_type_t<M, N>. The least common multiple of |m| and |n| should be representable as a value of type common_type_t<M, N>.
(Note: The use of fully closed ranges is intentional.)

Remarks: If either m or N is not an integer type, or if either is bool, the program is ill-formed.

Returns: Zero when either m or n is zero. Otherwise, returns the least common multiple of |m| and |n|.
Throws: Nothing.

## 29.9 Mathematical functions for floating-point types

### 29.9.1 Header <cmath> synopsis

```cpp
namespace std {
    using float_t = see below;
    using double_t = see below;
}

#define HUGE_VAL see below
#define HUGE_VALF see below
#define HUGE_ALL see below
#define INFINITY see below
#define NAN see below
#define FP_INFINITE see below
#define FP_NAN see below
#define FP_NORMAL see below
#define FP_SUMNDN see below
#define FP_ZERO see below
#define FP_FAST_FMA see below
#define FP_FAST_PMF see below
#define FP_ILOGBO see below
#define FP_ILOGNAN see below
#define MATH_ERRNO see below
#define MATH_ERREXCEPT see below
```

```cpp
namespace std {
    float acos(float x); // see 20.2
    double acos(double x);
    long double acos(long double x); // see 20.2
    float acos(float x);
    long double acos(long double x);

    float asin(float x); // see 20.2
    double asin(double x);
    long double asin(long double x); // see 20.2
    float asin(float x);
    long double asin(long double x);

    float atan(float x); // see 20.2
    double atan(double x);
    long double atan(long double x); // see 20.2
    float atan(float x);
    long double atan(long double x);

    float atan2(float y, float x); // see 20.2
    double atan2(double y, double x);
    long double atan2(long double y, long double x); // see 20.2
}
```

#define math_errhandling see below
