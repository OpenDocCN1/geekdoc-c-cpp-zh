
# Solutions to Chapter 13 | C++

13.9 Write a smart pointer (smart_ptr) class.

# SOLUTION

Smart_ptr is the same as a normal pointer, but it provides safety via automatic memory. It avoids dangling pointers, memory leaks, allocation failures etc. The smart pointer must maintain a single reference count for all instances.

```cpp
template <class T> class SmartPointer {
public:
    SmartPointer(T * ptr) {
        ref = ptr;
        ref_count = (unsigned*)malloc(sizeof(unsigned));
        ref_count = 1;
    }
    SmartPointer(SmartPointer<T> sptr) {
        ref = sptr.ref;
        ref_count = sptr.ref_count;
        ++ref_count;
    }
    SmartPointer<T> &operator=(SmartPointer<T> &sptr) {
        if (this != &sptr) {
            ref = sptr.ref;
            ref_count = sptr.ref_count;
            ++ref_count;
        }
        return *this;
    }
    ~SmartPointer() {
        --ref_count;
        if (*ref_count == 0) {
            delete ref;
            free(ref_count);
        }
        ref = NULL;
        ref_count = NULL;
    }
    T getValue() { return *ref; }
protected:
    T * ref;
    unsigned *ref_count;
};
```

![](img/50974dc108b2978cf2cacf9397df9934_230_0.png)

14.1 In terms of inheritance, what is the effect of keeping a constructor private?

# SOLUTION

Declaring the constructor private will ensure that no one outside of the class can directly instantiate the class. In this case, the only way to create an instance of the class is by providing a static public method, as is done when using the Factory Method Pattern.

Additionally, because the constructor is private, the class also cannot be inherited.

# Solutions to Chapter 14 | Java

In Java, does the finally block get executed if we insert a return statement inside the try block of a try-catch-finally?

pg 78

# SOLUTION

Yes, it will get executed.

The finally block gets executed when the try block exists. However, even when we attempt to exit within the try block (normal exit, return, continue, break or any exception), the finally block will still be executed.

> Note: There are some cases in which the finally block will not get executed: if the virtual machine exits in between try-catch block execution, or the thread which is executing try/catch block gets killed.

# Solutions to Chapter 14 | Java

14.3 What is the difference between final, finally, and finalize?

# SOLUTIONS

### Final

- When applied to a variable (primitive): The value of the variable cannot change.
- When applied to a variable (reference): The reference variable cannot point to any other object on the heap.
- When applied to a method: The method cannot be overridden.
- When applied to a class: The class cannot be subclassed.

### Finally

There is an optional finally block after the try block or after the catch block. Statements in the finally block will always be executed (except if JVM exits from the try block). The finally block is used to write the cleanup code.

### Finalize

This is the method that the JVM runs before running the garbage collector.

# Solutions to Chapter 14 | Java

14.4 Explain the difference between templates in C++ and generics in Java. pg 78

# SOLUTION

| C++ Templates | Java Generics |
| :--- | :--- |
| Classes and functions can be templated. | Classes and methods can be generic. |
| Parameters can be any type or integral value. | Parameters can only be reference types (not primitive types). |
| Separate copies of the class or function are likely to be generated for each type parameter when compiled. | One version of the class or function is compiled, works for all type parameters. |
| Objects of a class with different type parameters are different types at run time. | Type parameters are erased when compiled; objects of a class with different parameters are the same type at run time. |
| Implementation source code of the template class or function must be included in order to use it (declaration insufficient). | Signature of the class or function from a compiled class file is sufficient to use it. |
| Templates can be specialized - a separate implementation could be provided for a particular template parameter. | Generics cannot be specialized. |
| Does not support wildcards. Instead, return types are often available as nested typedefs. | Supports wildcard as type parameter if it is only used once. |
| Does not directly support bounding of type parameters, but metaprogramming provides this. | Supports bounding of type parameters with "extends" and "super" for upper and lower bounds, respectively; allows enforcement of relationships between type parameters. |
| Allows instantiation of class of type parameter. | Does not allow instantiation of class of type parameter. |
| Type parameter of templated class can be used for static methods and variables. | Type parameter of templated class cannot be used for static methods and variables. |
| Static variables are not shared between classes of different type parameters. | Static variables are shared between instances of classes of different type parameters. |

From http://en.wikipedia.org/wiki/Comparison_of_Java_and_C%28%29BTemplates_vs. Generics

# Solutions to Chapter 14 | Java

14.5 Explain what reflection is in Java and why it is useful. pg 78

# SOLUTION

Reflection is a feature in Java that allows you to inspect and modify the runtime behavior of applications. It provides a way to:

- Get information about classes, methods, and fields at runtime.
- Create new instances of classes without knowing the exact type at compile time.
- Invoke methods and get/set fields dynamically.

```java
import java.lang.reflect.*;

public class Sample {
    public static void main(String[] args) {
        try {
            Class<?> c = Class.forName("Sample");
            Method[] m = c.getDeclaredMethods();
            for (Method method : m) {
                System.out.println(method);
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

Reflection is useful for:
1. Developing tools and IDEs that need to analyze other code.
2. Creating frameworks (like Spring or Hibernate) that use dependency injection or ORM.
3. Implementing unit testing frameworks that need to access private methods.

14.6 Suppose you are using a map in your program, how would you count the times it appears?

# SOLUTION

To count occurrences, you can iterate through the map and use a counter.

```java
import java.util.HashMap;
import java.util.Map;

public class Counter {
    public static void main(String[] args) {
        Map<String, Integer> map = new HashMap<>();
        map.put("apple", 1);
        map.put("banana", 2);
        map.put("apple", 3);

        Map<String, Integer> counts = new HashMap<>();
        for (String key : map.keySet()) {
            counts.put(key, counts.getOrDefault(key, 0) + 1);
        }
        System.out.println(counts);
    }
}
```

# Solutions to Chapter 15 | Databases

15.1 Write a query to find the number of employees in each department. pg 80

# SOLUTION

This problem uses a LEFT JOIN to ensure we include departments with 0 employees.

```sql
SELECT Departments.Dept_Name, COUNT(Employees.Employee_ID) AS num_employees
FROM Departments
LEFT JOIN Employees ON Departments.Dept_ID = Employees.Dept_ID
GROUP BY Departments.Dept_Name;
```

# Solutions to Chapter 15 | Databases

15.2 What are the different types of joins? Please explain how they differ and why certain types are better in certain situations. pg 80

# SOLUTION

JOIN is used to combine the results of two tables. To perform a join, each of the tables must have at least one field which will be used to find records from the other table. The join type defines which records will go into the result set.

- INNER JOIN: Returns records that have matching values in both tables.
- LEFT OUTER JOIN: Returns all records from the left table, and the matched records from the right table. If no match is found, NULL is returned for the right side.
- RIGHT OUTER JOIN: Returns all records from the right table, and the matched records from the left table.
- FULL OUTER JOIN: Returns all records when there is a match in either left or right table.

Situations:
- Use INNER JOIN when you only want data that exists in both tables.
- Use LEFT JOIN when you want all entries from the primary table, regardless of whether they have a related entry in the secondary table (e.g., finding all departments, even those without employees).
