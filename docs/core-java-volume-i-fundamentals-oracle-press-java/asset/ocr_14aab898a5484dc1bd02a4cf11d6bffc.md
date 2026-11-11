```
```java
class Holiday extends GregorianCalendar { ... }
```
```

Unfortunately, the set of holidays is not *closed* under the inherited operations. One of the public methods of `GregorianCalendar` is `add`. And `add` can turn holidays into nonholidays:

```
```java
Holiday christmas;
christmas.add(Calendar.DAY_OF_MONTH, 12);
```
```

Therefore, inheritance is not appropriate in this example.

Note that this problem does not arise if you extend an immutable class. Suppose you have an immutable date class, similar to `LocalDate` but not `final`. If you form a holiday subclass, there is no method that can turn a holiday into a nonholiday.

# 5. *Don’t change the expected behavior when you override a method.*

The substitution principle applies not just to syntax but, more importantly, to behavior. When you override a method, you should not unreasonably change its behavior. The compiler can’t help you—it cannot check whether your redefinitions make sense. For example, you can “fix” the issue of the `add` method in the `Holiday` class by redefining `add`, perhaps to do nothing, or to throw an exception, or to move on to the next holiday.

However, such a fix violates the substitution principle. The sequence of statements

```
```java
int d1 = x.get(Calendar.DAY_OF_MONTH);
x.add(Calendar.DAY_OF_MONTH, 1);
int d2 = x.get(Calendar.DAY_OF_MONTH);
System.out.println(d2 - d1);
```
```

should have the *expected behavior*, no matter whether `x` is of type `GregorianCalendar` or `Holiday`.

Of course, therein lies the rub. Reasonable and unreasonable people can argue at length about what the expected behavior is. For example, some authors argue that the substitution principle requires `Manager.equals` to ignore the bonus field because `Employee.equals` ignores it. These discussions are pointless if they occur in a vacuum. Ultimately, what