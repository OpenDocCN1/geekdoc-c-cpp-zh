# **LISTING 1.19: Commenting Your Code**

```
class Comment Samples
{
static void Main()
{
string firstName; // Variable for storing the first name
string lastName; // Variable for storing the last name
System.Console.WriteLine("Hey you!");
System.Console.Write /* No new line */ ("Enter your first name: ");
firstName = System.Console.ReadLine();
System.Console.Write /* No new line */ ("Enter your last name: ");
lastName = System.Console.ReadLine();
/* Display a greeting to the console using composite formatting. */
System.Console.WriteLine("Your full name is {0} {1}", firstName, lastName);
// This is the end
// of the program listing
}
}
```

# **OUTPUT 1.7**

```
Hey you!
Enter your first name: Inigo
Enter your last name: Montoya
Your full name is Inigo Montoya.
```

In spite of the inserted comments, compiling and executing the new program produces the same output as before.

Programmers use comments to describe and explain the code they are writing, especially where the syntax itself is difficult to understand, or perhaps a particular algorithm implementation is surprising. Since comments are pertinent only to the programmer reviewing the code, the compiler ignores comments and generates an assembly that is devoid of any trace that comments were part of the original source code.

Table 1.2 shows four different C# comment types. The program in Listing 1.18 includes two of these.