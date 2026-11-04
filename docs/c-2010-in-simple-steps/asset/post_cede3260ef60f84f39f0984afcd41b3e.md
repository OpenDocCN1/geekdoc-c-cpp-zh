
```csharp
{
    class Program
    {
        static void Main(string[] args)
        {
            string Name;
            int Marks;
            Console.Write("Enter Your Name:");
            Name = Console.ReadLine();
            Console.WriteLine("Select the Range of Marks:");
            Console.WriteLine("1. 0-50");
            Console.WriteLine("2. 51-100");
            Console.Write("Enter Your Choice (1,2):");
            Marks = int.Parse(Console.ReadLine());
            switch (Marks)
            {
                case 1:
                {
                    Console.Write(Name + " your marks are Low.\n");
                }
                break;
                case 2:
                {
                    Console.Write(Name + " your marks are Good. \n");
                }
                break;
                default:
                break;
            }
            Console.Write("\nPress ENTER to quit...");
            Console.ReadLine();
        }
    }
}
```

In Listing 3.4, a string variable called Name and an integer variable called Marks are declared. The Name variable is used to store the name of the user while the Marks variable is used to store either of the two options, 1 and 2 that specify the range within which your marks lie. The value stored in Marks is then matched with the value in the case statement. The code inside the case statement whose value matches with the value of the Marks variable is executed.

- 5. Press the F5 key to run the SwitchStatement application.

The output appears, as shown in Fig.C4-3.9:

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_90_0.png)

Fig.C4-3.9

As seen in Fig.C4-3.9, you are prompted to enter your name.

- 6. Enter your name and press the Enter key.

Now, you are prompted to select the range in which your marks lie, as shown in Fig.C4-3.10:

Now, let's create a console application named WhileLoop to demonstrate how to use the while loop. Perform the following steps to create the WhileLoop application:

- 1. Repeat steps 1 to 3 as discussed earlier while creating the If Example application in the The if Statement section of this chapter.
- 2. Enter WhileLoop in the Name text box to specify the name of the application, and specify an appropriate location for the application in the Location combo box. In this case, we have retained the default location, which is C:\users\temp\documents\visual studio 2010\Projects.
- 3. Click the OK button. The WhileLoop application is created.
- 4. Add the highlighted code given in Listing 3.5 in the Program.cs file:

### Listing 3.5: Using the while Loop

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace WhileLoop
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Loop 1:");
            int i = 0;
            while (i < 5)
            {
                Console.WriteLine("I = {0}", i);
                i++;
            }
            Console.ReadLine();
        }
    }
}
```

In Listing 3.5, the while loop is used to execute the code inside it repeatedly till the specified condition, that is, i<5 evaluates to true. The condition in the while loop is checked before the while loop is executed. If the condition evaluates to true, the statements inside the while loop are executed.

- 5. Press the F5 key to run the WhileLoop application. The output appears, as shown in Fig.C4-3.12:

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_92_0.png)

Fig.C4-3.12

As you can see in Fig.C4-3.12, the while loop continues to print the incremented value of the variable, i, until it remains less than 5.

## The do...while Loop

The function of the do...while loop is similar to that of the while loop. The primary difference between the do...while and while loops is that the condition in the do...while loop is checked at the end of the loop. This implies that the do...while loop executes at least once even if the condition evaluates to false. The syntax of the do...while loop is as follows:

```csharp
do
{
    //statement
} while (condition); //condition
```

Now, let's create a console application named **DoWhileLoop** to demonstrate how to use the **do...while** loop. Perform the following steps to create the **DoWhileLoop** application:

- 1. Repeat steps 1 to 3 as discussed earlier while creating the **If Example** application in the **The if Statement** section of this chapter.
- 2. Enter **DoWhileLoop** in the **Name** text box to specify the name of the application, and specify an appropriate location for the application in the **Location** combo box. In this case, we have retained the default location which is C:\\users\\temp\\documents\\visual studio 2010\\Projects.
- 3. Click the OK button. The **DoWhileLoop** application is created.
- 4. Add the highlighted code given in Listing 3.6 in the **Program.cs** file.

### Listing 3.6: Using the do...while Loop

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace DoWhileLoop
{
    class Program
    {
        static void Main(string[] args)
        {
            int i = 5;
            Console.WriteLine("Loop 1:");
            do
            {
                Console.WriteLine("i = {0}", i);
                i++;
            } while (i < 20);
            Console.ReadLine();
        }
    }
}
```

In Listing 3.6, an integer variable, *i*, is declared and assigned the value 5. The **do...while** loop generates numbers from 5 to 19. The condition, *i*<20, in the **do...while** loop is checked at the end of the loop. When this condition evaluates to false, the **do...while** loop is terminated.

- 5. Press the **F5** key to run the application. The output of the application appears, as shown in Fig.C4-3.13:

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_93_0.png)

**Fig.C4-3.13**

Next, let's discuss about the for loop.

## The for Loop

The function of the for loop is also similar to that of the while loop. The only difference between the two is in the syntax. The syntax of the for loop includes an initializer, condition, and a loop expression. The initializer initializes a variable, the loop expression increments or decrements the value of the variable, and condition refers to a condition specified in the for loop. A for loop repeatedly executes the statement(s) enclosed within it until the specified condition evaluates to false. You can use the for loop when you know how many times you want to execute a statement or a block of statements. The syntax of the for loop is as follows:

```
for ( initializer; condition; loop expression)
{
...
...    //statements
}
```

In the preceding syntax, initializer is the starting value of a variable, condition is the expression that is checked before the execution of a loop, and loop expression either increments or decrements the loop counter.

Now, let's create a console application named ForLoop to demonstrate the use of the for loop. Perform the following steps to create the ForLoop application:

- 1. Repeat steps 1 to 3 as discussed earlier while creating the If Example application in the The if Statement section of this chapter.
- 2. Enter ForLoop in the Name text box to specify the name of the application, and specify an appropriate location for the application in the Location combo box. In this case, we have selected the default location, which is C:\users\temp\documents\visual studio 2010\Projects.
- 3. Click the OK button. The ForLoop application is created.
- 4. Add the highlighted code given in Listing 3.7 in the Program.cs file:

### Listing 3.7: Using the for Loop

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace ForLoop
{
    class Program
    {
        static void Main(string[] args)
        {
            for (int i = 0; i < 5; i++)
            {
                Console.WriteLine("Welcome to C# 2010 in Simple Steps.");
                Console.Write("\nPress ENTER to quit...");
                Console.ReadLine();
            }
        }
    }
}
```

In Listing 3.7, an integer variable, i, is declared and initialized to 0 inside the for loop. The condition for the for loop is set to i<5. In addition, the i variable is incremented by 1 in the for loop expression.

- 5. Press the F5 key to run the ForLoop application. The output appears, as shown in Fig.C4-3.14:
