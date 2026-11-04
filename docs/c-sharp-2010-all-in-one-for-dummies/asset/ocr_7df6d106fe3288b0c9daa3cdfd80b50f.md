![](bbox=[0.07, 0.15, 0.2, 0.3])

To be truly complete, you need to include the decimal point for floating-point variables and include a leading minus sign for negative numbers — but hey, you get the idea.

# Here's the method:

```
// IsAllDigits -- Return true if all characters
// in the string are digits.
public static bool IsAllDigits(string raw)
{
 // First get rid of any benign characters at either end;
 // if there's nothing left, you don't have a number.
 string s = raw.Trim(); // Ignore white space on either side.
 if (s.Length == 0) return false;
 // Loop through the string.
 for(int index = 0; index < s.Length; index++)
 {
 // A nondigit indicates that the string probably isn't a number.
 if (Char.IsDigit(s[index]) == false) return false;
 }
 // No nondigits found; it's probably okay.
 return true;
}
```

The method IsAllDigits() first removes any harmless white space at either end of the string. If nothing is left, the string was blank and could not be an integer. The method then loops through each character in the string. If any of these characters turns out to be a nondigit, the method returns false, indicating that the string is probably not a number. If this method returns true, the probability is high that the string can be converted into an integer successfully.

The following code sample inputs a number from the keyboard and prints it back out to the console. (I omitted the IsAllDigits() method from the listing to save space, but I've boldfaced where this program calls it.)

![](bbox=[0.08, 0.77, 0.2, 0.88])

```
// IsAllDigits -- Demonstrate the IsAllDigits method.
using System;
namespace IsAllDigits
{
 class Program
 {
 public static void Main(string[] args)
 {
 // Input a string from the keyboard.
 Console.WriteLine("Enter an integer number:");
 string s = Console.ReadLine();
 // First check to see if this could be a number.
 if (!IsAllDigits(s)) // Call the special method.
 {
 Console.WriteLine("Hey! That isn't a number!");
 }
 else
 {
 // Convert the string into an integer.
 int n = Int32.Parse(s);
```