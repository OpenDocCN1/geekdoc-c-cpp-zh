
# ISO/IEC 14882:2020(E)

## 26.7.8.2 Assignment [mask.array.assign]

```
void operator=(const valarray<T>&) const;
const mask_array& operator=(const mask_array&) const;
```

These assignment operators have reference semantics, assigning the values of the argument array elements to selected elements of the valarray<T> object to which the mask_array object refers.

## 26.7.8.3 Compound assignment [mask.array.comp.assign]

```
void operator*= (const valarray<T>&) const;
void operator/= (const valarray<T>&) const;
void operator%= (const valarray<T>&) const;
void operator+= (const valarray<T>&) const;
void operator-= (const valarray<T>&) const;
void operator^= (const valarray<T>&) const;
void operator&= (const valarray<T>&) const;
void operator|= (const valarray<T>&) const;
void operator<<=(const valarray<T>&) const;
void operator>>=(const valarray<T>&) const;
```

These compound assignments have reference semantics, applying the indicated operation to the elements of the argument array and selected elements of the valarray<T> object to which the mask_array object refers.

## 26.7.8.4 Fill function [mask.array.fill]

```
void operator=(const T&) const;
```

This function has reference semantics, assigning the value of its argument to the elements of the valarray<T> object to which the mask_array object refers.

## 26.7.9 Class template indirect_array [template.indirect.array]

### 26.7.9.1 Overview [template.indirect.array.overview]

```
namespace std {
template<class T> class indirect_array {
public:
using value_type = T;

void operator= (const valarray<T>&) const;
void operator*= (const valarray<T>&) const;
void operator/= (const valarray<T>&) const;
void operator%= (const valarray<T>&) const;
void operator+= (const valarray<T>&) const;
void operator-= (const valarray<T>&) const;
void operator^= (const valarray<T>&) const;
void operator&= (const valarray<T>&) const;
void operator|= (const valarray<T>&) const;
void operator<<=(const valarray<T>&) const;
void operator>>=(const valarray<T>&) const;

indirect_array(const indirect_array&);
~indirect_array();
const indirect_array& operator=(const indirect_array&) const;
void operator=(const T&) const;

indirect_array() = delete; // as implied by declaring copy constructor above
};
}
```

This template is a helper template used by the indirect subscript operator

```
indirect_array<T> valarray<T>::operator[](const valarray<size_t>&).
```

It has reference semantics to a subset of an array specified by an indirect_array. Thus, the expression a[indirect] = b; has the effect of assigning the elements of b to the elements in a whose indices appear in indirect.

## 26.7.9.2 Assignment [indirect.array.assign]

```
void operator=(const valarray<T>&) const;
const indirect_array& operator=(const indirect_array&) const;
```

1 These assignment operators have reference semantics, assigning the values of the argument array elements to selected elements of the valarray<T> object to which it refers.

2 If the indirect_array specifies an element in the valarray<T> object to which it refers more than once, the behavior is undefined.

> [Example 1:
> int addr[] = {2, 3, 1, 4, 4};
> valarray<size_t> indirect(addr, 5);
> valarray<double> a(0., 10), b(1., 5);
> a[indirect] = b;
> results in undefined behavior since element 4 is specified twice in the indirection. — end example]

## 26.7.9.3 Compound assignment [indirect.array.comp.assign]

```
void operator*= (const valarray<T>&) const;
void operator/= (const valarray<T>&) const;
void operator%= (const valarray<T>&) const;
void operator+= (const valarray<T>&) const;
void operator-= (const valarray<T>&) const;
void operator^= (const valarray<T>&) const;
void operator&= (const valarray<T>&) const;
void operator|= (const valarray<T>&) const;
void operator<<=(const valarray<T>&) const;
void operator>>=(const valarray<T>&) const;
```

1 These compound assignments have reference semantics, applying the indicated operation to the elements of the argument array and selected elements of the valarray<T> object to which the indirect_array object refers.

2 If the indirect_array specifies an element in the valarray<T> object to which it refers more than once, the behavior is undefined.

## 26.7.9.4 Fill function [indirect.array.fill]

```
void operator=(const T&) const;
```

1 This function has reference semantics, assigning the value of its argument to the elements of the valarray<T> object to which the indirect_array object refers.

## 26.7.10 valarray range access [valarray.range]

1 In the begin and end function templates that follow, unspecified1 is a type that meets the requirements of a mutable Cpp17RandomAccessIterator (23.3.5.7) and models contiguous_iterator (23.3.4.14), whose value_type is the template parameter T and whose reference type is T&. unspecified2 is a type that meets the requirements of a constant Cpp17RandomAccessIterator and models contiguous_iterator, whose value_type is the template parameter T and whose reference type is const T&.

2 The iterators returned by begin and end for an array are guaranteed to be valid until the member function resize(size_t, T) (26.7.2.8) is called for that array or until the lifetime of that array ends, whichever happens first.

```
template<class T> unspecified1 begin(valarray<T>& v);
template<class T> unspecified2 begin(const valarray<T>& v);
```

3 Returns: An iterator referencing the first value in the array.

```
template<class T> unspecified1 end(valarray<T>& v);
template<class T> unspecified2 end(const valarray<T>& v);
```

4 Returns: An iterator referencing one past the last value in the array.

```
long double frexpl(long double value, int* exp);

int ilogb(float x);                 // see 16.2
int ilogb(double x);
int ilogb(long double x);          // see 16.2
int ilogbf(float x);
int ilogbl(long double x);

float ldexp(float x, int exp);      // see 16.2
double ldexp(double x, int exp);
long double ldexp(long double x, int exp);   // see 16.2
float ldexpf(float x, int exp);
long double ldexpl(long double x, int exp);

float log(float x);                 // see 16.2
double log(double x);
long double log(long double x);     // see 16.2
float logf(float x);
long double logl(long double x);

float log10(float x);               // see 16.2
double log10(double x);
long double log10(long double x);   // see 16.2
float log10f(float x);
long double log10l(long double x);

float log1p(float x);               // see 16.2
double log1p(double x);
long double log1p(long double x);   // see 16.2
float log1pf(float x);
long double log1pl(long double x);

float log2(float x);                // see 16.2
double log2(double x);
long double log2(long double x);    // see 16.2
float log2f(float x);
long double log2l(long double x);

float logb(float x);                // see 16.2
double logb(double x);
long double logb(long double x);    // see 16.2
float logbf(float x);
long double logbl(long double x);

float modf(float value, float* iptr); // see 16.2
double modf(double value, double* iptr);
long double modf(long double value, long double* iptr);   // see 16.2
float modff(float value, float* iptr);
long double modfl(long double value, long double* iptr);

float scalbn(float x, int n);       // see 16.2
double scalbn(double x, int n);
long double scalbn(long double x, int n);   // see 16.2
float scalbnf(float x, int n);
long double scalbnl(long double x, int n);

float scalbln(float x, long int n);  // see 16.2
double scalbln(double x, long int n);
long double scalbln(long double x, long int n);   // see 16.2
float scalblnf(float x, long int n);
long double scalblnl(long double x, long int n);

float cbrt(float x);                // see 16.2
double cbrt(double x);

long double cbrt(long double x);      // see 16.2
float cbrtf(float x);
long double cbrtl(long double x);

// 26.8.2, absolute values
int abs(int j);
long int abs(long int j);
long long int abs(long long int j);
float abs(float j);
double abs(double j);
long double abs(long double j);

float fabs(float x);      // see 16.2
double fabs(double x);
long double fabs(long double x);      // see 16.2
float fabsf(float x);
long double fabsl(long double x);

float hypot(float x, float y);      // see 16.2
double hypot(double x, double y);
long double hypot(long double x, long double y);  // see 16.2
float hypotf(float x, float y);
long double hypotl(long double x, long double y);

// 26.8.3, three-dimensional hypotenuse
float hypot(float x, float y, float z);
double hypot(double x, double y, double z);
long double hypot(long double x, long double y, long double z);

float pow(float x, float y);      // see 16.2
double pow(double x, double y);
long double pow(long double x, long double y);      // see 16.2
float powf(float x, float y);
long double powl(long double x, long double y);

float sqrt(float x);      // see 16.2
double sqrt(double x);
long double sqrt(long double x);      // see 16.2
float sqrtf(float x);
long double sqrtl(long double x);

float erf(float x);      // see 16.2
double erf(double x);
long double erf(long double x);      // see 16.2
float erff(float x);
long double erfl(long double x);

float erfc(float x);      // see 16.2
double erfc(double x);
long double erfc(long double x);      // see 16.2
float erfcf(float x);
long double erfcl(long double x);

float lgamma(float x);      // see 16.2
double lgamma(double x);
long double lgamma(long double x);      // see 16.2
float lgamm af(float x);
long double lgammal(long double x);

float tgamma(float x);      // see 16.2
double tgamma(double x);
long double tgamma(long double x);      // see 16.2
float tgammaf(float x);
long double tgammal(long double x);
```
