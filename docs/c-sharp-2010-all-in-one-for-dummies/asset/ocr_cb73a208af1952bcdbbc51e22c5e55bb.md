```
~~~csharp
// Get the next line.
Console.WriteLine("Enter a string ");
string line = Console.ReadLine();
// Exit the loop if line is a terminator.
string[] terms = { "EXIT", "exit", "QUIT", "quit" };
// Compare the string entered to each of the
// legal exit commands.
bool quitting = false;
foreach (string term in terms)
{
    // Break out of the for loop if you have a match.
    if (String.Compare(line, term) == 0)
    {
        quitting = true;
    }
}
if (quitting == true)
{
    break;
}
// Otherwise, add it to the sentence.
sentence = String.Concat(sentence, line);
// Let the user know how she's doing.
Console.WriteLine("\nYou've entered: " + sentence);
}
Console.WriteLine("\n\nTotal sentence:\n" + sentence);
// Wait for user to acknowledge the results.
Console.WriteLine("Press Enter to terminate...");
Console.Read();
}
}
~~~
```

After prompting the user for what the program expects, the program creates an empty initial sentence string called sentence. From there, the program enters an infinite loop.

![](bbox=[0.08, 0.6, 0.18, 0.69])

The controls while(true) and for(;;) loop forever, or at least long enough for some internal break or return to break you out. The two loops are equivalent, and in practice, you'll see them both. (Looping is covered in Chapter 5 of this minibook.)

BuildASentence prompts the user to enter a line of text, which the program reads using the ReadLine() method. Having read the line, the program checks to see whether it is a terminator using the boldfaced lines in the preceding example.

The termination section of the program defines an array of strings called terms and a bool variable quitting, initialized to false. Each member of the terms array is one of the strings you're looking for. Any of these strings causes the program to quit faster than a programmer forced to write COBOL.

![](bbox=[0.08, 0.84, 0.18, 0.93])

The program must include both "EXIT" and "exit" because Compare() considers the two strings different by default. (The way the program is written, these are the only two ways to spell exit. Strings such as "Exit" and