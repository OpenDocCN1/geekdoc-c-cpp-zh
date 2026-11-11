+   14. The function call `strcmp("abc", "ABC");` returns a positive number. (LO 10.4)
+   15. We can assign a character constant or a character variable to an `int` type variable. (LO 10.4)

# ## DISCUSSION QUESTIONS

+   1. Describe the limitations of using `getchar` and `scanf` functions for reading strings. (LO 10.2)

+   2. Character strings in C are automatically terminated by the *null* character. Explain how this feature helps in string manipulations. (LO 10.4)

+   3. Strings can be assigned values as follows: (LO 10.1)
+      (a) During type declaration: `char string[ ] = ".......";` (LO 10.2)
+      (b) Using `strcpy` function: `strcpy(string, ".......");`
+      (c) Reading using `scanf` function: `scanf("%s", string);` (LO 10.4)
+      (d) Reading using `gets` function: `gets(string);`
+      Compare them critically and describe situations where one is superior to the others.

+   4. Assuming the variable `string` contains the value “The sky is the limit”, determine what output of the following program segments will be. (LO 10.3)
+      (a) `printf("%s", string);`
+      (b) `printf("%25.10s", string);`
+      (c) `printf("%s", string[0]);`
+      (d) `for (i=0; string[i] != '\0'; i++) printf("%c", string[i]);`
+      (e) `for (i=0; string[i] != '\0'; i++) printf("%d\n", string[i]);`
+      (f) `for (i=0; i <= strlen[string]; ; ) { string[i++] = i; } printf("%s\n", string[1]);`
+      (g) `printf("%c\n", string[10] + 5);`
+      (h) `printf("%c\n", string[10] + 5);`

+   5. Which of the following statements will correctly store the concatenation of strings s1 and s2 in string s3? (LO 10.4)
+      (a) `s3 = strcat (s1, s2);`
+      (b) `strcat (s1, s2, s3);`
+      (c) `strcat (s3, s2, s1);`
+      (d) `strcpy (s3, strcat (s1, s2));`
+      (e) `strcmp (s3, strcat (s1, s2));`
+      (f) `strcpy (strcat (s1, s2), s3);`

+   6. What will be the output of the following statement? (LO 10.3)
+      `printf ("%d", strcmp ("push", "pull"));`

+   7. Assume that s1, s2 and s3 are declared as follows: (LO 10.4)
+      `char s1[10] = "he", s2[20] = "she", s3[30], s4[30];`