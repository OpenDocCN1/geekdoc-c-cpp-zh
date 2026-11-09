```
```java
else {
    int first = list.get(0);
    int middle = list.get(1);
    int last = list.get(2);
    List<Integer> lessers = new ArrayList<>();
    List<Integer> greaters = new ArrayList<>();

    if (first < middle)
        lessers.add(first);
    if (last < middle)
        lessers.add(last);
    if (first > middle)
        greaters.add(first);
    if (last > middle)
        greaters.add(last);

    List<Integer> result = new ArrayList<>();
    result.addAll(lessers);
    result.add(middle);
    result.addAll(greaters);
    return result;
}

assertEquals(asList(1, 2, 3), sort(asList(1, 3, 2)));
assertEquals(asList(1, 2, 3), sort(asList(3, 2, 1)));

assertEquals(asList(1, 2, 3, 4), sort(asList(1, 2, 3, 4)));

List<Integer> result = new ArrayList<>();
result.addAll(lessers);
result.add(middle);
result.addAll(sort(greaters));
return result;
```
```