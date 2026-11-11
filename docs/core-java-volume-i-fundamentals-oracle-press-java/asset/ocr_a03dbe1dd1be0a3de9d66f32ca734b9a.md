However, the method must return two numbers. We can achieve that by defining a class `Pair` that holds two values:

```
```java
class Pair
{
    private double first;
    private double second;
    public Pair(double f, double s)
    {
        first = f;
        second = s;
    }
    public double getFirst() { return first; }
    public double getSecond() { return second; }
}
```
```

The minmax method can then return an object of type `Pair`.

```
```java
class ArrayAlg
{
    public static Pair minmax(double[] values)
    {
        . . .
        return new Pair(min, max);
    }
}
```
```

The caller of the method uses the `getFirst` and `getSecond` methods to retrieve the answers:

```
```java
Pair p = ArrayAlg.minmax(d);
System.out.println("min = " + p.getFirst());
System.out.println("max = " + p.getSecond());
```
```

Of course, the name Pair is an exceedingly common name, and in a large project, it is quite possible that some other programmer had the same bright idea—but made a Pair class that contains a pair of strings. We can solve this