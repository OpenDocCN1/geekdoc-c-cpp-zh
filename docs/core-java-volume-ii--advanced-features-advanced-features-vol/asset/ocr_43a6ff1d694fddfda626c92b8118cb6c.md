The CallNonvirtualXxxMethod functions receive an implicit argument, a method ID, a class object (which must correspond to a superclass of the implicit argument), and explicit arguments. The function calls the version of the method in the specified class, bypassing the normal dynamic dispatch mechanism.

All call functions have versions with suffixes “A” and “V” that receive the explicit parameters in an array or a va_list (as defined in the C header stdarg.h).

```
**Listing 12.14** `printf3/Printf3Test.java`

```java
import java.io.*;

/**
 * @version 1.11 2018-05-01
 * @author Cay Horstmann
 */
class Printf3Test
{
   public static void main(String[] args)
   {
      double price = 44.95;
      double tax = 7.75;
      double amountDue = price * (1 + tax / 100);
      var out = new PrintWriter(System.out);
      Printf3.printf(out, "Amount due = %.2f\\n", amountDue);
      out.flush();
   }
}
```
```

```
**Listing 12.15** `printf3/Printf3.java`

```java
import java.io.*;

/**
 * @version 1.10 1997-07-01
 * @author Cay Horstmann
 */
class Printf3
{
   public static native void fprintf(PrintWriter out, String format, double x);

   static
   {
      System.loadLibrary("printf3");
   }
}
```
```