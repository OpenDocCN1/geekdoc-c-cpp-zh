because every class that implements the `Comparable` interface must supply the method.

![](bbox=[0.128, 0.177, 0.181, 0.219])

# **NOTE:**

You would expect that the sort method in the `Arrays` class is defined to accept a `Comparable[]` array so that the compiler can complain if anyone ever calls sort with an array whose element type doesn’t implement the `Comparable` interface. Sadly, that is not the case. Instead, the sort method accepts an `Object[]` array and uses a clumsy cast:

```
```java
// approach used in the standard library—not recommended
if (((Comparable) a[i]).compareTo(a[j]) > 0)
{
   // rearrange a[i] and a[j]
   . . .
}
```
```

If `a[i]` does not belong to a class that implements the `Comparable` interface, the virtual machine throws an exception.

[Listing 6.1] presents the full code for sorting an array of instances of the class `Employee` ([Listing 6.2]).

# **Listing 6.1** `interfaces/EmployeeSortTest.java`

```
```java
package interfaces;

import java.util.*;

/**
 * This program demonstrates the use of the Comparable
 * interface.
 * @version 1.30 2004-02-27
 * @author Cay Horstmann
```
```