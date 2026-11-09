```
```java
    List<Integer> result = new ArrayList<>();
    result.addAll(sort(lessers));
    result.add(middle);
    result.addAll(sort(greaters));
    return result;
    }
```
```

It should come as no surprise that this passes and also passes the next two tests:

[Click here to view code image]()

```
```java
assertEquals(asList(1, 2, 3, 4), sort(asList(2, 1, 3, 4)));
assertEquals(asList(1, 2, 3, 4), sort(asList(4, 3, 2, 1)));
```
```

But now you may be wondering about that `middle`. What if the `middle` element was not unique in the list? Let’s try that:

[Click here to view code image]()

```
```java
assertEquals(asList(1, 1, 2, 3), sort(asList(1, 3, 1, 2)));
```
```

Yeah, that fails. That just means we should stop treating the `middle` as something special:

[Click here to view code image]()

```
```java
else {
    int middle = list.get(0);
    List<Integer> middles =
        list.stream().filter(x -> x == middle).collect(toList());
    List<Integer> lessers =
        list.stream().filter(x -> x<middle).collect(toList());
    List<Integer> greaters =
        list.stream().filter(x -> x>middle).collect(toList());


    List<Integer> result = new ArrayList<>();
    result.addAll(sort(lessers));
    result.addAll(middles);
    result.addAll(sort(greaters));
    return result;
}
```
```