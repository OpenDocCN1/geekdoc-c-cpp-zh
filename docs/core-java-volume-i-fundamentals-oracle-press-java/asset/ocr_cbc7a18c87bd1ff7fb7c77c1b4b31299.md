This tag adds an entry to the “parameters” section of the current method. The description can span multiple lines and can use HTML tags. All @param tags for one method must be kept together.

+   - @return *description*
+   
+     This tag adds a “returns” section to the current method. The description can span multiple lines and can use HTML tags.

+   - @throws *class description*
+   
+     This tag adds a note that this method may throw an exception. Exceptions are the topic of Chapter 7.

Here is an example of a method comment:

```
```java
/**
 * Raises the salary of an employee.
 * @param byPercent the percentage by which to raise the
salary (e.g., 10 means 10%)
 * @return  the amount of the raise
 */
public double raiseSalary(double byPercent)
{
    double raise = salary * byPercent / 100;
    salary += raise;
    return raise;
}
```
```

# ### 4.10.4 Field Comments

You only need to document public fields—generally that means static constants. For example:

```
```java
/**
 * The "Hearts" card suit
 */
public static final int HEARTS = 1;
```
```