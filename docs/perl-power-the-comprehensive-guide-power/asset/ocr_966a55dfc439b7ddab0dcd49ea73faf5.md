# The Basics of Calling and Defining a Function

At comment #1, you call the `viewOpening()` function. The form of the function call resembles that of the built-in functions (such as `print()`). It is not necessary, but when you call a function, a good practice involves following the function name with a set of parentheses. Likewise, when you place a function on a separate line and treat it as a separate statement, you close the line with a semicolon.

Comment #2 appears in the definitions section of the program. At comment #2, you see first a typical program comment line used to identify a function. In this case, the comment line consists of dashes and the name of the function. Programmers often insert a few sentences at this point describing the use of function. To save space, such comments do not appear in this section.

The definition of `viewOpening()` characterizes the definition of many basic functions. The first element of the definition consists of the keyword `sub`. This keyword designates that the word immediately following it names a function. The function name, `viewOpening`, represents a convention. The convention involves combining at least two words. You allow the first word to remain in lowercase letters while you capitalize the second word and, in the event that you use still more words, every subsequent word. Here are a few more examples:

+   ```text
+   viewOpening
+   determineQuantity
+   showPreliminaryResults
+   calculateNetGainFromLoss
+   ```

In each case, the words appear in their entirety, not abbreviated. The use of such *verbose* function names constitutes a coding convention that characterizes the work of many programmers. Generally, this approach results in programs that are easier to understand and maintain.

Following the name of the function, you create what is known as the *function block*. Two curly braces, an *opening brace* and a *closing brace*, define the *scope* of the function block. Within the function block you place any statements you choose. The essential features of the function are as follows:

```
```text
sub viewOpening{
}
```
```

The lines that fall within the scope of the `viewOpening` function consist first of a call to the `print()` function and a text block. The lines here differ slightly from those in the Geology Review program of Chapter 11 (Listing11_03). In addition to the use of the `print()` function, the name of the block in this instance is ECOSYS, and to create blank lines, you use the `$ML` and `$NL` identifiers, which hold newline characters.