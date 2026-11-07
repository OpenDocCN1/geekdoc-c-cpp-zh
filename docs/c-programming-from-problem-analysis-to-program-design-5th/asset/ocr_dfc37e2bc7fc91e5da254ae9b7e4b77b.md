```
Line 9: After putback and then cin.get(ch); ch = b
Line 11: After cin.peek(); ch = c
Line 13: After cin.get(ch); ch = c
```

The user input, abcd, allows you to see the effect of the functions get, putback, and peek in the preceding program. The statement in Line 1 prompts the user to enter a string. In Line 2, the statement cin.get(ch); extracts the first character from the input stream and stores it in the variable ch. So after Line 2 executes, the value of ch is 'a'.

The cout statement in Line 4 outputs the value of ch. The statement cin.get(ch); in Line 5 extracts the next character from the input stream, which is 'b', and stores it in ch. At this point, the value of ch is 'b'.

The cout statement in Line 6 outputs the value of ch. The cin.putback(ch); statement in Line 7 puts the previous character extracted by the get function, which is 'b', back into the input stream. Therefore, the next character to be extracted from the input stream is 'b'.

The cin.get(ch); statement in Line 8 extracts the next character from the input stream, which is still 'b', and stores it in ch. Now the value of ch is 'b'. The cout statement in Line 9 outputs the value of ch as 'b'.

In Line 10, the statement ch = cin.peek(); checks the next character in the input stream, which is 'c', and stores it in ch. The value of ch is now 'c'. The cout statement in Line 11 outputs the value of ch. The cin.get(ch); statement in Line 12 extracts the next character from the input stream and stores it in ch. The cout statement in Line 13 outputs the value of ch, which is still 'c'.

Note that the statement ch = cin.peek(); in Line 10 did not remove the character 'c' from the input stream; it only peeked into the input stream. The output of Lines 11 and 13 demonstrates this functionality.

# The Dot Notation between I/O Stream Variables and I/O Functions:
A Precaution

In the preceding sections, you learned how to manipulate an input stream to get data into a program. You also learned how to use the functions get, ignore, peek, and putback. It is important that you use these functions exactly as shown. For example, to use the get function, you used statements such as the following:

```
cin.get(ch);
```

Omitting the dot—that is, the period between the variable cin and the function name get—results in a syntax error. For example, in the statement:

```
cin.get(ch);
```

cin and get are two separate identifiers separated by a dot. In the statement:

```
cinet(ch);
```