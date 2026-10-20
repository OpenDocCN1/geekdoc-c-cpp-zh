```
Pushing elements onto doubleStack
1.1 2.2 3.3 4.4 5.5
Popping elements from doubleStack
5.5 4.4 3.3 2.2 1.1
EmptyStackException: Stack is empty, cannot pop
    at Stack.pop(Stack.java:32)
    at StackTest2.testPop(StackTest2.java:50)
    at StackTest2.main(StackTest2.java:17)

Pushing elements onto integerStack
1 2 3 4 5 6 7 8 9 10
Popping elements from integerStack
10 9 8 7 6 5 4 3 2 1
EmptyStackException: Stack is empty, cannot pop
    at Stack.pop(Stack.java:32)
    at StackTest2.testPop(StackTest2.java:50)
    at StackTest2.main(StackTest2.java:21
```

Fig. 21.10 | Passing generic Stack objects to generic methods. (Part 3 of 3.)

Lines 11–12 create the Stack<Double> and Stack<Integer> objects, respectively. Lines 15–16 and 19–20 invoke generic methods testPush and testPop to test the Stack objects. Because type parameters can represent only reference types, to be able to pass arrays doubleElements and integerElements to generic method testPush, the arrays declared in lines 7–8 must be declared with the wrapper types Double and Integer. When these arrays are initialized with primitive values, the compiler autoboxes each primitive value.

Generic method testPush (lines 24–35) uses type parameter T (specified at line 24) to represent the data type stored in the Stack<T>. The generic method takes three arguments—a String that represents the name of the Stack<T> object for output purposes, a reference to an object of type Stack<T> and an array of type T—the type of elements that will be pushed onto Stack<T>. The compiler enforces consistency between the type of the Stack and the elements that will be pushed onto the Stack when push is invoked, which is the real value of the generic method call. Generic method testPop (lines 38–58) takes two arguments—a String that represents the name of the Stack<T> object for output purposes and a reference to an object of type Stack<T>.

# 21.7 Raw Types

The test programs for generic class Stack in Section 21.6 instantiate Stacks with type arguments Double and Integer. It’s also possible to instantiate generic class Stack without specifying a type argument, as follows:

```
Stack objectStack = new Stack( 5 ); // no type-argument specified
```

In this case, the objectStack is said to have a raw type, which means that the compiler implicitly uses type Object throughout the generic class for each type argument. Thus the preceding statement creates a Stack that can store objects of any type. This is important for backward compatibility with prior versions of Java. For example, the data structures of the Java Collections Framework (see Chapter 20) all stored references to Objects, but are now implemented as generic types.