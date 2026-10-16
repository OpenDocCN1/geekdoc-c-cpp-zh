```
topIndex = -1;
}
public void push(int number) {
    if (topIndex == maxLen)
        System.out.println("Error in push-stack is full");
    else stackRef[++topIndex] = number;
}
public void pop() {
    if (empty())
        System.out.println("Error in pop-stack is empty");
    else --topIndex;
}
public int top() {
    if (empty()) {
        System.out.println("Error in top-stack is empty");
        return 9999;
    }
    else
        return (stackRef[topIndex]);
}
public boolean empty() {return (topIndex == -1);}
}
```

An example class that uses StackClass follows:

```
public class TstStack {
    public static void main(String[] args) {
        StackClass myStack = new StackClass();
        myStack.push(42);
        myStack.push(29);
        System.out.println("29 is: " + myStack.top());
        myStack.pop();
        System.out.println("42 is: " + myStack.top());
        myStack.pop();
        myStack.pop(); // Produces an error message
    }
}
```

One obvious difference is the lack of a destructor in the Java version, obviated by Java's implicit garbage collection.

# 11.4.3.2 Evaluation

Although different in some primarily cosmetic ways, Java's support for abstract data types is similar to that of C++. Java clearly provides for what is necessary to design abstract data types.

3. In Java, the finalize method serves as a kind of destructor.