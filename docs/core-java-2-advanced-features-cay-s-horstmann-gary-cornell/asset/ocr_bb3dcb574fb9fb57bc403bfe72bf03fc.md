```
```java
14    PrintWriter out = new PrintWriter(System.out);
15    Printf3.fprintf(out, "Amount due = %8.2f\n", amountDue);
16    out.flush();
17  }
18 }
```
```

# **Listing 12.15** printf3/Printf3.java

```
```java
1  import java.io.*;
2
3  /**
4   * @version 1.10 1997-07-01
5   * @author Cay Horstmann
6   */
7  class Printf3
8  {
9     public static native void fprintf(PrintWriter out, String format, double x);
10
11    static
12    {
13       System.loadLibrary("Printf3");
14    }
15 }
```
```

# **Listing 12.16** printf3/Printf3.c

```
```c
1  /**
2   * @version 1.10 1997-07-01
3   * @author Cay Horstmann
4   */
5
6  #include "Printf3.h"
7  #include <string.h>
8  #include <stdlib.h>
9  #include <float.h>
10
11 /**
12    @param format a string containing a printf format specifier
13    (such as "%8.2f"). Substrings "%%" are skipped.
14    @return a pointer to the format specifier (skipping the '%')
15    or NULL if there wasn't a unique format specifier
16 */
17 char* find_format(const char format[])
18 {
19    char* p;
20    char* q;
21
```
```

*(Continues)*