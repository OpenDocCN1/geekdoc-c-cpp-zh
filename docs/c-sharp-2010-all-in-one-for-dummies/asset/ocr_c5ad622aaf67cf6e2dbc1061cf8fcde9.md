In the rest of the chapter, I cover Strings and strings and all the tasks you can accomplish by using them.

# The Union Is Indivisible, and So Are Strings

You need to know at least one thing that you didn’t learn before the sixth grade: You can’t change a string object itself after it has been created. Even though I may speak of modifying a string, C# doesn’t have an operation that modifies the actual string object. Plenty of operations appear to modify the string that you’re working with, but they always return the modified string as a new object, instead. One string becomes two.

For example, the operation "His name is " + "Randy" changes neither of the two strings, but it generates a third string, "His name is Randy". One side effect of this behavior is that you don’t have to worry about someone modifying a string out from under you.

Consider this simplistic example program:

![](bbox=[0.15, 0.58, 0.25, 0.73])

```
// ModifyString -- The methods provided by class String do
// not modify the object itself. (s.ToUpper() doesn't
// modify 's'; rather it returns a new string that has
// been converted.)
using System;
namespace ModifyString
{
class Program
{
public static void Main(string[] args)
{
// Create a student object.
Student s1 = new Student();
s1.Name = "Jenny";
// Now make a new object with the same name.
Student s2 = new Student();
s2.Name = s1.Name;
// 'Changing' the name in the s1 object does not
// change the object itself because ToUpper() returns
// a new string without modifying the original.
s2.Name = s1.Name.ToUpper();
Console.WriteLine("s1 - " + s1.Name + ", s2 - " + s2.Name);
// Wait for user to acknowledge the results.
Console.WriteLine("Press Enter to terminate...");
Console.Read();
}
}
// Student -- You just need a class with a string in it.
class Student
{
public String Name;
}
}
```