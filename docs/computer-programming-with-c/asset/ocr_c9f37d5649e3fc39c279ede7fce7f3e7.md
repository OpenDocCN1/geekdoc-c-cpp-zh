will print 65530 which is the address (starting address to be considered) of variable a in memory. Whereas, the statement,

```
```c
printf("%d", a);
```
```

is a normal `printf()` statement to print value of a, which will print 5 on the computer screen.

To summarize this discussion, let us now create a float variable b as shown in the following statement:

```
```c
float b=42.8;
```
```

Because the variable b is 4 bytes in size, it will occupy four locations in RAM. Let the four addresses in RAM where b is stored be 2000, 2001, 2002, and 2003. The address of variable b in such a case should be considered as 2000 because it is the starting address of the variable as shown in the Figure 8.4.

![](bbox=[0.243, 0.367, 0.753, 0.487])

**Figure 8.4:** Storage of variable in RAM

The statement

```
```c
printf("%d", &b);
```
```

will print 2000 which is the address of variable b. Note that we have used control parameter `%d` and not `%f` while printing address, because address of b will always be of type integer even if the value of b is of type float.

Whereas the statement

```
```c
printf("%f", &b);
```
```

will print 42.8 because it is the value stored inside variable b. Note that we have used & in printing the actual value of b.

# How are character and floating point constants stored in computer memory?

> We know that every character has an ASCII value which is in a range from 0 to 255. In order to store a character constant in computer memory, the ASCII value corresponding to the character constant is converted into binary and the resultant bit pattern is stored in computer memory. For example, if we want to store the character constant ‘a’, system will store the bit pattern as 01100001, which is the binary equivalent of 97 (which is ASCII value of ‘a’).
> 
> Floating point numbers will also be converted into binary before they are stored in memory. There are certain floating point formats defined by IEEE which are used to represent floating point numbers in machine language. Discussion of various IEEE formats for floating point representation is out of scope of this text book.