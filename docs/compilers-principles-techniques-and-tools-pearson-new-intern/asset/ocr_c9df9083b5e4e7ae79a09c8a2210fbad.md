# 3.3.6 Exercises for Section 3.3

**Exercise 3.3.1:** Consult the language reference manuals to determine (i) the sets of characters that form the input alphabet (excluding those that may only appear in character strings or comments), (ii) the lexical form of numerical constants, and (iii) the lexical form of identifiers, for each of the following languages: (a) C (b) C++ (c) C# (d) Fortran (e) Java (f) Lisp (g) SQL.

**! Exercise 3.3.2:** Describe the languages denoted by the following regular expressions:

+   a) `a(a|b)*a`.
+   
+   b) `((ε|a)b*)*`.
+   
+   c) `(a|b)*a(a|b)(a|b)`.
+   
+   d) `a*ba*ba*ba*`.
+   
+   ! e) `(aa|bb)*((ab|ba)(aa|bb)*(ab|ba)(aa|bb)*)*`.

**Exercise 3.3.3:** In a string of length *n*, how many of the following are there?

+   a) Prefixes.
+   
+   b) Suffixes.
+   
+   c) Proper prefixes.
+   
+   ! d) Substrings.
+   
+   ! e) Subsequences.

**Exercise 3.3.4:** Most languages are *case sensitive*, so keywords can be written only one way, and the regular expressions describing their lexemes are very simple. However, some languages, like SQL, are *case insensitive*, so a keyword can be written either in lowercase or in uppercase, or in any mixture of cases. Thus, the SQL keyword SELECT can also be written `select`, `Select`, or `sElEcT`, for instance. Show how to write a regular expression for a keyword in a case-insensitive language. Illustrate the idea by writing the expression for “select” in SQL.

**! Exercise 3.3.5:** Write regular definitions for the following languages:

+   a) All strings of lowercase letters that contain the five vowels in order.
+   
+   b) All strings of lowercase letters in which the letters are in ascending lexicographic order.
+   
+   c) Comments, consisting of a string surrounded by `/*` and `*/`, without an intervening `*/`, unless it is inside double-quotes (`"`).