This class could be instantiated with the following:

```
```java
MyClass<String> myString;
```
```

There are some drawbacks to these user-defined generic classes. For one
thing, they cannot store primitives. Second, the elements cannot be indexed.
Elements must be added to user-defined generic collections with the add
method. Next, we implement the generic stack example using an ArrayList.
Note that the last element of an ArrayList is found using the size method,
which returns the number of elements in the structure. Elements are deleted
from the structure with the remove method. Following is the generic class:

```
```java
import java.util.*;
public class Stack2<T> {

    private ArrayList<T> stackRef;
    private int maxLen;
    public Stack2() { // A constructor
        stackRef = new ArrayList<T> ();
        maxLen = 99;
    }
    public void push(T newValue) {
        if (stackRef.size() == maxLen)
            System.out.println("Error in push-stack is full");
        else
            stackRef.add(newValue);
    }
    public void pop() {
        if (empty())
            System.out.println("Error in pop-stack is empty");
        else
            stackRef.remove(stackRef.size() - 1);
    }
    public T top() {
        if (empty())
            System.out.println("Error in top-stack is empty");
            return null; }
        else
            return (stackRef.get(stackRef.size() - 1));
    }
    public boolean empty() {return (stackRef.isEmpty());}
}
```
```

This class could be instantiated for the String type with the following:

```
```java
Stack2<String> myStack =  new  Stack2<String>();
```
```

Recall from Chapter 9, that Java 5.0 supports wildcard classes. For example,
Collection<?> is a wildcard class for all collection classes. This allows
a method to be written that can accept any collection type as a parameter.
Because a collection can itself be generic, the Collection<?> class is in a sense
a generic of a generic class.