```
printf("\n");
printf("word1 = %s\nword2 = %s\n", word1, word2);
printf("word3 = %s\nword4 = %s\n", word3, word4);
}
```

Output
Enter text :
Oxford Road, London M17ED
word1 = Oxford
word2 = Road,
word3 = London
word4 = M17ED
Enter text :
Oxford-Road, London-M17ED United Kingdom
word1 = Oxford-Road
word2 = London-M17ED
word3 = United
word4 = Kingdom

Fig. 4.1 Reading a series of words using scanf function

We can also specify the field width using the form %ws in the scanf statement for reading a specified number of characters from the input string . Example:

```
scanf("%ws", name);
```

Here, two things may happen.

+   1. The width w is equal to or greater than the number of characters typed in. The entire string will be stored in the string variable.
+   2. The width w is less than the number of characters in the string. The excess characters will be truncated and left unread.

Consider the following statements:

```
char name[10];
scanf("%5s", name);
```

The input string RAM will be stored as:

![](bbox=[0.28, 0.7, 0.88, 0.78])

The input string KRISHNA will be stored as:

![](bbox=[0.28, 0.84, 0.88, 0.92])

# 4.3.2 Reading a Line of Text

We have seen just now that scanf with %s or %ws can read only strings without whitespaces. That is, they cannot be used for reading a text containing more than one word. However, C supports a format specification known as the edit set conversion code %[...] that can be used to read a line containing a variety of characters,