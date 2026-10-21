+   - Forgetting to use appropriate namespaces.
+   - Improper choice of metacharacters in regular expressions.
+   - Using StringBuilder methods that are not members of String class to manipulate string objects.
+   - Attempting to access a character that is outside the bounds of a string.

# Review Questions

+   10.1 Distinguish between String and StringBuilder classes.
+   10.2 Distinguish between a string object and string literal.
+   10.3 What is concatenation? How is it achieved in C#?
+   10.4 What is the typical use of the ToString method?
+   10.5 How would you use a ReadLine method to create a string?
+   10.6 What is a verbatim string? Where and when do you use it?
+   10.7 What is an immutable string? How can we modify such a string?
+   10.8 Compare the functioning of two versions of the Compare method. Give typical use of these methods.
+   10.9 How do you invoke the overloaded Equals method?
+   10.10 String class supports two Substring methods. How do they differ? Give an example where both the methods will return the same substring.
+   10.11 When do you use the System.Text namespace?
+   10.12 How would you create an array of strings? Give an example of its typical use.
+   10.13 How would you create a mutable string? How does it differ from creating an immutable string?
+   10.14 What does an Append method achieve?
+   10.15 What is AppendFormat method? How is it different from the Append method?
+   10.16 What are regular expressions? When do you use them?
+   10.17 Lists atleast three properties provided by the StringBuilder class. State their typical use in string manipulations.
+   10.18 Find errors, if any, in the following statements:
+   (a) string s1 = ("abc + xyz");
+   (b) String s2 = s1 + "abc";
+   (c) string s1.Copy ("abc");
+   (d) string s3 = "@\ABC\n\Csharp;"
+   10.19 State what the following statements would accomplish?
+   (a) int n = s1.Length;
+   (b) int m = s1.IndexOf ("are");
+   (c) string s2 = s1.Insert (s1.IndexOf("OK"), "not");
+   (d) int n = string.Compare (s1, s2, false);
+   (e) Console.WriteLine (s1[5]);
+   10.20 State whether the following statements are true or false:
+   (a) All methods of System.String class can work on the objects of string type.
+   (b) The ToString method is used to convert a System.String object to a string type string.