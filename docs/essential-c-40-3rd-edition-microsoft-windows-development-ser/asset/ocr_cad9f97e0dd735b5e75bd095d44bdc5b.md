```
System.Console.WriteLine("Hey you!");
System.Console.Write("Enter your first name: ");
firstName = System.Console.ReadLine();
System.Console.Write("Enter your last name: ");
lastName = System.Console.ReadLine();
System.Console.WriteLine(
    "Your full name is {0} {1}.", firstName, lastName);
}
```

# OUTPUT 1.5:

```
Hey you!
Enter your first name: Inigo
Enter your last name: Montoya
Your full name is Inigo Montoya.
```

Instead of writing out Your full name is followed by another Write statement for firstName, a third write statement for the space, and finally a writeline statement for lastName, Listing 1.15 writes out the entire output using composite formatting. With composite formatting, the code first supplies a format string to define the output format. In this example, the format string is "Your full name is {0} {1}." It identifies two indexed placeholders for data insertion in the string.

Note that the index value begins at zero. Each inserted parameter (known as a format item) appears after the format string in the order corresponding to the index value. In this example, since firstName is the first parameter to follow immediately after the format string, it corresponds to index value 0. Similarly, lastName corresponds to index value 1.

Note that the placeholders within the format string need not appear in order. For example, Listing 1.16 switches the order of the indexed placeholders and adds a comma, which changes the way the name is displayed (see Output 1.6).

# LISTING 1.16: Swapping the Indexed Placeholders and Corresponding Variables

```
System.Console.WriteLine("Your full name is {1}, {0}",
    firstName, lastName);
```