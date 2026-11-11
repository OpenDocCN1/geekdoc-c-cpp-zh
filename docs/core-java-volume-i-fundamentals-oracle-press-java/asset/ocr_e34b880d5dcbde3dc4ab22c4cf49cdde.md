cannot know which of these choices applies. Therefore, the compiler cannot accept a call with an argument of type `Employee` or `Object`. After all, `T` might have been `Manager`. It is only possible to pass an object of type `Manager` or a subtype such as `Executive`.

Conversely, if you call `getFirst`, there is no guarantee about the type of the returned object. You can only assign it to an `Object`.

Here is a typical example. We have an array of managers and want to put the manager with the lowest and highest bonus into a `Pair` object. What kind of `Pair`? A `Pair<Employee>` should be fair game or, for that matter, a `Pair<Object>` (see Figure 8.4). The following method will accept any appropriate `Pair`:

```
```java
public static void minmaxBonus(Manager[] a, Pair<? super
Manager> result)
{
    if (a.length == 0) return;
    Manager min = a[0];
    Manager max = a[0];
    for (int i = 1; i < a.length; i++)
    {
        if (min.getBonus() > a[i].getBonus()) min = a[i];
        if (max.getBonus() < a[i].getBonus()) max = a[i];
    }
    result.setFirst(min);
    result.setSecond(max);
}
```
```

Intuitively speaking, wildcards with supertype bounds let you write to a generic object, while wildcards with subtype bounds let you read from a generic object.