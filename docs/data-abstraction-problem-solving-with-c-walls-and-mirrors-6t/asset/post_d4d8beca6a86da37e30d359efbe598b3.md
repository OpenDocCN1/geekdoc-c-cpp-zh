
## FIGURE 6-14 Adjacency list for the flight map in Figure 6-6 for Programming Problem 11

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_250_0.png)

- 13. Implement an expanded version of the HPAir problem. In addition to the “from” and “to” cities, each line of input contains a flight number (an integer) and the cost of the flight (an integer). Modify the HPAir program so that it will produce a complete itinerary for each request, including the flight number of each flight, the cost of each flight, and the total cost of the trip.

```
For example, the input files could appear as
cityFile: Albuquerque
Chicago
San Diego

flightFile: Chicago, San Diego 703 325
Chicago, Albuquerque 111 250
Albuquerque, Chicago 178 250

requestFile: Albuquerque, San Diego
Albuquerque, Paris
San Diego, Chicago
```

For this input, the program should produce the following output:

```
Request is to fly from Albuquerque to San Diego.
Flight #178 from Albuquerque to Chicago   Cost: $250
Flight #703 from Chicago to San Diego      Cost: $325
Total Cost ............ $575
Request is to fly from Albuquerque to Paris.
Sorry. HPAir does not serve Paris.
Request is to fly from San Diego to Chicago.
Sorry. HPAir does not fly from San Diego to Chicago.
```

When the nonrecursive isPath method finds a sequence of flights from the origin city to the destination city, its stack contains the corresponding path of cities. The stumbling block to reporting this path is that the cities appear in the stack in reverse order; that is, the destination city is at the top of the stack and the origin city is at the bottom. For example, if you use the program to find a path from city P to city Z in Figure 6-6, the final contents of the stack will be P-W-Y-Z with Z on top. You want to display the origin city P first, but it is at the bottom of the stack. If you restrict yourself to the stack operations, the only way you can write the path in its correct order is first to reverse the stack by popping it onto a temporary stack and then to write the cities as you pop them off the temporary stack. Note that this approach requires that you process each city on the path twice.

Evidently, a stack is not the appropriate ADT for the problem of writing the path of cities in the correct order; the appropriate ADT is a traversable stack. In addition to the standard stack operations isEmpty, push, pop, and peek, a traversable stack includes the operation traverse. The traverse operation begins at one end of the stack and visits each item in the stack until it reaches the other end of the stack. For this project, you want traverse to begin at the bottom of the stack and move toward the top.

- 14. What modifications to the previous programming problem are required to find a least-cost trip for each request? How can you incorporate time considerations into the problem?

This page intentionally left blank

## Exceptions

### Contents

- C3.1 Background 228
- C3.1.1 A Problem to Solve 228
- C3.2 Assertions 229
- C3.3 Throwing Exceptions 230
- C3.4 Handling Exceptions 233
- C3.4.1 Multiple catch Blocks 235
- C3.4.2 Uncaught Exceptions 236
- C3.5 Programmer-Defined Exception Classes 239

### Prerequisites

- C++ Interlude 1
- C++ Classes

Exceptions provide a mechanism in C++ and other programming languages for interrupting program execution when errors, unusual circumstances, or other events occur. An **exception** is an object that signals the rest of the program that something unexpected has happened. Our code can react appropriately to the exception based on its type and what the exception can tell us via its methods. We **handle** the exception when we detect and react to it.

Some exceptions indicate mistakes in your code. By correcting those mistakes, you avoid the exceptions and no longer have to worry about them. In fact, your final code gives no indication that an exception could occur. Furthermore, if your code is entirely correct, an exception will not occur. On the other hand, you can intentionally cause an exception. In fact, the programmers who wrote the code for the C++ Standard Library did so. At the very least, we need to know about exceptions so we can use the methods in the Standard Library.

What should we do when an exception occurs? Should we ever intentionally cause an exception in our own programs, and if so, how would we do so? These are some of the questions that this interlude will answer. This knowledge will be particularly important when we implement the ADT stack in the next chapter.

### C3.1 Background

It would be great if every time a method was called, its preconditions were met. As you have seen, that does not always happen. The client could ask a method to remove an item from a container, but the container might be empty. How do we deal with this unusual or exceptional condition? In our implementation so far, a method returns false to indicate that it is unable to perform its task. This value tells the client that some precondition was not met, or that the method has failed for some other reason. It is then the client’s responsibility to check the return value to ensure that the method completed its task before continuing.

Sometimes it is not possible for a method to return a boolean value when an unusual situation prevents it from completing its task. For example, the ADT stack’s method peek returns a copy of the top item on the stack. Its prototype is

```
virtual ItemType peek() const = 0;
```

What should this method do if the stack is empty? Returning a boolean value would be possible only if the stack contained boolean values, that is, if ItemType was of type bool. Regardless of the type of data in the stack, the return value will indicate a problem only if it is a special value not contained in the stack. We need a consistent mechanism to let the client know that the method could not perform its task—one that does not depend on the type of data stored in the stack. Before we get into the details of such mechanisms, let’s look at another example.

### C3.1.1 A Problem to Solve

Recall from the previous C++ Interludes the video game that we are working on for our friend. Our next task is to create a function that searches for a given string in a number of boxes. The function has three parameters: an array of PlainBox<string> objects, an integer that represents the number of PlainBox objects in the array, and the string to be located in each box. The function will return a copy of the box that contains the string. Listing C3-1 shows our first attempt at this function.

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_254_0.png)

This version of findBox meets the basic requirements: It searches the array of boxes and returns the box containing the target string. We encounter a problem if a box containing the target string is not in the array. If the target is not found, the function’s while loop ends when index is equal to size, which is the number of entries in the array. The function would then return boxes[size], which is undefined. Problems will occur when the client tries to use this “box.” We can repair our code by testing found to make sure we found the target before returning a box from the array. Using a simple if statement is insufficient, as we still would have the problem of what to return when the target is not found. The next section gives one way to fix our code.

### C3.2 Assertions

Chapter 3 and Appendix B define an assertion either as a statement of truth about some aspect of a program’s logic. You can express an assertion either as a comment or by using the C++ function assert. By using assert, you can make assertions about variables and objects in a program. Such assertions are in the form of a boolean expression that should be true at a specific point in the program. If the assertion is false, the assert function halts execution of the program. Assertions can be used to validate method preconditions before trying to execute the body of a function or method.

To use assert in a program, you first must include its header file:

```
#include <cassert>
```

To call the assert function, you provide a boolean condition as its argument:

```
assert(someBooleanCondition);
```

When program execution reaches this statement, the boolean condition—that is, the assertion—is tested. If the assertion is true, the program continues to execute normally. If the assertion is false, the program halts and an error message is displayed.

The assert statement is an easy way to verify a method’s preconditions or postconditions. For example, when implementing the stack method peek, we could execute

```
assert(!isEmpty());
```

before trying to return the top of the stack.

Our findBox function can test whether the box was found before returning boxes[index] by calling assert:

```
assert(found);
```

If the target is not found, the assertion is false and the program halts. This prevents the program from trying to use a box that does not exist. Listing C3-2 shows the revised findBox function using assertions.

### LISTING C3-2 Revised findBox function with assertions

```
PlainBox<string> findBox(PlainBox<string> boxes[], int size, string target)
{
 int index = 0;
 bool found = false;
 (continues)
```

Use an assert statement to test a precondition or postcondition
