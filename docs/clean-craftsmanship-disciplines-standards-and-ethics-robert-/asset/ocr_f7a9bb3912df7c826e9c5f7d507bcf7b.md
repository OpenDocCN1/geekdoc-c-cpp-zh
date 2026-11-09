```
```java
// T:01:09 StackTest.java
public class StackTest {
    @Test
    public void canCreateStack() throws Exception {
        Stack stack = new Stack();
    }
}
```
```

```
```java
// T: 01:09 Stack.java
package stack;

public class Stack {
}
```
```

Here we see another rule: red → green → refactor. Never miss an opportunity to clean things up.

> *Rule 2: Make it fail. Make it pass. Clean it up.*

Writing code that works is hard enough. Writing code that works and is clean is even harder. Fortunately, we can break the effort up into two steps. We can write bad code that works. Then, if we have tests, we can easily clean up the bad code while keeping it working.

Thus, every circuit around the TDD loop, we take the opportunity to clean up any little messes we might have made.

You may have noticed that our test does not actually assert any behavior. It compiles and passes but asserts nothing at all about the newly created stack. We can fix that in 15 seconds:

Click here to view code image

```
```java
// T: 01:24 StackTest.java
public class StackTest {
    @Test
    public void canCreateStack() throws Exception {
        Stack stack = new Stack();
        assertTrue (stack.isEmpty());
    }
}
```
```

The second law kicks in here, so we’d better get this to compile:

Click here to view code image