part of a larger program would call this method, so the user interface shown in Figure 22-2 is purely for testing purposes. A real program would not allow the user to enter invalid values. Instead it might take the values from a database. In that case, the method's assertions protect it from invalid data in the database.

# ## Lesson Requirements

In this lesson, you:

+   - Build a program similar to the one shown in Figure 22-2.
+   - When the user clicks Calculate, make the program split the values entered in the `TextBox` apart, copy them into an array of `decimals`, pass them to the `AverageSalary` method, and display the result.
+   - Make the `AverageSalary` method validate its inputs by asserting that the array has a reasonable number of elements and that the salaries are reasonable. (Assume you're not working on Wall Street so salaries are at least $10,000 and less than $1 million.) Also validate the average.

> > **NOTE** You can download the code and resources for this lesson from the web-site at www.wrox.com/go/csharp24hourtrainer2e.

# ## Hints

+   - Think about how the program should react in a final release build for each of the input conditions.

For example, if the `values` array contains a salary of $1,600, what should the method do? In this case, that value is unusual but it could be valid (perhaps the company hired an intern for a week) so the method can calculate a meaningful (although unusual) result. The method should check this condition with `Debug.Assert` so it can calculate a result in the release version.

For another example, suppose the `values` array is empty. In this case the method cannot calculate a meaningful value so it should throw an exception to make the calling code deal with the problem.

# ## Step-by-Step

+   - Build a program similar to the one shown in Figure 22-2.
+     1. This is reasonably straightforward.
+   - When the user clicks Calculate, make the program split the values entered in the `TextBox` apart, copy them into an array of `decimals`, pass them to the `AverageSalary` method, and display the result.