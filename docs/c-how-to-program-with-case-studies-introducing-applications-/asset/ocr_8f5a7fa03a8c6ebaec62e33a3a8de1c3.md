There are a couple of preventative measures you can take to prevent such an attack. If you need to display a string that terminates with a newline, rather than `printf`, use the `puts` function, which displays its string argument followed by a newline. For example, in Fig. 2.1, line 7

```
```c
printf("Welcome to C\\n");
```
```

should be written as

```
```c
puts("Welcome to C!");
```
```

Function `puts` simply displays its string argument’s contents, so a conversion specification would be displayed as its individual characters.

To display a string without a terminating newline character, use `printf` with two arguments—a "%s" format control string and the string to display. The `%s` conversion specification is a placeholder for a string. For example, in Fig. 2.2, line 7

```
```c
printf("Welcome ");
```
```

should be written as

```
```c
printf("%s", "Welcome ");
```
```

As with `puts`, if `printf`’s second argument contains a conversion specification, it will be displayed as its individual characters.

As written, this chapter’s `printf`s actually are secure, but these changes are responsible coding practices that will eliminate certain security vulnerabilities as we get deeper into C. We’ll explain the rationale later in the book. From this point forward, we use these practices in our examples, and you should use them in your code.

# scanf, printf, scanf_s and printf_s

We’ll be saying more about scanf and printf in subsequent Secure C Programming sections, beginning with Section 3.13. We’ll also discuss scanf_s and printf_s, which were introduced in C11 as an attempt to eliminate various scanf and printf security vulnerabilities. In a later Secure C Programming section, we’ll discuss well-known scanf security vulnerabilities and how to avoid them.

![](bbox=[0.061, 0.596, 0.137, 0.622])

# ✓ Self Check

+   1. *(Code)* Rewrite the following statement as an equivalent secure `puts` statement:
+   
+      ```c
+      printf("Enter your age:\n");
+      ```
+   
+      **Answer:** `puts("Enter your age:");`

+   2. *(Code)* Rewrite the following statement as an equivalent secure `printf` statement:
+   
+      ```c
+      printf("Enter your age:");
+      ```
+   
+      **Answer:** `printf("%s", "Enter your age:");`

# Summary

This chapter introduced many important C features, including displaying data on the screen, inputting data from the user, performing calculations and making decisions. In