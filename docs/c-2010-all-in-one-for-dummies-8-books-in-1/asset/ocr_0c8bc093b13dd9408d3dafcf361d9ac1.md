# Making Your Console App Do Something

Compile complete -- 0 errors, 0 warnings
Program1 -> C:\Programs\... (and more)==Build: 1 succeeded or up-to-date,
failed, 0 skipped==

The key point is the 1 succeeded part on the last line.

As a general rule of programming, succeeded is good; failed is bad.
The bad — the exceptions — covered in Chapter 9 of this minibook.

To execute the program, Debug:Start. The program brings up a
black window and terminates immediately. (If you have a
computer, the appearance of this window is just a flash on the screen).
The program has seemingly done nothing. In fact, this is the template
is nothing but an empty shell.

An alternative command, Debug:Start Without Debugging, behaves a bit
better at this point. Try it out.

# Making Your Console App Do Something

Edit the Program.cs template file until it appears this way:

```
namespace Program1
{
    public class Program
    {
        // This is your program starts.
        static void Main(string[] args)
        {
            // Prompt user to enter a name.
            Console.WriteLine("Enter your name, ");

// Now read the name entered.
            string name = Console.ReadLine();

            // Greet the user with the name that was entered.
            Console.WriteLine("Hello, " + name);");

            // Wait for user to acknowledge the results.
            Console.WriteLine("Press Enter to terminate...\*");
            Console.Read();
        }
    }
}
```

Don't sweat the following the double or triple slashes (// or /////),
Don't worry about whether to enter one or two spaces or one or two new
lines. However, pay attention to capitalization.