+   - Compressed or outline views of programs (class names only or logical structures without the contents, also known as “folding”)
+   - Jump to definitions of classes, routines, and variables
+   - Jump to all places where a class, routine, or variable is used
+   - Language-specific formatting
+   - Interactive help for the language being edited
+   - Brace (begin-end) matching
+   - Templates for common language constructs (the editor completing the structure of a for loop after the programmer types for, for example)
+   - Smart indenting (including easily changing the indentation of a block of statements when logic changes)
+   - Automated code transforms or refactorings
+   - Macros programmable in a familiar programming language
+   - Listing of search strings so that commonly used strings don’t need to be retyped
+   - Regular expressions in search-and-replace
+   - Search-and-replace across a group of files
+   - Editing multiple files simultaneously
+   - Side-by-side diff comparisons
+   - Multilevel undo

Considering some of the primitive editors still in use, you might be surprised to learn that several editors include all these capabilities.

# Multiple-File String Searching and Replacing

If your editor doesn’t support search-and-replace across multiple files, you can still find supplementary tools to do that job. These tools are useful for search for all occurrences of a class name or routine name. When you find an error in your code, you can use such tools to check for similar errors in other files.

You can search for exact strings, similar strings (ignoring differences in capitalization), or regular expressions. Regular expressions are particularly powerful because they let you search for complex string patterns. If you wanted to find all the array references containing magic numbers (digits “0” through “9”), you could search for “[“, followed by zero or more spaces, followed by one or more digits, followed by zero or more spaces, followed by “]”. One widely available search tool is called “grep.” A grep query for magic numbers would look like this:

```
grep "\[ * [0-9]+ * \]" *.cpp
```