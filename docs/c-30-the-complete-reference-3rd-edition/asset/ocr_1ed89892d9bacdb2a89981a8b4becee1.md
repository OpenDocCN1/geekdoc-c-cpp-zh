to specify StringComparison.InvariantCulture for the how parameter in which case all cultural differences are avoided. This approach is demonstrated by the following program:

```
// Compare strings using StringComparison enumeration.
using System;

class StrCmpDemo {
    static void Main() {
        // Note: Never embed a password in real code.
        // This is for demonstration purposes only.
        string pwd = "we-23b1x5";
        string str;

        Console.WriteLine("Enter password: ");
        str = Console.ReadLine();

        // Compare using invariant culture.
        if (String.Compare(pwd, str, StringComparison.InvariantCulture) == 0)
            Console.WriteLine("Password accepted.");
        else
            Console.WriteLine("Password invalid.");
    }
}
```

# Concatenating Strings

There are two ways to concatenate (join together) two or more strings. First, you can use the + operator, as demonstrated in Chapter 7. Second, you can use one of the various concatenation methods defined by String. Although using + is the easiest approach in many cases, the concatenation methods give you an alternative.

The method that performs concatenation is called Concat(). One of its most commonly used forms is shown here:

```
public static string Concat(string str1, string str2)
```

This method returns a string that contains str2 concatenated to the end of str1. Another form of Concat(), shown here, concatenates three strings:

```
public static string Concat(string str1, string str2, string str3)
```

In this version, a string that contains the concatenation of str1, str2, and str3 is returned. There is also a form that concatenates four strings:

```
public static string Concat(string str1, string str2, string str3, string str4)
```

This version returns the concatenation of all four strings. The version of Concat() shown next concatenates an arbitrary number of strings:

```
public static string Concat(params string[] strs)
```