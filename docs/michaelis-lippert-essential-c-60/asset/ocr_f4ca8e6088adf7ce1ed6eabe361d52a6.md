continue statement exits the current iteration (regardless of whether additional statements remain) and jumps to the loop condition. At that point, if the loop conditional is still true, the loop will continue execution.

Listing 3.52 uses the continue statement so that only the letters of the domain portion of an email are displayed. Output 3.25 shows the results of Listing 3.52.

# LISTING 3.52: Determining the Domain of an Email Address

```
class EmailDomain
{
    static void Main()
    {
        string email;
        bool insideDomain = false;
        System.Console.WriteLine("Enter an email address: ");

        email = System.Console.ReadLine();

        System.Console.Write("The email domain is: ");

        // Iterate through each letter in the email address.
        foreach (char letter in email)
        {
            if (!insideDomain)
            {
                if (letter == '@')
                {
                    insideDomain = true;
                }
                continue;
            }

            System.Console.Write(letter);
        }
    }
}
```

# OUTPUT 3.25

```
Enter an email address:
mark@dotnetprogramming.com
The email domain is: dotnetprogramming.com
```

In Listing 3.52, if you are not yet inside the domain portion of the email address, you can use a continue statement to move control to the end of the loop, and process the next character in the email address.