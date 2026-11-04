```
```csharp
// Fig. 5.5: StudentTest.cs
// Create and test Student objects.
using System;

class StudentTest
{
    static void Main()
    {
        Student student1 = new Student("Jane Green", 93);
        Student student2 = new Student("John Blue", 72);

        Console.Write($"{student1.Name}'s letter grade equivalent of ");
        Console.WriteLine($"{student1.Average} is {student1.LetterGrade}");
        Console.Write($"{student2.Name}'s letter grade equivalent of ");
        Console.WriteLine($"{student2.Average} is {student2.LetterGrade}");
    }
}
```
```

```
```text
Jane Green's letter grade equivalent of 93 is A
John Blue's letter grade equivalent of 72 is C
```
```

Fig. 5.5 | Create and test Student objects.

# 5.6 while Iteration Statement

An iteration statement allows you to specify that a program should repeat an action while some condition remains *true*. Consider a code segment designed to find the first power of 3 larger than 100—when the following while iteration statement finishes executing, product contains the result:

```
```csharp
int product = 3;

while (product <= 100)
{
    product = 3 * product;
}
```
```

When this while statement begins execution, variable product contains the value 3. Each iteration of the while statement multiplies product by 3, so product takes on the values 9, 27, 81 and 243 successively. When product becomes 243, product <= 100 becomes false. This terminates the iteration, so the final value of product is 243. At this point, program execution continues with the next statement after the while statement.

![](bbox=[0.15, 0.82, 0.21, 0.88])

**Common Programming Error 5.1**
*Not providing in the body of a while statement an action that eventually causes the condition in the while to become false results in an infinite loop.*

# *while Iteration Statement Activity Diagram*

The UML activity diagram in Fig. 5.6 illustrates the flow of control in the preceding while statement. This diagram introduces the UML's merge symbol. The UML rep-