
Using the data in Fig. 3.1, the first method is pictured in Fig. 3.4(a) and the second method is pictured in Fig. 3.4(b).

![](img/f1df4c31f1795198a6843c842acc2216_72_0.png)

### (a) Records with sentinels.

![](img/f1df4c31f1795198a6843c842acc2216_72_1.png)

### (b) Record whose lengths are listed.

Fig. 3.4

Remark: One might be tempted to store strings one after another by using some separation marker, such as the two dollar signs ($$) in Fig. 3.5(a), or by using a pointer array giving the location of the strings, as in Fig. 3.5(b). These ways of storing strings will obviously save space and are sometimes used in secondary memory when records are relatively permanent and require little change. However, such methods of storage are usually inefficient when the strings and their lengths are frequently being changed.

## Linked Storage

Computers are being used very frequently today for word processing, i.e., for inputting, processing and outputting printed matter. Therefore, the computer must be able to correct and modify the printed matter, which usually means deleting, changing and inserting words, phrases, sentences and even paragraphs in the text. However, the fixed-length memory cells discussed above do not easily lend themselves to these operations. Accordingly, for most extensive word processing applications, strings are stored by means of linked lists. Such linked lists, and the way data are inserted and deleted in them, are discussed in detail in Chapter 5. Here we simply look at the way strings appear in these data structures.

By a (one-way) linked list, we mean a linearly ordered sequence of memory cells, called nodes, where each node contains an item, called a link, which points to the next node in the list (i.e., which contains the address of the next node). Figure 3.6 is a schematic diagram of such a linked list.

![](img/f1df4c31f1795198a6843c842acc2216_73_0.png)

Fig. 3.6 Linked List

Strings may be stored in linked lists as follows. Each memory cell is assigned one character or a fixed number of characters, and a link contained in the cell gives the address of the cell containing the next character or group of characters in the string. For example, consider this famous quotation:

> To be or not to be, that is the question.

Figure 3.7(a) shows how the string would appear in memory with one character per node, and Fig. 3.7(b) shows how it would appear with four characters per node.

![](img/f1df4c31f1795198a6843c842acc2216_73_1.png)

### (a) One character per node.

![](img/f1df4c31f1795198a6843c842acc2216_73_2.png)

### (b) Four characters per node.

Fig. 3.7

## 3.4 CHARACTER DATA TYPE

This section gives an overview of the way various programming languages handle the character data type. As noted in the preceding chapter (in Sec. 2.7), each data type has its own formula for decoding a sequence of bits in memory.

### Constants

Many programming languages denote string constants by placing the string in either single or double quotation marks. For example, 'THE END' and 'TO BE OR NOT TO BE' are string constants of lengths 7 and 18 characters respectively. Our algorithms will also define character constants in this way.

### Variables

Each programming language has its own rules for forming character variables. However, such variables fall into one of three categories: static, semistatic and dynamic. By a static character variable, we mean a variable whose length is defined before the program is executed and cannot change throughout the program. By a semistatic character variable, we mean a variable whose length may vary during the execution of the program as long as the length does not exceed a maximum value determined by the program before the program is executed. By a dynamic character variable, we mean a variable whose length can change during the execution of the program. These three categories correspond, respectively, to the ways the strings are stored in the memory of the computer as discussed in the preceding section.

### Example 3.2

In C, variables are declared using alphanumeric characters. The only special character that is allowed inside a variable name is an underscore (_). Further, a variable name must comply with certain rules; for instance:

- A variable name must always begin with a letter
- A variable name cannot be the same as a system keyword
- No white spaces are allowed inside a variable name

Following are some examples of character variable declaration in C:

```
char a; //declares a single character variable a
char str[20]; //declares a character array (string) of length 20
```

## 3.5 STRINGS AS ADT

Most languages have strings as a built-in data type or a standard library, and a set of operations defined on that type. Therefore, there is actually no need for us to create our own string ADT. However, we can implement our own string data type, if required. The use of a data type in string processing applications should not depend on how it is implemented, or whether it is built-in or user defined. We only need to know what operations are allowed on the string.

A string data type typically should have operations to:

- Return the nth character in a string.
- Set the nth character in a string to c.
- Find the length of a string.
- Concatenate two strings.
- Copy a string.
- Delete part of a string.
- Modify and compare strings in other ways.

The following is a set of operations we might want to do on strings.

| Operation | Description |
|---|---|
| GETCHAR(str, n) | Returns the n<sup>th</sup> character in the string |
| PUTCHAR(str, n, c) | Sets the n<sup>th</sup> character in the string to c |
| LENGTH(str) | Returns the number of characters in the string |
| POS(str1, str2) | Returns the position of the first occurrence of str2 found in str1, or 0 if no match |
| CONCAT(str1, str2) | Returns a new string consisting of characters in str1 followed by characters in str2 |
| SUBSTRING(str1, i, m) | Returns a substring of length m starting at position i in string str |
| DELETE(str, i, m) | Deletes m characters from str starting at position i |
| INSERT(str1, str2, i) | Changes str1 into a new string with str2 inserted in position i |
| COMPARE(str1, str2) | Returns an integer indicating whether str1 > str2 |

Let S1 be a string. There are a number of ways in which this string can be implemented as shown in Example 3.3.

> **Example 3.3**
> 
> Suppose S1 = ‘JANICE’.
> 
> (a) In this case, as the length is known, it can be implemented as a fixed length array, where the first element denotes the length of the string as shown below.
> 
> [6, J, A, N, I, C, E]
> 
> (b) If the length is not known, it can be implemented as an array but with the end of the string indicated using a special ‘NULL’ character denoted by ‘\0’ as shown below. Memory can then be dynamically allocated for the string once we know its length.
> 
> [J, A, N, I, C, E, \0,.....]
> 
> The first implementation has the disadvantages of all fixed length array implementations. However, some operations are efficient, for instance, finding the length.
> 
> The second implementation has the advantages of dynamic allocation of space; modifying the string also may be more efficient, as we need not recalculate size.

## 3.6 STRING OPERATIONS

Although a string may be viewed simply as a sequence or linear array of characters, there is a fundamental difference in use between strings and other types of arrays. Specifically, groups of consecutive elements in a string (such as words, phrases and sentences), called substrings, may be units unto themselves. Furthermore, the basic units of access in a string are usually these substrings, not individual characters.

Consider, for example, the string

```
'TO BE OR NOT TO BE'
```

We may view the string as the 18-character sequence T, O, ␣, B, ..., E. However, the substrings TO, BE, OR, ... have their own meaning.

On the other hand, consider an 18-element linear array of 18 integers,
