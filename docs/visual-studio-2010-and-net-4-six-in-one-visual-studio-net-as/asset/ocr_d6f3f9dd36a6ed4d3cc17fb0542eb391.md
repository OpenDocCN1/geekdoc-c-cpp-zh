# Flowcharts WF 4.0

Now, let's create a flowchart-based workflow that checks whether an integer number is a prime number. This is not a typical application of a workflow, this example can be helpful when learning about the Flowchart.

Create a new Workflow Console Application and name it PrimeWorkflow. Add a new code file to the project, name TestResult.cs, and define the enumerated type:

```
namespace PrimeWorkflow
{
    public enum TestResult
    {
        NotTested,
        Prime,
        NonPrime
    }
}
```

The algorithm will return NotTested if the input argument is greater than 1 billion. If it is less, Prime or NonPrime will be returned according the test. Build the project right now — it will be important in a future step.

The check is very simple. Let's try to divide the number by a few prime numbers (from 2 to 31). If the number can be divided by the prime number without a remainder, it cannot be a prime number. For demonstration purposes, the workflow will be extended to count the number of different primes that divide the argument, and it will display a few messages accounting this counter.

# Adding a Flowchart to the Workflow

Open the Workflow.xml file and draw a Flowchart activity (located in the Flowchart tab) to the design surface. This activity will display a simple Start state representing the entry point of this activity.
Add an Int32 argument to the workflow and name NumberToTest. Add an output argument, and name it Prime. Click the Argument column, and in the drop-down list, select "Browse for Types." A new dialog pops up. Expand the <Current project> node and its children until you find the TestResult node, then select and close it. If you did not build the project earlier, you would not be able to find the TestResult type.

The algorithm will use two variables. Add the dividersCount variable with a type of Int32, and another one, with the type of Int32[]. For the latter, select the "Array of T" from the Variable column, and then select Int32 from the dialog that pops up.

# Adding a Decision Activity

Drag a Decision activity to the Flowchart begin the Start point. Set its properties to the following values:

+   - Condition: NumberToTest > 1000000000
- FalseLabel: Testable
- TrueLabel: Too big to test