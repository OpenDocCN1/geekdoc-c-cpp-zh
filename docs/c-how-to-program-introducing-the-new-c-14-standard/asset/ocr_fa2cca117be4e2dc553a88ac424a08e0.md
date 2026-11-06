```
```cpp
7    cout << "__LINE__ = " << __LINE__ << endl;
8    cout << "__FILE__ = " << __FILE__ << endl;
9    cout << "__DATE__ = " << __DATE__ << endl;
10   cout << "__TIME__ = " << __TIME__ << endl;
11   cout << "__cplusplus = " << __cplusplus << endl;
12 }  // end main
```
```

```
```
__LINE__ = 9
__FILE__ = c:\\cpp4\\ch19\\ex19_02.CPP
__DATE__ = Jul 17 2002
__TIME__ = 09:55:58
__cplusplus = 199711L
```
```

# 3. E.3

+   A. `#define YES 1`
+   B. `#define NO 0`
+   C. `#include "common.h"`
+   D.

```
```cpp
#if defined(TRUE)
    #undef TRUE
    #define TRUE 1
#endif
```
```