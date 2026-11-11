# Listing 12.17 *(Continued)*

```
```c
89  /* now call ps.print(str) */
90
91  /* get the class */
92  jclass class_PrintWriter = (*env)->GetObjectClass(env, out);
93
94  /* get the method ID */
95  jmethodID id_print = (*env)->GetMethodID(env, class_PrintWriter, "print", "(C)V");
96
97  /* call the method */
98  for (i = 0; str[i] != 0 && !(*env)->ExceptionOccurred(env); i++)
99      (*env)->CallVoidMethod(env, out, id_print, str[i]);
100
101  free(str);
102  }
```
```

# Listing 12.18 `printf4/Printf4.java`

```
```java
1  import java.io.*;
2
3  /**
4   * @version 1.10 1997-07-01
5   * @author Cay Horstmann
6   */
7  class Printf4
8  {
9      public static native void fprintf(PrintWriter ps, String format, double x);
10
11     static
12     {
13         System.loadLibrary("Printf4");
14     }
15 }
```
```

# Listing 12.19 `printf4/Printf4Test.java`

```
```java
1  import java.io.*;
2
3  /**
4   * @version 1.11 2018-05-01
5   * @author Cay Horstmann
6   */
7  class Printf4Test
8  {
9      public static void main(String[] args)
10     {
```
```