# Compound if Statements

A compound statement is a group of statements combined into a bundle enclosed by a pair of braces. A compound if statement is an if statement that executes this bundle as if it were a single action. The proper way to write a compound statement is demonstrated in Example 2.7. (Note: Either else or else-if could still be used simply by placing those keywords at the end of the compound statement.)

# Example 2.7. A compound if statement.

```
```csharp
using System;

namespace Chapter2 {
    class Class1 {
        static void Main() {
            string input;
            float MyNumber;

            Console.WriteLine("How old are you? ");
            input = Console.ReadLine();
            MyNumber = float.Parse(input);

            if (MyNumber >= 18) {  // compound statement
                Console.WriteLine("\n You're an adult");
                Console.WriteLine("You can vote\n");
            } else
                Console.WriteLine("\n Your turn will come");
        }
    }
}
```
```

The rules guiding the execution of compound if statements are simple. When the if statement is true, all the statements inside the compound statement are executed, and when the if statement is false, all the statements are ignored. This may not seem like much when discussing a compound statement made up of only two lines, but imagine dealing with compound statements of over two hundred lines. Many C# commands can be placed inside of these compound statements including other if statements, but we'll leave such matters to the sections ahead. The else and else-if statements can also use compound statements, as demonstrated in Example 2.8. Notice how important it becomes to comments when programs become longer and more complicated.