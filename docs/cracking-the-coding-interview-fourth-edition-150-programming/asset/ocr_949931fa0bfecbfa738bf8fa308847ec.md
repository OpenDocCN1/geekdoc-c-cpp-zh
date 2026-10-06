# Solutions to Chapter 3 | Stacks and Queues

```
}
  public void push(int value){
    if (value <= min()) {
      s2.push(value);
    }
    super.push(value);
  }
  public Integer pop() {
    int value = super.pop();
    if (value == min()) {
      s2.pop();
    }
    return value;
  }
  public int min() {
    if (s2.isEmpty()) {
      return Integer.MAX_VALUE;
    } else {
      return s2.peek();
    }
  }
}
```

Why might this be more space efficient? If many elements have the same local min, we're keeping a lot of duplicate data. By having the mins kept in a separate stack, we don't have this duplicate data (although we do use up a lot of extra space because we have a stack instead of a single int).