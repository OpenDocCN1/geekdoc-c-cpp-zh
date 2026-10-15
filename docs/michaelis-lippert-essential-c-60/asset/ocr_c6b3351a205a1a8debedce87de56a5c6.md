# Chapter 11: Generics

# OUTPUT 11.1

![](bbox=[0.139, 0.137, 0.652, 0.439])

Using the variable path, which is declared as a `System.Collections.Stack`, you save the previous move by passing a custom type, `Cell`, into the `Stack.Push()` method using `path.Push(currentPosition)`. If the user enters a Z (or presses Ctrl+Z), you undo the previous move by retrieving it from the stack using a `Pop()` method, setting the cursor position to be the previous position, and calling `Undo()`.

Although this code is functional, there is a fundamental shortcoming in the `System.Collections.Stack` class. As shown in Listing 11.1, the Stack class collects values of type object. Because every object in the CLR derives from object, Stack provides no validation that the elements you place into it are homogenous or are of the intended type. For example, instead of passing `currentPosition`, you can pass a string in which X and Y are concatenated with a decimal point between them. However, the compiler must allow the inconsistent data types because the stack class is written to take any object, regardless of its more specific type.

Furthermore, when retrieving the data from the stack using the `Pop()` method, you must cast the return value to a `Cell`. But if the type of the value returned from the `Pop()` method is not `Cell`, an exception is thrown. By deferring type checking until runtime by using a cast, you make the program more brittle. The fundamental problem with creating classes that