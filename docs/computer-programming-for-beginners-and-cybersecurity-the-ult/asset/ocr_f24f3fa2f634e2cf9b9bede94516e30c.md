+   4. Converting a decimal number into a binary number etc.

# Stack ADT Operations

Push(k): Adds value k to the top of the stack

Pop(): Remove element from the top of the stack and return its value.

Top(): Returns the value of the element at the top of the stack

Size(): Returns the number of elements in the stack

IsEmpty(): determines whether the stack is empty. It returns true if the stack is empty otherwise return false.

Note: All the above stack operations are implemented in O(1) Time Complexity.

# Stack implementation in JAVA Collection

The stack is implemented by calling push and pop methods of Stack <T> class.

Example:

```
```java
public class StackDemo {

    public static void main(String[] args) {
        Stack<Integer> stack = new Stack<Integer>();
        int temp;
        stack.push(1);
        stack.push(2);
        stack.push(3);
        System.out.println("Stack : "+stack);
        System.out.println("Stack size : "+stack.size());
```
```