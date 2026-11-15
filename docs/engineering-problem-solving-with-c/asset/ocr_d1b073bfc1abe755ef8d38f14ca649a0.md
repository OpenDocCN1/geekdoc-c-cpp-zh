+   18. Write a function that receives a pointer to a character string and a character. The function should return the number of times that the character occurred in the string. Assume that the function has the prototype statement
+   
+   int charcnt(char *ptr, char c);

+   19. Write a function that receives a pointer to a character string and returns the number of repeated characters that occur in the string. For example, the string “Mississippi” has three repeated characters. Do not count repeated blanks in the string. If a character occurs more than two times, it should still only count as one repeated character; thus, “hisssss” would have only one repeated character. Assume that the function has the prototype statement
+   
+   int repeat(char *ptr);

+   20. Rewrite the function from Problem 19 so that each pair of characters is counted as a repeat. Thus, the string “hisssss” would have four repeated characters. Assume that the function has the prototype statement
+   
+   int repeat2(char *ptr);

+   21. Write a function that receives pointers to two character strings and returns a count of the number of times that the second character string occurs in the first character string. Do not allow overlap of the occurrences. Thus, the string “110101” contains only one occurrence of “101.” Assume that the function has the prototype statement
+   
+   int overlap(char *ptr1, char *ptr2);

+   22. Rewrite the function from Problem 21 so that overlap of the occurrences of the second string in the first string is allowed. Thus, the string “110101” contains two occurrences of “101.” Assume that the function has the prototype statement
+   
+   int overlap(char *ptr1, char *ptr2);

+   23. Rewrite the function in Problem 19 using the string class instead of C-style strings. Assume that the function has the prototype statement
+   
+   int repeat(string);

+   24. Rewrite the function in Problem 20 using the string class instead of C-style strings. Assume that the function has the prototype statement
+   
+   int repeat2(string);

+   25. Rewrite the function in Problem 21 using the string class instead of C-style strings. Assume that the function has the prototype statement
+   
+   int pattern(string, string);