```
```c
{
    x = (PI/MAX)*angle;
    y = cos(x);
    printf("%15d %13.4f\n", angle, y);
    angle = angle + 10;
}
```
```

**Output**

| Angle | Cos(angle) |
|---|---|
| 0 | 1.0000 |
| 10 | 0.9848 |
| 20 | 0.9397 |
| 30 | 0.8660 |
| 40 | 0.7660 |
| 50 | 0.6428 |
| 60 | 0.5000 |
| 70 | 0.3420 |
| 80 | 0.1736 |
| 90 | -0.0000 |
| 100 | -0.1737 |
| 110 | -0.3420 |
| 120 | -0.5000 |
| 130 | -0.6428 |
| 140 | -0.7660 |
| 150 | -0.8660 |
| 160 | -0.9397 |
| 170 | -0.9848 |
| 180 | -1.0000 |

**Fig. 3.8**  *Program using a math function*

Another #include instruction that is often required is

```
```c
#include <stdio.h>
```
```

stdio.h refers to the *standard I/O* header file containing standard input and output functions

# ### 3.7.1  The #include Directive

As mentioned earlier, C programs are divided into modules or functions. Some functions are written by users, like us, and many others are stored in the C library. Library functions are grouped category-wise and stored in different files known as *header files*. If we want to access the functions stored in the library, it is necessary to tell the compiler about the files to be accessed.

This is achieved by using the preprocessor directive **#include** as follows:

```
```c
#include<filename>
```
```