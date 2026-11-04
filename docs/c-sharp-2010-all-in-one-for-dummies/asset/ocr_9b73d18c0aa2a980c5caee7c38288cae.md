```
```csharp
// ParseSequenceWithSplit -- Input a series of numbers separated by commas,
// parse them into integers and output the sum.
namespace ParseSequenceWithSplit
{
    using System;
    class Program
    {
        public static void Main(string[] args)
        {
            // Prompt the user to input a sequence of numbers.
            Console.WriteLine(
                "Input a series of numbers separated by commas:");
            // Read a line of text.
            string input = Console.ReadLine();
            Console.WriteLine();
            // Now convert the line into individual segments
            // based upon either commas or spaces.
            char[] dividers = { ',', ' ' };
            string[] segments = input.Split(dividers);
            // Convert each segment into a number.
            int sum = 0;
            foreach(string s in segments)
            {
                // Skip any empty segments.
                if (s.Length > 0)
                {
                    // Skip strings that aren't numbers.
                    if (IsAllDigits(s))
                    {
                        // Convert the string into a 32-bit int.
                        int num = 0;
                        if (Int32.TryParse(s, out num))
                        {
                            Console.WriteLine("Next number = {0}", num);
                            // Add this number into the sum.
                            sum += num;
                        }
                        // If parse fails, move on to next number.
                    }
                }
            }
            // Output the sum.
            Console.WriteLine("Sum = {0}", sum);
            // Wait for user to acknowledge the results.
            Console.WriteLine("Press Enter to terminate...");
            Console.ReadLine();
        }
    }
    // IsAllDigits here.
}
```
```

The ParseSequenceWithSplit program begins by reading a string from the keyboard. The program passes the dividers array of char to the Split() method to indicate that the comma and the space are the characters used to separate individual numbers. Either character will cause a split there.