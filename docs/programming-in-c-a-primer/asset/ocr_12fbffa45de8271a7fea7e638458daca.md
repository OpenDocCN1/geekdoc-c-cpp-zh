These classes provide a number of useful overloaded instance and static methods that could be exploited for various situations. Program 10.7 illustrates the use of Regex class and regular expressions for splitting a string into separate words.

# Program 10.7    USE OF REGULAR EXPRESSIONS

```
using System;
using System.Text;    //for StringBuilder class
using System.Text.RegularExpressions; //for Regex class
Class RegexTest
{
    public static void Main ()
    {
        string str;
        str = "Amar, Akbar, Antony are friends!";
        Regex reg = new Regex(" |,");
        StringBuilder sb = new StringBuilder();
        int count = 1;
        foreach(string sub in reg.Split(str))
        {
            sb.AppendFormat("{0}: {1}\n", count++, sub);
        }
        Console.WriteLine(sb);
    }
}
```

Program 10.7 would produce the following output:

+   1: Amar
+   2: Akbar
+   3: Antony
+   4: are
+   5: friends!

The program creates a regular expression object reg using the class Regex and stores the regular expression " |," in it. This pattern is used to search the string "Amar, Akbar, Antony are friends!" with the help of Split() method of Regex class. The call reg.Split(str) in the foreach statement splits the string wherever a comma or space appears and returns the substring to sub. These substrings are appended to the StringBuilder string sb using the AppendFormat method of StringBuilder. The output shows that the given string has been split into separate words using the separators ‘space’ and ‘comma’.