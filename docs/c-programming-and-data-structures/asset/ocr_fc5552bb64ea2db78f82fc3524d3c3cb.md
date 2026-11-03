# 4.52 Computer Programming

(g) The function scanf cannot be used in any way to read a line of text with the white-spaces.

(h) The ASCII character set consists of 128 distinct characters.

(i) In the ASCII collating sequence, the uppercase letters precede lowercase letters.

(j) In C, it is illegal to mix character data with numeric data in arithmetic operations.

(k) The function getchar skips white-space during input.

(l) In C, strings cannot be initialized at run time.

(m) The input function gets has one string parameter.

(n) The function call strcyp(s2, s1); copies string s2 into string s1.

(o) The function call strcmp("abc", "ABC"); returns a positive number.

# 4.2 Fill in the blanks in the following statements.

+   (a) We can use the conversion specification in scanf to read a line of text.

+   (b) We can initialize a string using the string manipulation function .

+   (c) The function strncat has .

+   (d) To use the function atoi in a program, we must include the header file .

+   (e) The function may be replaced by function for printing strings.

# 4.3 Describe the limitations of using getchar and scanf functions for reading strings.

# 4.4 Character strings in C are automatically terminated by the null character. Explain how this feature helps in string manipulations.

# 4.5 Strings can be assigned values as follows:

+   (a) During type declaration char string[] = {"......", "......"};

+   (b) Using strcyp function strcyp(string, "......");

+   (c) Reading using scanf function scanf("%s", string);

+   (d) Reading using gets function gets(string);

Compare them critically and describe situations where one is superior to the others.

# 4.6 Assuming the variable string contains the value "The sky is the limit.", determine what output of the following program segments will be.

+   (a) printf("%s", string);

+   (b) printf("%25.10s", string);

+   (c) printf("%s", string[0]);

+   (d) for (i=0; string[i] != '\0'; i++); printf("%c\n", string[i]);

+   (e) for (i=0; string[i] != '0'; i++); printf("%d\n", string[i]);

+   (f) for (i=0; i < strlen(string); i++)
+   {
+   string[i++] = i;
+   printf("%s\n", string[i]);
+   }

+   (g) printf("%c\n", string[10] + 5);

# 4.7 Which of the following statements will correctly store the concatenation of strings s1 and s2 in string s3?

+   (a) s3 = strcat(s1, s2);

+   (b) strcat(s1, s2);

+   (c) strcat(s1, s2, s3);

+   (d) strcyp(s3, strcat(s1, s2));

+   (e) strcpy(s3, s3, strcat(s1, s2));

+   (f) strcyp(s1, s2, s3);

# 4.8 What will be the output of the following statement?

```
printf("%d", strcyp ("push", "pull"));
```