
# Specifications 9

As the problem-solving process proceeds, you gradually refine the modules until eventually you implement their actions by writing code—typically, classes and their methods. Separating the purpose of a module from its implementation is known as functional(or procedural) abstraction. Once a module is written, you can use it without knowing the particulars of it as long as you have a statement of its purpose and a description of its arguments. Assuming the module is properly implemented, you can use it knowing only its specifications. You do not need to know its implementation.

Functional abstraction is essential to projects. After all, in a team, you have to use modules written by others, frequently without knowledge of their algorithms. Can you actually use a module without studying its code? In fact, you do this each time you use a C++ Standard Library function, such as sqrt in the C++ math library. Because sqrt is precompiled, you do not have access to its source statements. Furthermore, it may be that sqrt was written in a language other than C++. There is so much about that you do not know, yet you can use it in program without concern, as long as you know its specifications. If you pass a floating-point exception, it will return the floating-point square root of the value that expression. You can use sqrt even not knowing its implementation.

Consider a collection of data and a set of operations that include add new data to remove data from search for data. An abstraction function defines the operations on the collection of data, regardless of how you implement them. The other modules of the solution "what" operations they can perform, but they do not know how the operations are performed.

For example, you have used an array, but have you ever stopped to think about what an array actually is? There are many pictures of arrays throughout this book. They might resemble the way a C++ array is implemented on a computer, and they again might not. In either case, you can use an array without knowing what "looks like”—that is, how is implemented. Different systems implement arrays in different ways, the differences are transparent to the programmer.

For instance, regardless of how the array is implemented, you can always store the value 1492 in index of the array by using the statement

```cpp
years[index] = 1492;
```

and display the value by using the statement

```cpp
cout << years[index] << endl;
```

Thus, you can use an array without knowing the details of its implementation, just as you can use the function sqrt without knowing the details of its implementation. Let's explore this idea in more detail.

# 1.4 Information Hiding

As you have seen, abstraction tells you to write functional specifications for each module that describes its outside, or public, view. Abstraction also helps you identify details that you should hide from public view—details that should not be in the specifications but rather private. The principle of Information hiding tells you not only to hide such details within a module, but also to ensure that no other module can access these hidden details.

While writing a module's specifications, you must identify details that you can hide within the module. The principle of information hiding involves not hiding these details, but also making them inaccessible from a outside module. One way to understand information hiding is to imagine walls around the various tasks a program performs. These walls prevent the tasks from becoming entangled. The goal around each task prevents the isolation of the modules cannot be, however. The isolation cannot be total. Although MyProgram does not know how the task is performed, it must know what the task is and how to initiate it. For example, suppose your program needs to operate on a sorted array of names. The program may, for instance, search for a name or display the names in alphabetical order. The program needs a function that sorts an array of names. Although the rest of the program knows that sort can sort an array, it should not know how sort completes its task.

Thus, imagine a tiny slit in the wall, as Figure 1-2 illustrates. The slit is not large enough to allow the outside world to see the function's inner workings, but items can pass through the slit into out of the function. This slit is the prototype, declaration, or header of the function. The slit comprises the function or method, parameter list, and return type. For example, you can pass the array into the function sort, and the function can pass the sorted array out to you. What goes in and out is governed by the terms of the function's specifications, or contract: If you use the function in this way, this is exactly what it will do for you.

# FIGURE 1-2 Tasks communicate through a slit in the wall

![](img/d0cb86b2f18b2db569968ad7c743510e_36_0.png)

Suppose that a faster sort algorithm is developed. Since the function sort is isolated from the other modules in the program, the new algorithm can be implemented in the sort function without affecting those other modules. Thus, if MyProgram uses the task sort, and if the algorithm implementation for performing the sort changes, MyProgram will not be affected. As Figure 1-3 illustrates, the wall prevents MyProgram's algorithm from depending on sort's algorithm.

> Note: Information hiding hides the ways in which you need to deal with modules and data. As a user of a module, you do not worry about the details of its implementation. As an implementer of a module, you do not worry about its uses.

A module's interface is the only way to interact with that module.

# 1.3.5 Minimal and Complete Interfaces

The interface for a class is made up of the publicly accessible methods and data. Typically, a class interface contains only methods, as you will see, because publicly accessible data fields generally cause problems. The interface for a class describes the only programmers to interact with that class. Thus, interfaces are where collaboration between objects takes place. It is through its interface that a class is coupled to other classes. Designing good class interfaces is an important skill.

Each class should be easy to understand. Thus, when designing a class, you should keep the number of methods small. Your classes should provide programmers the power to do what they need to easily. These desires are at odds.

A complete interface for a class is one that will allow programmers to accomplish any reasonable task, the responsibilities of that class. A minimal interface for a class is one that contains a method if method is essential to that class's responsibilities. Programmers can more early learn how to interact with a class that has a minimal interface, as it has fewer methods to understand. Classes with minimal interfaces are also easier to maintain. Changes to a class can extend You should evaluate classes in terms of how complete and minimal their interfaces are. It is important that interfaces be complete. Somewhat less importance is having a minimal interface; sometimes a needless method is just too useful to omit.

FIGURE 1-3 A revised implementation communicates through the same slit in the wall

![](img/d0cb86b2f18b2db569968ad7c743510e_37_0.png)

# 1.4 Abstract Data Types

Often the solution to the problem requires operations on data. Such operations are broadly described in one of three ways:

- Add data to a collection.
- Remove data from a data collection.
- Ask questions about the data in a data collection.

Typical operations on data
