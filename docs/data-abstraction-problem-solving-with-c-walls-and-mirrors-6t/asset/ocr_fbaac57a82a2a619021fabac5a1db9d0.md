determination to be made at execution time. That is, the outcome of a particular operation depends upon the object that performs the operation. For example, you can create a pointer to a clock object, myClock, in your program in such a way that it could reference either a clock object or an alarm clock. When myClock is asked to display the time, the compiler cannot determine whether it should use the clock implementation to display the time or the alarm clock implementation, since it does not know to which class of clocks the object referenced by myClock belongs. Polymorphism allows the compiler to simply note that the meaning of an operation is unknown until execution time.

+   **Note: Three principles of object-oriented programming**
+   
+   1. Encapsulation: Objects combine data and operations.
+   2. Inheritance: Classes can inherit properties from other classes.
+   3. Polymorphism: Objects can determine appropriate operations at execution time.

# 1.2 Achieving a Better Solution

The last program you wrote most likely solved the given problem correctly. However, was it the best possible solution? If you spent little—if any—time doing analysis and design, the solution probably left something to be desired. If you were to code the same program again, you would doubtless produce a better solution than your first attempt. However, if you spent some extra time analyzing the problem and designing a solution, you would probably get your best solution.

> Time devoted to analysis and design is time well spent

Suppose that you generated three correct but different solutions. Can you identify aspects of each solution that makes it better than the other solutions? What are these aspects? What should you focus on to create better solutions?

Creating a good set of modules for a moderate-sized problem is more art than science. It requires experience on the part of the programmer. A given problem likely has no “best” set of modules. Some sets of modules—and their interactions—might be better than others in light of certain measures. Moreover, for a sufficiently large problem, several different sets of modules could be considered “best,” depending upon the measure used. The “better” designs, however, do adhere to certain principles, which we examine next.

# 1.2.1 Cohesion

> A highly cohesive module performs one well-defined task.

Each module should perform one well-defined task; that is, it should be highly cohesive. A highly cohesive module brings several immediate benefits to a design or solution.

First, the module, if well named, promotes self-documenting, easy-to-understand code. For example, a highly cohesive function called sort should do nothing but sort. What this function does is clear from its name: If this function also prints the sorted values, it is not cohesive.

Second, a highly cohesive module is easy to reuse in other software projects. If a solution for another problem is being developed, the highly cohesive sort function can be used without change. If this function also prints the sorted values, it is much less likely to be the right sorting routine for the job.

Third, a highly cohesive module is much easier to maintain. Because the highly cohesive function does nothing but sort, fixing a logical error is simpler. If this function prints the sorted values, too, the printing code will complicate the function’s maintenance. A highly cohesive module has but one task that might need revision.

> A robust module performs well under unusual conditions

Fourth, a highly cohesive module is more robust; that is, it is less likely to be affected by change. The highly cohesive sort function will require change only if the system requires a different kind of sort. For example, you might need to sort data into descending, rather than ascending, order, or you might need a faster sort.