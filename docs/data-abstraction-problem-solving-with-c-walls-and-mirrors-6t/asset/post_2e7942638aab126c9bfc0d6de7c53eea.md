
Like many object-oriented principles, cohesion can be described in human terms. A person with low cohesion has “too many irons in the fire.” Such people tend to get bogged down in everything that they need to get done, and nothing they do gets done well. They could become more cohesive by delegating some of their responsibilities to others.

> Note: A guiding principle of OOD is that each class should have a single, well-defined responsibility. The methods of a class should be highly cohesive and related directly to supporting the responsibility of the class. The responsibilities of a class are functionally equivalent to the tasks that the class needs to perform. If a class has too many responsibilities, it should be split into multiple classes, each with a single responsibility taken from the original class.

## 1.2.2 Coupling

Coupling is a measure of the dependence among modules. This dependence, for example, could involve sharing data structures or calling each other’s methods. Ideally, the modules in a design should be independent of one another. However, some degree of coupling is necessary to get work done. That is, modules should be loosely coupled, and highly coupled modules should be avoided.

A loosely coupled module is independent

Loose coupling benefits a system in several ways. First, a module with loose coupling tends to create a system that is more adaptable to change. If class A depends on—that is, highly coupled to—class B and class B is changed, it is very likely that these changes will affect class A and break it.

Second, a module with loose coupling creates a system that is easier to understand. If class A depends on a class B, understanding how class A works requires an understanding of class B. Thus, class A is difficult to understand in isolation. A solution with a high degree of coupling can become nearly impossible to understand.

Third, a module with loose coupling increases the reusability of that module. If class A depends on class B, reusing class A in another program is complicated by the need to include class B in that program as well. Reusing coupled modules requires reusing all of the modules together as a unit. Often this is not desirable, or possible.

Fourth, a module with loose coupling has increased cohesion. Moreover, highly cohesive modules tend to be loosely coupled. As the level of cohesion associated with a module goes down, that module does more unrelated work, as we saw in the previous section. This has the side effect of causing the module to be coupled with many other modules from other areas in the program.

Again, realize that some coupling is required; coupling cannot and should not be eliminated from designs and solutions. To get work done, objects must collaborate. But collaboration requires objects to depend on one another. Tasks that an object has delegated to other objects create coupling between these objects. This coupling is necessary, but it should be kept to a minimum. However, other factors may influence a design. Thus, some designs with more coupling are better than other designs with less coupling because of these other factors.

> Note: If, in the past, you have spent little or no time on analysis and design for your programs, you must change this habit! The end result of OOD should be a modular solution that is easy to translate into the constructs of a particular programming language. By spending adequate time with analysis and design, you will spend less time writing and debugging your program.

## FIGURE 1-1 The task sort is a module separate from the MyProgram module

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_32_0.png)

## 1.3 Specifications

When you design a modular solution to a problem, each module simply states what it does but not how it does it. No one module may “know” how any other module performs its task—it may know only what that task is. For example, if one part of a solution is to sort some data, one of the modules may be a sorting algorithm, as Figure 1-1 illustrates. The other modules know that the sorting module sorts, but they do not know how it sorts. In this way, the various components of a solution are kept isolated from one another.

- Write specifications for each module before implementing it

Using this idea, you can write the modules in relative isolation from one another, knowing what each one will do but not necessarily how each will eventually do it. It is essential that a module’s specifications be written and understood.

## 1.3.1 Operation Contracts

- A module's contract specifies the module's purpose, assumptions, input, and output

An operation contract documents how a method can be used and what limitations it has. You should begin specifying this contract during analysis, finish the specification during design, and then document the contract in your code, particularly within the header files. In this way, programmers who use your code can understand what contract they need to honor for the method to generate correct results.

There is certain information you need to provide for each method. A method’s interface will specify how to call the method and the number, order, and types of arguments it expects—as already discussed. You also need to specify what should be true before the method is called and what will be true after the method finishes execution.

- Specify the data flow among modules

During design, it is also important that you clearly specify not only the purpose of each module, but also the data flow among modules. For example, you should provide answers to these questions for each module: What data is available to the module before its execution? What does the module assume? What actions have taken place, and what does the data look like, after the module executes? Thus, you should specify in detail the assumptions, input, and output for each module.

For example, if you as program designer needed to sort an array of integers, you might write the following specifications for a sort function:

```
The function will receive an array of num integers, where num > 0.
The function will return the array with the integers sorted.
```

You can view these specifications as the terms of a contract between your function and the module that calls it.

Specifications are the terms of a contract

This contract helps programmers understand what responsibilities the module will have to other modules in the solution. Whoever writes the sort function must live up to this contract. After the sort function has been written and tested, the contract tells the rest of the program how to call the sort function properly, as well as the result of doing so.

An operation contract should not describe how a module will perform its task

Notice, however, that a module's contract does not commit the module to a particular way of performing its task. If another part of the program assumes anything about the algorithm, it does so at its own risk. Thus, for example, if at some later date you rewrite your function to use a different sorting algorithm, you should not need to change the rest of the program at all. As long as the new function honors the terms of the original contract, the rest of the program should be oblivious to the change.

This should not be news to you. Although you might not have explicitly used the term contract before, the concept should be familiar. You write a contract when you write a function's precondition, which is a statement of the conditions that must exist at the beginning of a function, as well as when you write its postcondition, which is a statement of the conditions at the end of a function. For example, the sort function that adheres to the previous contract could appear in pseudocode as:

Operation contracts should include precise preconditions and postconditions

```
// Sorts an array;
// Precondition: anArray is an array of num integers; num > 0.
// Postcondition: The integers in anArray are sorted.
sort(anArray, num)
```

First-draft specifications

These particular pre- and postconditions actually are deficient, as can be the case in a first-draft contract. For example, does sorted mean ascending order or descending order? How large can num be? While implementing this function, you might assume that sorted means ascending order and that num will not exceed 100. Imagine the difficulties that can arise when another person tries to use sort to sort an array of 500 integers into descending order. This user will not know your assumptions unless you documented them by revising the contract as follows:

Revised specifications

```
// Sorts an array into ascending order.
// Precondition: anArray is an array of num integers and 1 <= num <= MAX_ARRAY,
// where MAX_ARRAY is a global constant that specifies the maximum size of anArray.
// Postcondition: anArray[0] <= anArray[1] <= ... <= anArray[num - 1];
// num is unchanged.
sort(anArray, num)
```

When you write a precondition, begin by describing the method or function's input arguments, mention any global named constants that it uses, and finally list any assumptions that it makes. When you write a postcondition, describe what changes the module has made. Note that in the case of a method or function that returns a value—which is technically a part of the postcondition—the value should be described.

Precise documentation is essential

Novice programmers tend to dismiss the importance of precise documentation, particularly when they are simultaneously designer, programmer, and user of a small program. If you design sort but do not write down the terms of the contract, will you remember them when you later implement the function? Will you remember how to sort weeks after you have written it? To refresh your memory, would you rather examine your program code or read a simple set of pre- and postconditions? As the size of a program increases, good documentation becomes even more important, regardless of whether you are sole author or part of a team.
