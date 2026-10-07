# SQL Server Database Programming with C#

Two example projects are provided in this part to illustrate 1) to query a string to determine the number of numeric digits it contains, and 2) how to sort lines of structured text, such comma-separated values, by any field in the line.

# 4.4.2.1 Query to Determine the Number of Numeric Digits

Because the String class implements the generic IEnumerable<T> interface, any string can be queried as a sequence of characters. However, this is not a common use of LINQ. For complex pattern matching operations, use the Regex class.

The following example queries a string to determine the number of numeric digits it contains. Note that the query 'reused' after it is executed the first time. This is possible because the query itself does not store any results.

Create a new C# project and name it **QueryStringLinq**, and enter the codes that are shown in Figure 4.26 into the opened code window of the **C# Program** file.

Let's have a closer look at this piece of codes to see how it works.

**A.** The namespace System.IO in the namespace section of this project since we need to use some components in that namespace.

| QueryStringLinq | Main() | |
| using System; using System.Collections.Generic; using System.Linq; using System.Text; using System.IO; namespace QueryStringLinq { class Program { static void Main(string[] args) { string aString = "ABCDE99F-J74-12-89A"; // Select only characters that are numbers Enumerable<char> query = from aString where Char.IsDigit(ch) select ch; // Execute the query foreach (char c in query) Console.Write("" + c + ""); // Call the count on the existing query. int count = query.Count(); Console.WriteLine("Count = " + count + ""); // Select all characters before the first '.\' Enumerable<char> stringQuery2 = aString.TakeWhile(c => c != '!\'); // Execute the second query foreach (char c in stringQuery2) Console.Write(c); Console.WriteLine(System.Environment.NewLine + "Press any key to exit"); } } } |

FIGURE 4.26 The codes for the example project QueryStringLinq.