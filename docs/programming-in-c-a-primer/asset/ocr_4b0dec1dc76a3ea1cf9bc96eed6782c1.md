```
s[n-1] = '!';
Console.WriteLine("Final string      : " + s);
}
```

Look at the output produced by Program 10.3:

+   Original string  :  Object
+   Length           :  7
+   String now       :  Object language
+   Modified string  :  Object oriented language
+   Final string     :  Object oriented language!

Program 10.4 accepts two string inputs from users and appends the first string to a predefined value. Using StringBuilder class, a string value is inserted in the string. Then, all spaces in first string are replaced with * and the program calculates the length of the two strings after appending.

# Program 10.4    USING STRINGBUILDER CLASS

```
using System;
using System.Collections.Generic;
using System.Text;
namespace StringExample
{
    class Program
    {
        public void Show()
        {
            string str1="";
            string str2="";
            Console.Write("Please enter a string : ");
            str1 = Console.ReadLine();
            Console.Write("Please enter another string : ");
            str2 = Console.ReadLine();
            StringBuilder builder1 = new StringBuilder(str1, 4);
            StringBuilder builder2 = new StringBuilder(str2, 4);
            int cap = builder1.EnsureCapacity(55);
            Console.Write("string str1 appended to : ");
            builder1.Append(". This is a class test.");
            Console.WriteLine(builder1);
            Console.Write("string str2 inserted with : ");
            builder2.Insert(2, " String Builder");
            Console.WriteLine(builder2);
            Console.WriteLine("\nSecond character of string2 removed.\n");
            builder2.Remove(2, 4);
            Console.WriteLine(builder2);
            builder1.Replace(' ', '*');
            Console.WriteLine("\nSpaces removed from string1\n");
            Console.WriteLine(builder1);
```