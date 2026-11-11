A minimal form of a queue interface might look like this:

```
```java
public interface Queue<E> // a simplified form of the interface
in the standard library
{
    void add(E element);
    E remove();
    int size();
}
```
```

The interface tells you nothing about how the queue is implemented. Of the two common implementations of a queue, one uses a "circular array" and one uses a linked list (see Figure 9.2).

![](bbox=[0.12, 0.54, 0.88, 0.92])