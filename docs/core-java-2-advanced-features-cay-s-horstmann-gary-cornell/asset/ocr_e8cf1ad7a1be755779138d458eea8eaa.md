```
Listing 12.12  employee/Employee.java

```java
/**
 * @version 1.10 1999-11-13
 * @author Cay Horstmann
 */

public class Employee
{
   private String name;
   private double salary;

   public native void raiseSalary(double byPercent);

   public Employee(String n, double s)
   {
      name = n;
      salary = s;
   }

   public void print()
   {
      System.out.println(name + " " + salary);
   }

   static
   {
      System.loadLibrary("Employee");
   }
}
```
```

```
Listing 12.13  employee/Employee.c

```c
/**
 * @version 1.10 1999-11-13
 * @author Cay Horstmann
 */

#include "Employee.h"

#include <stdio.h>

JNIEXPORT void JNICALL Java_Employee_raiseSalary(JNIEnv* env, jobject this_obj, jdouble byPercent)
{
   /* get the class */
   jclass Class_Employee = (*env)->GetObjectClass(env, this_obj);
}
```
```

_(Continues)_