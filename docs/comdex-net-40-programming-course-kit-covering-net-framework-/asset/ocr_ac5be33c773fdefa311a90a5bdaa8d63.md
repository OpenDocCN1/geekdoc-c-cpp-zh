# Listing 1.5: Showing the Code to Demonstrate the Use of Nested if Statements

```
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace NestedIfStatements {
    class Program {
        static void Main(string[] args) {
            Console.Write("Enter a vowel:");
            char myChar = Convert.ToChar(Console.ReadLine());
            char x = Char.ToUpper(myChar);
            if (x == 'A')     //First if statement
                Console.WriteLine("The entered vowel is: A");
            else if (x == 'E') //Second if statement
                Console.WriteLine("The entered vowel is: E");
            else if (x == 'I') //Third if statement
                Console.WriteLine("The entered vowel is: I");
            else if (x == 'O') //Fourth if statement
                Console.WriteLine("The entered vowel is: O");
            else if (x == 'U') //Fifth if statement
                Console.WriteLine("The entered vowel is: U");
            else
                Console.WriteLine("The entered character is not a vowel!");
            Console.ReadLine();
        }
    }
}
```
```

In the highlighted lines of Listing 1.5, we first prompt a user to enter a vowel. Then, we store the entered character in that char type variable, myChar. Next, we convert the entered character into its uppercase version and store the uppercase version in another char type variable, x. After this, we use a series of nested if statements to check which of the vowels in the English alphabet was entered by the user, and display a message specifying the entered vowel on the console. In the else clause of the last if statement, we display a message indicating that the entered character is not a vowel. This message is displayed only if none of the conditions in the if statements evaluate to true.

+   8. Press the F5 key on the keyboard to run the application. The output of the application appears, prompting you to enter a vowel, as shown in Fig.C#-1.17.

![](bbox=[0.432, 0.6, 0.591, 0.678])

+   9. Type (a or A) on the console and press the ENTER key. A message appears on the console, indicating that the entered vowel is A, as shown in Fig.C#-1.18.

![](bbox=[0.432, 0.735, 0.591, 0.814])

+   10. Close the console displaying the output.