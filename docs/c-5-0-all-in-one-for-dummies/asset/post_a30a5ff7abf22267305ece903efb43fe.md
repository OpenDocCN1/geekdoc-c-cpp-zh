
- An initial input section in which the user inputs the principal, interest, and duration information
- A section mirroring the input data so that the user can verify the entry of the correct data
- A section that creates and outputs the table

Use this list to start looking for ways to refactor the program. In fact, if you further examine the input section of that program, you can see that the same basic code is used to input these amounts:

- Principal
- Interest
- Duration

Your observation gives you another good place to look. Alternatively, you can write empty methods for some of those comments and then fill them in one by one. That's programming by intention.

I used the techniques for planning a method to create the following version of the CalculateInterestTableWithMethods program:

![](img/80ff26f06fc9ab951e1cd4257b867366_251_0.png)

```
// CalculateInterestTableWithMethods -- Generate an interest table
// much like the other interest table programs, but this time using a
// reasonable division of labor among several methods.
// using System;
namespace CalculateInterestTableWithMethods
{
    public class Program
    {
        public static void Main(string[] args)
        {
            // Section 1 -- Input the data you need to create the table.
            decimal principal = 0M;
            decimal interest = 0M;
            decimal duration = 0M;
            InputInterestData(ref principal, ref interest, ref duration);
            // Section 2 -- Verify the data by mirroring it back to the user.
            Console.WriteLine();  // Skip a line.
            Console.WriteLine("Principal  = " + principal);
            Console.WriteLine("Interest   = " + interest + "%");
            Console.WriteLine("Duration   = " + duration + " years");
            Console.WriteLine();
            // Section 3 -- Finally, output the interest table.
            OutputInterestTable(principal, interest, duration);
            // Wait for user to acknowledge the results.
            Console.WriteLine("Press Enter to terminate...");
            Console.Read();
        }
        // InputInterestData -- Retrieve from the keyboard the
        // principal, interest, and duration information needed
        // to create the future value table. (Implements Section 1.)
        public static void InputInterestData(ref decimal principal,
ref decimal interest,
ref decimal duration)
{
    // 1a -- Retrieve the principal.
    principal = InputPositiveDecimal("principal");
    // 1b -- Now enter the interest rate.
    interest = InputPositiveDecimal("interest");
    // 1c -- Finally, the duration
    duration = InputPositiveDecimal("duration");
}
// InputPositiveDecimal -- Return a positive decimal number
//    from the keyboard.
public static decimal InputPositiveDecimal(string prompt)
{
    // Keep trying until the user gets it right.
    while(true)
    {
        // Prompt the user for input.
        Console.Write("Enter " + prompt + ":");
        // Retrieve the decimal value from the keyboard.
        string input = Console.ReadLine();
        decimal value = Convert.ToDecimal(input);
        // Exit the loop if the value that's entered is correct.
        if (value >= 0)
        {
            // Return the valid decimal value entered by the user.
            return value;
        }
        // Otherwise, generate an error on incorrect input.
        Console.WriteLine(prompt + " cannot be negative!");
        Console.WriteLine("Try again");
        Console.WriteLine();
    }
}
// OutputInterestTable -- Given the principal and interest,
//    generate a future value table for the number of periods
//    indicated in duration. (Implements Section 3.)
public static void OutputInterestTable(decimal principal,
    decimal interest,
    decimal duration)
{
    for (int year = 1; year <= duration; year++)
    {
        // Calculate the value of the principal plus interest.
        decimal interestPaid;
        interestPaid = principal * (interest / 100);
        // Now calculate the new principal by adding
        // the interest to the previous principal.
        principal = principal + interestPaid;
        // Round off the principal to the nearest cent.
        principal = decimal.Round(principal, 2);
        // Output the result.
        Console.WriteLine(year + " " + principal);
    }
}
```

I divided the Main() method into three clearly distinguishable parts, each marked with boldfaced comments. I further divided the first section into subsections labeled 1a, 1b, and 1c.

## Book II Chapter 3 We Have Our Methods

![](img/80ff26f06fc9ab951e1cd4257b867366_253_0.png)

Normally, you don't include the boldfaced comments. If you did, the listings would grow rather complicated because of all the numbers and letters. In practice, those types of comments aren't necessary if the methods are well thought out and their names clearly express the intent of each one.

Part 1 calls the method InputInterestData() to input the three variables the program needs in order to create the table: principal, interest, and duration. Part 2 displays these three values for verification just as earlier versions of the program do. Part 3 outputs the table via the method OutputInterestTable().

From the bottom and working upward, the OutputInterestTable() method contains an output loop with the interest rate calculations. This loop is the same one used in the inline, nonmethod CalculateInterestTable program. The advantage of this version, however, is that when writing this section of code, you don't need to concern yourself with any details of inputting or verifying data. When writing this method, think of it this way: "Given the three numbers — principal, interest, and duration — output an interest table," and that's it. After you're done, you can return to the line that called the OutputInterestTable() method and continue from there.

![](img/80ff26f06fc9ab951e1cd4257b867366_253_1.png)

OutputInterestTable() offers a target for trying the Visual Studio 2012 Refactor menu. Take these steps to give it a whirl:

1. Using the CalculateInterestTableMoreForgiving example from Book I, Chapter 5 as a starting point, select the code from the declaration of the year variable through the end of the while loop:
2. Choose Refactor→Extract Method.
3. In the Extract Method dialog box, type OutputInterestTable. Examine the Preview Method Signature box.

```
int year = 0;      // You grab the loop variable
while(year <= duration)  // and the entire while loop.
{
    //...
}
```

Notice that the proposed signature for the new method begins with the private static keywords and includes principal, interest, and duration in parentheses. (I introduce private, an alternative to public, in Book I. For now, you can make the method public after the refactoring, if you like.)

```
private static decimal OutputInterestTable(decimal principal,
decimal interest, int duration)
```

4. Click OK and then Apply to complete the Extract Method refactoring.

The code you selected in Step 1 is moved to a new method, located below Main() and named OutputInterestTable(). In the spot that it formerly occupied, you see this method call:

```
principal = OutputInterestTable(principal, interest, duration);
```

The Preview Changes window shows two panes so that you can preview exactly which information will change. The top pane shows the code as you're fixing as it looks now. The lower pane shows the code as it will look when it changes. For more sweeping refactorings, each pane may have numerous lines. You can select or deselect them individually to determine which specific elements to refactor.

![](img/80ff26f06fc9ab951e1cd4257b867366_254_0.png)

If, after refactoring, you suffer "buyer's remorse," click Undo or press Ctrl+Z.

Suppose that the previous refactoring did something you don't like, such as fail to include principal as a parameter. (Because this situation is possible, you must always check a refactoring to be certain that it's what you want.)

This situation happened the first time this section was written, in fact. (I'm writing this chapter based on beta software.) Rather than make principal a parameter, the Extract Method refactoring made it a local variable. To move principal into the parameter list, you can use the Promote Local Variable to Parameter refactoring. But before you do that, you need to initialize the local variable principal (the promotion refactoring doesn't work if the variable is uninitialized):

```
decimal principal = 0M; // M means decimal.
```

To carry out the Promote Local Variable to Parameter refactoring, you right-click the local principal variable's name and click Promote Local Variable to Parameter to move the local variable definition to the parameter list:

```
private static decimal OutputInterestTable(decimal interest,
int duration,
    decimal principal) ...
```

However, principal is at the end of the list and you want it at the beginning. You can use the Reorder Parameters refactoring to fix this problem.

To carry out Reorder Parameters, right-click the new principal parameter and click the Reorder Parameters link. In the dialog box, click the principal line to select it. Then click the ↑ button twice to move principal to the top of the list. Click OK.
