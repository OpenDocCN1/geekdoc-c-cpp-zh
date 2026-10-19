interpreted. (It also depends on what processor you’re using, so keep that in mind if you try to duplicate these results on your Desktop Cray.) The same raw memory contents can be interpreted as a string, an integer, a floating point, or anything else—it all depends on the base type of the pointer that points to the memory.

# General Tips on Pointers

With many types of defects, locating the error is the easiest part of dealing with the error and correcting it is the hard part. Pointer errors are different. A pointer error is usually the result of a pointer’s pointing somewhere it shouldn’t. When you assign a value to a bad pointer variable, you write data into an area of memory you shouldn’t. This is called “memory corruption.” Sometimes memory corruption produces horrible, fiery system crashes; sometimes it alters the results of a calculation in another part of the program; sometimes it causes your program to skip routines unpredictably; and sometimes it doesn’t do anything at all. In the last case, the pointer error is a ticking time bomb, waiting to ruin your program five minutes before you show it to your most important customer. Symptoms of pointer errors tend to be unrelated to causes of pointer errors. Thus, most of the work in correcting a pointer error is locating the cause.

Working with pointers successfully requires a two-pronged strategy. First, avoid installing pointer errors in the first place. Pointer errors are so difficult to find that extra preventive measures are justified. Second, detect pointer errors as soon after they are coded as possible. Symptoms of pointer errors are so erratic that extra measures to make the symptoms more predictable are justified. Here’s how to achieve these key goals:

![](bbox=[0.166, 0.438, 0.24, 0.5])

**Isolate pointer operations in routines or classes**  Suppose you use a linked list in several places in a program. Rather than traversing the list manually each place it’s used, write access routines such as `NextLink()`, `PreviousLink()`, `InsertLink()`, and `DeleteLink()`. By minimizing the number of places in which pointers are accessed, you minimize the possibility of making careless mistakes that spread throughout your program and take forever to find. Because the code is then relatively independent of data-implementation details, you also improve the chance that you can reuse it in other programs. Writing routines for pointer allocation is another way to centralize control over your data.

**Declare and define pointers at the same time**  Assigning a variable its initial value close to where it is declared is generally good programming practice, and it’s all the more valuable when working with pointers. Here is an example of what not to do:

![](bbox=[0.17, 0.827, 0.237, 0.89])

```
### C++ Example of Bad Pointer Initialization

Employee *employeePtr;
// lots of code
...
employeePtr = new Employee;
```