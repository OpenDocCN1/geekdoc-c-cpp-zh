The if-else statement works in basically the same manner as the if statement.
The term else implies “in all other cases,” or an “everything else here” type situation.
This ability to alter the direction of our programs is effectively defined as a programming
technique. if-else, however, is still limited to two directions, of which the second is
nonspecific. To specify the second direction or multiple paths, we would have to use the
third type of if statement known as the else-if statement.

# The else-if Statement

Else-if, like else is a dependent or secondary extension to the original if state-
ment. Yet else-if definitely adds something new to the table. Since else-if must
be added after an if statement, we'll alter the previous program once again, this
time giving the user a little more to go by than just the word wrong—see Example
2.5.

# Example 2.5. The else-if statement.

```
using System;

namespace Chapter2 {
    class Class1 {
        static void Main() {
            string input;
            double Answer;

            Console.Write("1 + 1.5 =  ");
            input = Console.ReadLine();
            Answer = double.Parse(input);

            if (Answer == 2.5)
                Console.WriteLine("\n That is correct!");
            else if (Answer > 2.5)
                Console.WriteLine("\n Wrong, too high!!!");
            else if (Answer < 2.5)
                Console.WriteLine("\n Wrong, too low!!!");
        }
    }
}
```