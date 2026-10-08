# 5.9 Formulating Algorithms: Counter-Controlled Iteration

```
// processing phase uses counter-controlled iteration
while (gradeCounter <= 10) // loop times
{
    Console.Write("Enter grade:"); // prompt
    int grade = int.Parse(Console.ReadLine()); // input grade
    total = total + grade; // add the grade to total
    gradeCounter = gradeCounter + 1; // increment the counter by 1
}
```

```
// termination phase
int average = total / 10; // integer division yields integer result
Console.WriteLine("$total of all 10 grades is {total}");
Console.WriteLine(\$$Class average is {average}");
```

```
Enter grade: 88
Enter grade: 79
Enter grade: 95
Enter grade: 100
Enter grade: 48
Enter grade: 88
Enter grade: 92
Enter grade: 83
Enter grade: 90
Enter grade: 85
```

Total of all 10 grades is 848
Class average is 84

> Fig. 5.9 Solving the class-average problem using counter-controlled iteration. (Part 2 of 2)

Local Variables in Main
Lines 10, 11, 17 and 23 declare local variables total, gradeCounter, grade and average, respectively. A variable declared in a method is a local variable and can be used from the line of its declaration to the closing right of the block in which the variable is declared. A local variable's declaration must appear before it is used; otherwise, a compilation error occurs. Variable grade—declared in the body of the while loop—can be used only in that block.

Initialization Phase: Initializing Variables total and gradeCounter
# requires local variables to be definitely assigned—that is, each local variable must be assigned a value before the variable's value is used. Lines 10-11 declare and initialize totalnto 0 and gradeCounter to 1 before their values are used, so these variables are definitely assigned (as grade and average in lines 17 and 23, respectively).

![](bbox=[0.145, 0.893, 0.215, 0.943])

Common Programming Error 5.3
All local variables must beので assigned before their values are used in expressions.
Using a local variable's value before it's definitely assigned results in a compilation error.