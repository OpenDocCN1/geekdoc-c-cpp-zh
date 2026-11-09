This passes. However, look up at that `else`. Remember what’s above it? Here, I’ll show you:

[Click here to view code image]

```
```java
if (list.size() <= 1)
    return list;
else if (list.size() == 2){
    int first = list.get(0);
    int second = list.get(1);
    if (first > second)
        return asList(second, first);
    else
        return asList(first, second);
}
```
```

Is that ==2 case really necessary anymore? No. Removing it still passes all tests.

Okay, so what about that first `if` statement? Is that still necessary? Actually, it can be changed to something better. And, in fact, let me just show you the final algorithm:

[Click here to view code image]

```
```java
private List<Integer> sort(List<Integer> list) {
    List<Integer> result = new ArrayList<>();

    if (list.size() == 0)
        return result;
    else {
        int middle = list.get(0);
        List<Integer> middles =
            list.stream().filter(x -> x == middle).collect(toList());
        List<Integer> lessers =
            list.stream().filter(x -> x < middle).collect(toList());
        List<Integer> greaters =
            list.stream().filter(x -> x > middle).collect(toList());

        result.addAll(sort(lessers));
        result.addAll(middles);
        result.addAll(sort(greaters));
        return result;
    }
}
```
```