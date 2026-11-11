Let us put these functions to work and write a class that calls the C function sprintf. We would like to call the function as shown in Listing 12.8.

# **Listing 12.8** printf2/Printf2Test.java

```
```java
1  /**
2   * @version 1.10 1997-07-01
3   * @author Cay Horstmann
4   */
5  class Printf2Test
6  {
7     public static void main(String[] args)
8     {
9        double price = 44.95;
10       double tax = 7.75;
11       double amountDue = price * (1 + tax / 100);
12
13       String s = Printf2.sprintf("Amount due = $%.2f", amountDue);
14       System.out.println(s);
15    }
16 }
```
```

Listing 12.9 shows the class with the native sprintf method.

# **Listing 12.9** printf2/Printf2.java

```
```java
1  /**
2   * @version 1.10 1997-07-01
3   * @author Cay Horstmann
4   */
5  class Printf2
6  {
7     public static native String sprintf(String format, double x);
8
9     static
10    {
11       System.loadLibrary("Printf2");
12    }
13 }
```
```

Therefore, the C function that formats a floating-point number has the prototype

```
```c
JNIEXPORT jstring JNICALL Java_Printf2_sprintf(JNIEnv* env, jclass cl,
    jstring format, double x)
```
```

Listing 12.10 shows the code for the C implementation. Note the calls to GetStringUTFChars to read the format argument, NewStringUTF to generate the return