# CHAPTER 1 Data Abstraction: The Walls

determination to be made at execution time. That is, the outcome of a particular operation depends upon the object that performs the operation. For example, you can create a pointer to a clock object, myClock, in your program in such a way that it could reference either a clock object or an alarm clock. When myClock is called to display the time, the compiler cannot determine whether it should the clock implementation to display the time or the alarm clock implementation, since it does not know which class of clocks the object referenced by myClock belongs. Polymorphism allows the compiler to simply note that the meaning of an operation is unknown until execution time.

+   Note: Three principles of object-oriented programming
1. Encapsulation: Objects combine data and operations.
2. Inheritance: Classes can inherit properties from other classes.
3. Polymorphism: Objects can determine appropriate operations at execution time.

# 1.2 Achieving a Better Solution

The last program you wrote likely solved the given problem correctly. However, was it the best possible solution? If you spent little—any—time analysis and design, the solution probably left something to be improved. If you were to code the same program again, you would undoubtedly produce a better solution than your first attempt. If you spent some time analyzing the problem and designing a solution, you would probably get your best solution.

Suppose you generated three correct but different solutions. How could you identify of each solution makes it better than the others? What are the aspects? What would you focus on to create better solutions?

Creating a set of modules for a moderate-sized project is more art than science. It requires experience on part of the programmer. A given problem likely has no “best” set of modules. Some sets of modules and their interactions—might be better than others in light of certain measures. Moreover, for a sufficiently large project, several different sets of modules could be considered “best,” depending upon the pressure used. The “best” designs, however, do adhere to certain principles, which we must examine.

# 1.2.1 Cohesion

Each module should perform one well-defined task; that is, it should be cohesive. Highly cohesive modules provide immediate benefits to a design or solution.

First, the module well named, promotes self-documenting, easy-to-understand code. For example, a highly cohesive function sort does nothing but sort. What function does it clear from its name? If this function also needs to reuse the sorted values, it is not cohesive.

Second, a highly cohesive module is easy to use in other software projects. If another project is being developed, the highly cohesive sort function can be used without change. If this function also returns the sorted values, it is less likely to be the sorting routine for.

Third, a highly cohesive module is easier to maintain. The highly cohesive function does nothing but sort, fixing a logical error is simpler. If this function returns the sorted values, the testing code will complicate the function's maintenance. A highly cohesive module has one task that might need revision.

Fourth, a highly cohesive module is more robust; that is, it is less likely to be affected by change. The highly cohesive sort function will change only if the system requires a different kind of sort. If you might need to sort data into descending, rather than ascending, or you might need a faster sort.