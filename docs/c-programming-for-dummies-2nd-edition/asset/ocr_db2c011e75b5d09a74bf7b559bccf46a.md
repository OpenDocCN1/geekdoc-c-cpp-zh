```
```
%6.1f = 34.5
%5.1f = 34.5
%4.1f = 34.5
%3.1f = 34.5
%2.1f = 34.5
%1.1f = 34.5
%9.1f = 12.3
%9.2f = 12.35
%9.3f = 12.346
%9.4f = 12.3457
%9.5f = 12.34568
%9.6f = 12.345679
%9.7f = 12.3456793
%9.8f = 12.34567928
```
```

From this output, you can see how the width value “pads” the numbers on the left. As the width value decreases, so does the padding. However, when the width specified is wider than the original value, nonsense is displayed, as shown by the last two lines of output. This is because the width is beyond the limit of single precision.

# Setting the output width

The w output width option is available to all the conversion characters, not just %f. The width is the minimum amount of space provided for output. When the output is less than the width, it’s right-justified. When the output is greater than the width, the width value is ignored. Listing 13-6 provides examples using the %s placeholder.

# LISTING 13-6: Messing with the Width

```
```c
#include <stdio.h>

int main()
{
    printf("%15s = %15s\n","hello");
    printf("%14s = %14s\n","hello");
    printf("%13s = %13s\n","hello");
    printf("%12s = %12s\n","hello");
    printf("%11s = %11s\n","hello");
    printf("%10s = %10s\n","hello");
    printf(" %9s = %9s\n","hello");
    printf("  %8s = %8s\n","hello");
}
```
```