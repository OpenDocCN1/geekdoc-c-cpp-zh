# **Drill**

+   1.  Find out if **regex** is shipped as part of your standard library. Hint: Try `std::regex` and `tr1::regex`.
2.  Get the little program from §23.7 to work; that may involve figuring out how to set the project and/or command-line options to link to the **regex** library and use the **regex** headers.
3.  Use the program from drill 2 to test the patterns from §23.7.

# **Review**

+   1.  Where do we find “text”?
2.  What are the standard library facilities most frequently useful for text analysis?
3.  Does `insert()` add before or after its position (or iterator)?
4.  What is Unicode?
5.  How do you convert to and from a **string** representation (to and from some other type)?
6.  What is the difference between `cin>>s` and `getline(cin,s)` assuming **s** is a **string**?
7.  List the standard streams.
8.  What is the key of a **map**? Give examples of useful key types.
9.  How do you iterate over the elements of a **map**?
10. What is the difference between a **map** and a **multimap**? Which useful **map** operation is missing for **multimap**, and why?
11. What operations are required for a forward iterator?
12. What is the difference between an empty field and a nonexistent field? Give two examples.
13. Why do we need an escape character to express regular expressions?
14. How do you get a regular expression into a **regex** variable?
15. What does `\w+\s\d{4}` match? Give three examples. What string literal would you use to initialize a **regex** variable with that pattern?
16. How (in a program) do you find out if a string is a valid regular expression?
17. What does `regex_search()` do?
18. What does `regex_match()` do?
19. How do you represent the character dot (.) in a regular expression?
20. How do you represent the notion of “at least three” in a regular expression?
21. Is **7** a **\w** character? Is `_` (underscore)?
22. What is the notation for an uppercase character?
23. How do you specify your own character set?
24. How do you extract the value of an integer field?