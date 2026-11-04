tasks, you typically determined *what* you wanted to accomplish in a task, then specified precisely *how* to accomplish it.

For example, let’s assume that *what* you’d like to accomplish is to sum the elements of an int array named `values` (the *data source*). You might use the following code:

```
```csharp
var sum = 0;

for (var counter = 0; counter < values.Length; ++counter)
{
    sum += values[counter];
}
```
```

This loop specifies precisely *how* to add each array element’s value to the sum—with a `for` iteration statement that processes each element one at a time, adding its value to the sum. This technique is known as external iteration—because you specify how to iterate, not the library—and requires you to access the elements sequentially from beginning to end in a single thread of execution. To perform the preceding task, you also create two variables (`sum` and `counter`) that are mutated repeatedly—their values change as the iteration is performed. You performed many similar array and collection tasks, such as displaying the elements of an array, determining the faces of a die that was rolled 60,000,000 times, calculating the average of an array’s elements and more.

# *External Iteration Is Error Prone*

The problem with external iteration is that even in this simple loop, there are many opportunities for error. You could, for example,

+   - initialize variable `sum` incorrectly,
+   - initialize control variable `counter` incorrectly,
+   - use the wrong loop-continuation condition,
+   - increment control variable `counter` incorrectly or
+   - incorrectly add each value in the array to the sum.

# *Internal Iteration*

In functional programming, you specify *what* you want to accomplish in a task, but not *how* to accomplish it. As you’ll see, to sum a numeric data source’s elements (such as those in an array or collection), you can use LINQ capabilities that allow you to say, “Here’s a data source, give me the sum of its elements.” You do *not* need to specify *how* to iterate through the elements or declare and use any mutable (that is, modifiable) variables. This is known as internal iteration, because the *library* code (behind the scenes) iterates through all the elements to perform the task.<sup>2</sup>

2. Systems developers have been familiar with the “what vs. how” distinction for decades. They begin a systems development effort by defining a requirements document that specifies what the system is supposed to do. Then, they use tools, such as the UML, to design the system, which specifies how the system should be built to meet the requirements. In the online chapters, we build the software for a very simple ATM. We begin with a requirements document that specifies what the software is supposed to do, then we use the UML to specify how the software should do it. We specify the final details of how by writing the actual C# code.