+   **Outline**
+   
+   - 16.1 Introduction
+   - 16.2 Fundamentals of Characters and Strings
+   - 16.3 string Constructors
+   - 16.4 string Indexer, Length Property and CopyTo Method
+   - 16.5 Comparing strings
+   - 16.6 Locating Characters and Substrings in strings
+   - 16.7 Extracting Substrings from strings
+   - 16.8 Concatenating strings
+   - 16.9 Miscellaneous string Methods
+   - 16.10 Class StringBuilder
+   - 16.11 Length and Capacity Properties, EnsureCapacity Method and Indexer of Class StringBuilder
+   - 16.12 Append and AppendFormat Methods of Class StringBuilder
+   - 16.13 Insert, Remove and Replace Methods of Class StringBuilder
+   - 16.14 Char Methods
+   - 16.15 Introduction to Regular Expressions (Online)
+   - 16.16 Wrap-Up

# ## 16.1 Introduction

This chapter introduces the .NET Framework Class Library’s string- and character-processing capabilities and demonstrates how to use regular expressions to search for patterns in text. The techniques it presents can be employed in most kinds of applications, and particularly in text editors, word processors, page-layout software, computerized typesetting systems and other kinds of text-processing software. Previous chapters presented some basic string-processing capabilities. Now we discuss in detail the text-processing capabilities of class string and type char from the System namespace and class StringBuilder from the System.Text namespace.

We begin with an overview of the fundamentals of characters and strings in which we discuss *character constants* and *string literals*. We then provide examples of class string’s many constructors and methods. The examples demonstrate how to determine the *length* of strings, *copy strings*, *access individual characters* in strings, *search strings*, obtain *substrings* from larger strings, *compare strings*, *concatenate strings*, *replace characters* in strings and convert strings to *uppercase or lowercase* letters.

Next, we introduce class StringBuilder, which is used to assemble strings dynamically. We demonstrate StringBuilder capabilities for determining and specifying the size of a StringBuilder, as well as *appending*, *inserting*, *removing* and *replacing* characters in a StringBuilder object. We then introduce the character-testing methods of struct Char that enable a program to determine whether a character is a digit, a letter, a lowercase letter, an uppercase letter, a punctuation mark or a symbol other than a punctuation mark. Such methods are useful for validating individual characters in user input. In addition, type Char provides methods for converting a character to *uppercase or lowercase*.

We provide an online section at http://www.deitel.com/books/CSharpFP that discusses regular expressions. We present classes Regex and Match from the System.Text.RegularExpressions namespace as well as the symbols that are used to form regular expressions. We then demonstrate how to *find patterns* in a string, *match entire strings to patterns*, *replace characters* in a string that match a pattern and *split strings* at delimiters specified as a pattern in a regular expression.