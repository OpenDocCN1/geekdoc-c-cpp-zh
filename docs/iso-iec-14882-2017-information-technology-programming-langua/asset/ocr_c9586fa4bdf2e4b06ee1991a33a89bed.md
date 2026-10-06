# ISO/IEC 14882:2017(E)

(2.4) frozen, set when the program has requested the array object not be altered, reallocated, or freed.

*Note: For the sake of exposition, the maintained data is presented here as:

+   3 (3.1) strstrate mode, the attributes of the array object associated with the strambuf object;
(3.2) int이자, the suggested minimum size for a dynamic array object;
(3.3) void (*palloc)(size_t), points to the function to allocate a dynamic array object;
(3.4) void (*pree)(void), points to the function to free a dynamic array object;

+   4 Each object of class strambuf has a seekable area, delimited by the pointers seeklow and seekhigh. If gnext is a null pointer, the seekable area is undefined. Otherwise, seeklow gbeg and seekhigh is either pend, if pend is not a null pointer, or gend.

D.6.1.1 strambuf constructors [depr.strambuf.com]

```
explicit strambuf(streamsize size_arg = 0);
```

Effects: Constructs an object of class strambuf, initializing the base class with strambuf(). The postconditions of this function are indicated in Table 142.

Table 142 — strambuf(streamsize) effects
| Element | Value |
|---|---|
| strmode | dynamic |
| alsize | alsize_arg |
| palloc | a null pointer |
| pfree | a null pointer |

```
strambuf(void* (*palloc)(size_t), void (*pree_arg)(void*));
```

Effects: Constructs an object of class strambuf, initializing the base class with strambuf(). The postconditions of this function are indicated in Table 143.

Table 143 — strambuf(+)(size_t), void (*)(void*)) effects
| Element | Value |
|---|---|
| strmode | dynamic |
| alsize | an unspecified value |
| palloc | palloc_arg |
| pfree | pfree_arg |

```
strambuf(char* gnext_arg, streamize n, char* pbeg_arg = nullptr);
strambuf(signed char* gnext_arg, streamize n, signed char* pbeg_arg = nullptr);
strambuf(unsigned char* gnext_arg, streamize n, unsigned char* pbeg_arg = nullptr);
```

3 Effects: Constructs an object of class strambuf, initializing the base class with strambuf(). The postconditions of this function are indicated in Table 144.

§ D.6.1.1 ©/IEC 2017 – All rights reserved(void) 1459