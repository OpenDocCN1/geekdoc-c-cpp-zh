+   l) Read three double values into variables d, e and f from the string "1.27 10.3 9.432".
+   m) Copy the string stored in array s2 into array s1.
+   n) Assign ptr the location of the first occurrence in s1 of any character from s2.
+   o) Compare the string in s1 with the string in s2. Print the result.
+   p) Assign ptr the location of the first occurrence of c in s1.
+   q) Use sprintf to print the values of integer variables x, y and z into array s1. Each value should be printed with a field width of 7.
+   r) Append 10 characters from the string in s2 to the string in s1.
+   s) Determine the length of the string in s1. Print the result.
+   t) Assign ptr to the location of the first token in s2. Tokens in the string s2 are separated by commas (,).

8.2 Show two different ways to initialize char array vowel1 with the string "AEIOU".

8.3 What, if anything, prints when each of the following C statements is performed? If the statement contains an error, describe the error and indicate how to correct it. Assume the following variable definitions:

```
```c
char s1[50] = "jack";
char s2[50] = "jill";
char s3[50] = "";
```
```

+   a) printf("%c%c", toupper(s1[0]), &s1[1]);
+   b) printf("%s", strcpy(s3, s2));
+   c) printf("%s", strcat(strcat(strcpy(s3, s1), " and "), s2));
+   d) printf("%zu", strlen(s1) + strlen(s2));
+   e) printf("%zu", strlen(s3)); // using s3 after part (c) executes

8.4 Find the error in each of the following and explain how to correct it:

+   a) char s[10] = "";
+      strncpy(s, "hello", 5);
+      printf("%s\n", s);
+   b) printf("%s", 'a');
+   c) char s[12] = "";
+      strcpy(s, "Welcome Home");
+   d) if (strcmp(string1, string2)) {
+         puts("The strings are equal");
+      }

# ## Answers to Self-Review Exercises

8.1 See the answers below:

+   a) c = toupper(c);
+   b) printf("%c%s\n", c, isdigit(c) ? " is a " : " is not a ");
+   c) printf("%c%s\n", c, iscntrl(c) ? " is a " : " is not a ");
+   d) fgets(s1, 100, stdin);