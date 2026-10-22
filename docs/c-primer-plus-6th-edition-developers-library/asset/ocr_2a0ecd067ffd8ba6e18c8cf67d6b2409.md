4. Given the program and files in question 3, which of the following are valid commands?

+   a. essayct <essay
+   b. count essay
+   c. essay >count

5. What is EOF?

6. What is the output of each of the following fragments for the indicated input (assume that ch is type int and that the input is buffered)?

a. The input is as follows:
If you quit, I will.[enter]

The fragment is as follows:

```
while ((ch = getchar()) != 'i')
    putchar(ch);
```

b. The input is as follows:
Harhar[enter]

The fragment is as follows:

```
while ((ch = getchar()) != '\n')
{
    putchar(ch++);
    putchar(++ch);
}
```

7. How does C deal with different computers systems having different file and newline conventions?

8. What potential problem do you face when intermixing numeric input with character input on a buffered system?

# Programming Exercises

Several of the following programs ask for input to be terminated by EOF. If your operating system makes redirection awkward or impossible, use some other test for terminating input, such as reading the & character.

1. Devise a program that counts the number of characters in its input up to the end of file.