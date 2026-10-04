These format specifiers can seem a bit bewildering. (I didn't even mention the detailed currency and date controls.) Explore the topic “format specifiers” in the Help Index for more information. To help you wade through these options, the following OutputFormatControls program enables you to enter a floating-point number followed by a specifier sequence. The program then displays the number, using the specified Format() control:

```
// OutputFormatControls -- Allow the user to reformat input numbers
// using a variety of format specifiers input at run time.
namespace OutputFormatControls
{
    using System;
    public class Program
    {
        public static void Main(string[] args)
        {
            // Keep looping -- inputting numbers until the user
            // enters a blank line rather than a number.
            for(;;)
            {
                // First input a number -- terminate when the user
                // inputs nothing but a blank line.
                Console.WriteLine("Enter a double number");
                string numberInput = Console.ReadLine();
                if (numberInput.Length == 0)
                {
                    break;
                }
                double number = Double.Parse(numberInput);
                // Now input the specifier codes; split them
                // using spaces as dividers.
                Console.WriteLine("Enter the format specifiers"
                    + " separated by a blank "
                    + "(Example: C E F1 NO 0000000.00000)");
                char[] separator = { ' ' };
                string formatString = Console.ReadLine();
                string[] formats = formatString.Split(separator);
                // Loop through the list of format specifiers.
                foreach(string s in formats)
                {
                    if (s.Length != 0)
                    {
                        // Create a complete format specifier
                        // from the letters entered earlier.
                        string formatCommand = "{0:" + s + "}";
                        // Output the number entered using the
                        // reconstructed format specifier.
                        Console.Write(
                            "The format specifier {0} results in ", formatCommand);
                        try
                        {
                            Console.WriteLine(formatCommand, number);
                        }
                        catch(Exception)
                        {
                            Console.WriteLine("<illegal control>");
                        }
                        Console.WriteLine();
                    }
                }
            }
        }
    }
}
```