The following code obtains the substrings you get when the string is split at each space — that is, you get an array of individual words:

```
string[] myWords;
myWords = myString.Split(separator);
```

Next, you loop through the words in this array using foreach and write each one to the console:

```
foreach (string word in myWords)
{
    WriteLine($"{word}");
}
```

> NOTE Each word obtained has no spaces, either embedded in the word or at either end. The separators are removed when you use Split().

# EXERCISES

# 5.1 Which of the following conversions can't be performed implicitly?

+   a. int to short
+   b. short to int
+   c. bool to string
+   d. byte to float

# 5.2 Show the code for a color enumeration based on the short type containing the colors of the rainbow plus black and white. Can this enumeration be based on the byte type?

# 5.3 Will the following code compile? Why or why not?

```
string[] blah = new string[5]
blah[5] = 5th string.
```

# 5.4 Write a console application that accepts a string from the user and outputs a string with the characters in reverse order.

# 5.5 Write a console application that accepts a string and replaces all occurrences of the string no with yes.

# 5.6 Write a console application that places double quotes around each word in a string.

Answers to the exercises can be found in Appendix A.