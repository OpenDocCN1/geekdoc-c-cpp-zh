```
```java
}
}
```
```

Right now, `getEmployees` can return `null`, but does it have to? If we change `getEmployee` so that it returns an empty list, we can clean up the code:

```
```java
List<Employee> employees = getEmployees();
for(Employee e : employees) {
    totalPay += e.getPay();
}
```
```

Fortunately, Java has `Collections.emptyList()`, and it returns a predefined immutable list that we can use for this purpose:

```
```java
public List<Employee> getEmployees() {
    if( .. there are no employees .. )
        return Collections.emptyList();
}
```
```

If you code this way, you will minimize the chance of `NullPointerExceptions` and your code will be cleaner.

# ## Don’t Pass Null

Returning `null` from methods is bad, but passing `null` into methods is worse. Unless you are working with an API which expects you to pass `null`, you should avoid passing `null` in your code whenever possible.

Let’s look at an example to see why. Here is a simple method which calculates a metric for two points:

```
```java
public class MetricsCalculator
{
    public double xProjection(Point p1, Point p2) {
        return (p2.x - p1.x) * 1.5;
    }
    …
}
```
```

What happens when someone passes `null` as an argument?

```
```java
calculator.xProjection(null, new Point(12, 13));
```
```