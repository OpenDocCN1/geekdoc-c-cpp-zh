# 2. *Don’t use protected fields.*

Some programmers think it is a good idea to define most instance fields as `protected`, “just in case,” so that subclasses can access these fields if they need to. However, the protected mechanism doesn’t give much protection, for two reasons. First, the set of subclasses is unbounded—anyone can form a subclass of your classes and then write code that directly accesses protected instance fields, thereby breaking encapsulation. And second, in Java, all classes in the same package have access to protected fields, whether or not they are subclasses.

However, protected methods can be useful to indicate methods that are not ready for general use and should be redefined in subclasses.

# 3. *Use inheritance to model the “is-a” relationship.*

Inheritance is a handy code-saver, but sometimes people overuse it. For example, suppose we need a `Contractor` class. Contractors have names and hire dates, but they do not have salaries. Instead, they are paid by the hour, and they do not stay around long enough to get a raise. There is the temptation to form a subclass `Contractor` from `Employee` and add an `hourlyWage` field.

```
```java
public class Contractor extends Employee
{
    private double hourlyWage;
    . . .
}
```
```

This is not a good idea, however, because now each contractor object has both a salary and hourly wage field. It will cause you no end of grief when you implement methods for printing paychecks or tax forms. You will end up writing more code than you would have written by not inheriting in the first place.

The contractor-employee relationship fails the “is-a” test. A contractor is not a special case of an employee.

# 4. *Don’t use inheritance unless all inherited methods make sense.*

Suppose we want to write a `holiday` class. Surely every holiday is a day, and days can be expressed as instances of the `GregorianCalendar` class, so we can use inheritance.