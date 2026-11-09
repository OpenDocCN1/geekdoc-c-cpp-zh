```
```java
// T:01:09 StackTest.java
public class StackTest {
    @Test
    public void canCreateStack() throws Exception {
        Stack stack = new Stack();
    }
}

// T: 01:09 Stack.java
package stack;

public class Stack {
}

// T: 01:24 StackTest.java
public class StackTest {
    @Test
    public void canCreateStack() throws Exception {
        Stack stack = new Stack();
        assertTrue(stack.isEmpty());
    }
}
```
```