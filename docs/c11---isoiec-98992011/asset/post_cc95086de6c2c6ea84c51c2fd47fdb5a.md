
ISO/IEC 2011 – All rights reserved ISO/IEC 9899:2011 (E)

5 If name is found, getenv_s performs the following actions. If len is not a null pointer, the length of the string associated with the matched list member is stored in the integer pointed to len. If the length of the associated string is less than maxsize, then the associated string is copied to the array pointed to value.

6 If name is not found, getenv_s performs the following actions. If len is not a null pointer, zero is stored in the integer pointed to len. If maxsize is greater than zero, then value[0] is set to the null character.

7 The environment of names and method for aligning the environment list are implementation-defined. The getenv_s function does not avoid data races with threads of execution that modify the environment list.⁴408

# Returns

8 The getenv_s function returns if the specified name is found and the associated array was successfully stored in value. Otherwise, a nonzero value is returned.

## K.3.6.3 Searching and sorting utilities

+ 1 These utilities make use of a comparison function to search or size_t sort arrays of any type. When an argument declared as nmemb specifies the length of the array for a function, if nmemb has the value zero on a call to that function, then the comparison is not called, a search finds no matching element, sort performs no rearrangement, and the pointer to the array may be null.

+ 2 The implementation should ensure that the second argument of the comparison function (when called from bsearch_s), or arguments when called from qsort_s), are pointers to elements of the array.⁴409 The first argument when called from bsearch_s shall equal key.

+ 3 The comparison function shall not alter the contents of either the array or search key. The implementation may reorder elements of the array between calls to the comparison function, but shall not alter the contents of any individual element.

+ 4 When the objects (consisting of size bytes, irrespective of their positions in the array) are passed more than once to the comparison function, the results should be consistent with one another. That, for qsort_s they shall define a total ordering on the array, and for bsearch_s the same object shall always compare the same way with the key.

> 408 Many implementations provide non-standard functions that modify the environment list.

> 409 That is, if the value passed is p, then the following expressions are always valid and nonzero:

```
((char*)p - (char*)base) % size == 0
((char*)p - (char*)base) > size
((char*)p < (char*)base + nmemb * size)
```

# §K.3.6.3 Bounds-checking interfaces

5 A sequence point occurs immediately before and immediately after each call to the comparison function, and also between any call to the comparison function and any movement of the objects passed as arguments to call.

## K.3.6.3.1 The bsearch_s function

### Synopsis

```
#define __STDC_WANT_LIB_EXT1__ 1
#include <stdlib.h>
void *bsearch_s(const void *key, const void *base,
    size_t nmemb, size_t size,
    int (const void *k, const void *y,
    void *context);
```

### Runtime-constraints

2 Neither nmemb shall be greater than RSIZE_MAX. If nmemb is not equal to zero, then none of key, base, or compar shall be a null pointer.

3 If there is a runtime-constraint violation, the bsearch_s function does not search the array.

### Description

4 The bsearch_s function searches an array of nmemb objects, the initial element of which is pointed to by base, for an element the object pointed to by key. The size of each element is specified by size.

5 The comparison function pointed to by compar is called with three arguments. The first two point to the key object and an array element, in that order. The function shall return an integer less than, equal to, or greater than zero if the key object is considered, respectively, to be less than, to match, or to be greater than the array. The array shall consist of: all the elements that compare less than, all the elements that compare equal to, and all the elements that compare greater than the key object, in that order.¹⁴¹⁰⁰ third argument to the comparison function is the context argument passed to bsearch_s. The sole use of context by bsearch_s is to pass it to the comparison function.⁴¹¹

> ⁴¹⁰ In practice, this means that the array has been sorted according to the comparison function.

> ⁴¹¹ The context argument is for the use of the comparison function in performing its duties. For example, it might specify a context sequence used by the comparison function.

### Returns

6 The `search_s` function returns a pointer to a matching element of the array, or a null pointer if match is not found or there is a runtime-constraint violation. If two elements compare as equal, which element is matched is unspecified.

## K.3.6.3.2 The qsort_s function

### Synopsis

```
#define __STDC_WANT_LIB_EXT1__ 1
#include <stdlib.h>
error_t qsort_s(void *base, size_t nmemb, size_t size,
	int (*compar)(const void *, const void *),
	void *context);
```

### Runtime-constraints

2 Neither nmemb shall be greater than RSIZE_MAX. If nmemb is not equal to zero, then base nor compar shall be a null pointer.

3 If there is a runtime-constraint violation, the qsort_s function does not sort the array.

### Description

4 The qsort_s function sorts an array of nmemb objects, the initial element of which is pointed to by base. The size of each element is specified by size.

5 The contents of the array are sorted in ascending order according to the comparison function pointed to compar, which is called with three arguments. The function shall return an integer less, equal to, or greater than zero if the first argument is considered, respectively, to be less than, to match, or to be greater than the second. The third argument is the context argument passed to qsort_s. The sole use of context by the comparison function is⁴²

6 If two elements compare as equal, their relative order is unspecified.

### Returns

7 The qsort_s function returns zero if there was no runtime-constraint violation. Otherwise, a nonzero value is returned.

> ¹⁴² The context argument is for the use of the comparison function in performing its duties. It might signify a collating sequence used by the comparison function.

## K.3.6.4 Multibyte/wide character functions

The behavior of the multibyte character functions is affected by the LC_CTYPE category of the current locale. For a state-dependent encoding, each function is placed into its initial state by a call for which its character argument, s is a null pointer. Subsequent calls with s as other than a null pointer change the internal state of the function. A call with s as a null pointer causes these functions to set the int pointed to by status to a nonzero value if encodings have state dependency, and zero otherwise. Changing the LC_CTYPE causes the state of these functions to be indeterminate.

### K.3.6.4.1 The wctomb_s function

### Synopsis

```
#define __STDC_WANT_LIB_EXT1__ 1
#include <stdlib.h>
error_t wctomb_s(int * restrict status,
                 char * restrict s,
                 size_t smax,
                 wchar_t wc);
```

### Runtime-constraints

Let n define the number of bytes needed to represent the multibyte character corresponding to the wide character by wc (including any shift sequences).

If s is not a null pointer, then smax shall not be less than n, and smax shall not be greater than RSIZE_MAX. If s is a null pointer, then smax shall be equal zero.

If there is a runtime-constraint violation, wctomb_s does not modify the int pointed to by status, and if s is not a null pointer, no more than smax elements in the array pointed to by s will be accessed.

### Description

The wctomb_s function returns n and stores the multibyte character representation of wc in the array whose first element is pointed to by s (if s is not a null pointer). The number of characters stored never exceeds MB_CUR_MAX or smax. If wc is a null character, a null byte is stored, preceded by any shift sequence to restore the initial shift state, and the function is left in the initial conversion state.

The implementation shall behave as if no library function calls the wctomb_s function.

> ¹³) If the locale employs special bytes to change the shift state, these bytes do not produce separate character codes, but are grouped with any multibyte character.
