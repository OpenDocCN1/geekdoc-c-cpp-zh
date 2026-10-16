```
int* p1 = v2+2; // p1 = &v2[2]
int* p2 = v2-2; // *p2 undefined
}
```

Complicated pointer arithmetic is usually unnecessary and best avoided. Addition of pointers makes no sense and is not allowed.

Arrays are not self-describing because the number of elements of an array is not guaranteed to be stored with the array. This implies that to traverse an array that does not contain a terminator the way C-style strings do, we must somehow supply the number of elements. For example:

```
void fp(char v[], int size)
{
for (int i=0; i!=size; ++i)
use(v[i]); // hope that v has at least size elements
for (int x : v)
use(x); // error :range-for does not work for pointers

const int N = 7;
char v2[N];
for (int i=0; i!=N; ++i)

use(v2[i]);
for (int x : v2)
use(x); // range-for works for arrays of known size
```

This array concept is inherently low-level. Most advantages of the built-in array and few of the disadvantages can be obtained through the use of the standard-library container array (§8.2.4, §34.2.1). Some C++ implementations offer optional range checking for arrays. However, such checking can be quite expensive, so it is often used only as a development aid (rather than being included in production code). If you are not using range checking for individual accesses, try to maintain a consistent policy of accessing elements only in well-defined ranges. That is best done when arrays are manipulated through the interface of a higher-level container type, such as vector, where it is harder to get confused about the range of valid elements.

# 7.4.2 Multidimensional Arrays

Multidimensional arrays are represented as arrays of arrays; a 3-by-5 array is declared like this: int ma[3][5]; // 3 arrays with 5 ints each
We can initialize ma like this:

```
void init_ma()
{
for (int i = 0; i!=3; i++) for (int j = 0; j!=5; j++) ma[i][j] = 10*i+j; }
or graphically:
ma: 00 01 02 03 04 10 11 12 13 14 20 21 22 23 24
```

The array ma is simply 15 ints that we access as if it were 3 arrays of 5 ints. In particular, there is no single object in memory that is the matrix ma – only the elements are stored.