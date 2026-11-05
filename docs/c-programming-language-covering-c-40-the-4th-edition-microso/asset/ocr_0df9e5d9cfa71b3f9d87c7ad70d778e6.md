# 7.15.3 Overload Resolution

Anonymous functions in an argument list participate in type inference and overload resolution. Please refer to §7.4.2.3 for the exact rules.

The following example illustrates the effect of anonymous functions on overload resolution.

```
class ItemList<T>: List<T>
{
    public int Sum(Func<T,int> selector) {
        int sum = 0;
        foreach (T item in this) sum += selector(item);
        return sum;
    }
    public double Sum(Func<T,double> selector) {
        double sum = 0;
        foreach (T item in this) sum += selector(item);
        return sum;
    }
}
```

The ItemList<T> class has two Sum methods. Each takes a selector argument, which extracts the value to sum over from a list item. The extracted value can be either an int or a double, and the resulting sum is likewise either an int or a double.

The Sum methods could, for example, be used to compute sums from a list of detail lines in an order.

```
class Detail
{
    public int UnitCount;
    public double UnitPrice;
    ...
}

void ComputeSums() {
    ItemList<Detail> orderDetails = GetOrderDetails(...);
    int totalUnits = orderDetails.Sum(d => d.UnitCount);
    double orderTotal = orderDetails.Sum(d => d.UnitPrice * d.UnitCount);
    ...
}
```

In the first invocation of orderDetails.Sum, both Sum methods are applicable because the anonymous function d => d.UnitCount is compatible with both Func<Detail,int> and Func<Detail,double>. However, overload resolution picks the first Sum method because the conversion to Func<Detail,int> is better than the conversion to Func<Detail,double>.

In the second invocation of orderDetails.Sum, only the second Sum method is applicable because the anonymous function d => d.UnitPrice * d.UnitCount produces a value of type double. Thus overload resolution picks the second Sum method for that invocation.