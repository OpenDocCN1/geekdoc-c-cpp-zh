```
Pushing elements onto intStack
1 2 3 4 5 6 7 8 9 10 11
Message: Stack is full, cannot push 11
    at Stack`1.Push(T pushValue) in C:\Users\PaulDeitel\Documents\
        examples\ch20\Fig20_09\Stack\Stack.cs:line 35
    at StackTest.TestPush[T](String name, Stack`1 stack, IEnumerable`1
        elements) in C:\Users\PaulDeitel\Documents\examples\ch20\Fig20_09\
        Stack\StackTest.cs:line 45

Popping elements from intStack
10 9 8 7 6 5 4 3 2 1
Message: Stack is empty, cannot pop
    at Stack`1.Pop() in C:\Users\PaulDeitel\Documents\
        examples\ch20\Fig20_09\Stack\Stack.cs:line 49
    at StackTest.TestPop[T](String name, Stack`1 stack) in
        C:\Users\PaulDeitel\Documents\examples\ch20\Fig20_09\Stack\
        Stack\StackTest.cs:line 68
```

**Fig. 18.9** | Testing generic class Stack. (Part 3 of 3.)

Method Main (Fig. 18.9, lines 17–30) creates the Stack<double> (line 19) and Stack<int> (line 20) objects. Lines 23–29 invoke generic methods TestPush and TestPop to test the Stack objects.

Generic method TestPush (lines 33–53) uses type parameter T (specified at line 33) to represent the data type stored in the Stack. The generic method takes three arguments—a string that represents the name of the Stack object for output purposes, an object of type Stack<T> and an IEnumerable<T> that contains the elements that will be pushed onto Stack<T>. The compiler enforces consistency between the type of the Stack and the elements that will be pushed onto the Stack when Push is invoked, which is the type argument of the generic method call. Generic method TestPop (lines 56–77) takes two arguments—a string that represents the name of the Stack object for output purposes and an object of type Stack<T>.

# 18.7 Wrap-Up

This chapter introduced generics. We discussed how generics ensure compile-time type safety by checking for type mismatches at compile time. You learned that the compiler will allow generic code to compile only if all operations performed on the type parameters in the generic code are supported for all types that could be used with the generic code. You also learned how to declare generic methods and classes using type parameters. We demonstrated how to use a type constraint to specify the requirements for a type parameter—a key component of compile-time type safety. We discussed several kinds of type constraints, including reference-type constraints, value-type constraints, class constraints, interface constraints and constructor constraints. We also discussed how to implement multiple type constraints for a type parameter. Finally, we showed how generics improve code reuse. In the chapter, we demonstrate the .NET Framework Class Library’s collection classes, interfaces and algorithms. Collection classes are pre-built data structures that you can reuse in your apps, saving you time.