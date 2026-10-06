# Chapter 12 Text Processing

```
4 // Declare a variable to step through the string.
5 Declare Integer index
7 // Display the characters in the string.
8 For index = 0 To length(name) - 1
9 Display name[index]
10 End For
```

# Program Output

Program 12-3 shows an example of changing individual characters in a string. The program reads a string as input from the keyboard, and then changes each occurrence of the letter "t" to the letter "d."

# Program 12-3

```
1 // Declare a string to hold input.
2 Declare String str
4 // Declare a variable to step through the string.
5 Declare Integer index
7 // Prompt the user to enter a sentence.
8 Display "Enter a sentence."
9 Input str
11 // Change each "t" to a "d".
12 For index = 0 To length(str) - 1
13 If str[index] = "t" Then
14 Set str[index] = "d"
15 End If
16 End For
18 // Display the modified string.
19 Display str
```

# Program Output (with Input Shown in Bold)

Enter a sentence.
Look at that kitty cat! [Enter]
Look at adhad kiddy cad!