based on the circumstances. Such an expert not only gets the code to compile but does so while following best practices that minimize bugs and enable maintenance well into the future. The coding guidelines highlight some of the key principles that readers will want to be sure to incorporate into their development.

# Code Samples

The code snippets in most of this text can run on most implementations of the Common Language Infrastructure (CLI), but the focus is on the Microsoft .NET Framework and the .NET Core implementation. Platform- or vendor-specific libraries are seldom used except when communicating important concepts relevant only to those platforms (e.g., appropriately handling the single-threaded user interface of Windows). Any code that specifically relates to C# 5.0, 6.0, or 7.0 is called out in the C# version indexes at the end of the book.

Here is a sample code listing.

```
**LISTING 1.19: Commenting Your Code**

```
class Comment Samples
{
    static void Main()
    {
        string firstName; //Variable for storing the first name
        string lastName;  //Variable for storing the last name

        System.Console.WriteLine("Hey you!");

        System.Console.Write /* No new line */ (
            "Enter your first name: ");
        firstName = System.Console.ReadLine();

        System.Console.Write /* No new line */ (
            "Enter your last name: ");
        lastName = System.Console.ReadLine();

        /* Display a greeting to the console
           using composite formatting. */
        System.Console.WriteLine("Your full name is {0} {1}.",
            firstName, lastName);
        // This is the end
        // of the program listing
    }
}
```
```