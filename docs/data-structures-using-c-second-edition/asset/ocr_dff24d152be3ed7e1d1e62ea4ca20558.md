| Code | Character |
|---|---|
| 00 | A |
| 01 | B |
| 10 | C |
| 11 | D |

# Data Coding

When we want to code our data (character) using bits, then we use r bits to code 2^r characters. For example, if r=1, then two characters can be coded. If these two characters are A and 8, then A can be coded as 0 and 8 can be coded as 1 and vice versa. Look at Tables 9.1 and 9.2 which show the range of characters that can be coded by using r=2 and r=3.

| Code | Character |
|---|---|
| 000 | A |
| 001 | B |
| 010 | C |
| 011 | D |
| 100 | E |
| 101 | F |
| 110 | G |
| 111 | H |

Now, if we have to code the data string ABBBBBBAAAACDEFGGGH, then the corresponding code would be:

```
0000001001001001001000000000000001000011100101110110110101101111
```

This coding scheme has a fixed-length code because every character is being coded using the same number of bits. Although this technique of coding is simple, coding the data can be made more efficient by using a variable-length code.

You might have observed that when we write a text in English, all the characters are not used frequently. For example, characters like a, e, i, 1, and r are used more frequently than w, x, y, z and so on. So, the basic idea is to assign a shorter code to the frequently occurring characters and a longer to less frequently occurring characters. Variable-length coding is preferred over fixed-length coding because it requires lesser number of bits to encode the same data.

For variable-length encoding, we first build a Huffman tree. First, arrange all the characters in a priority queue in which the character with the lowest frequency of occurrence has the highest priority. Then, create a Huffman tree as explained in the previous section. Figure 9.24 shows a Huffman tree that is used for encoding the data set.

In the Huffman tree, circles contain the cumulative weights of their child nodes. Every left branch is coded with 0 and every right branch is coded with 1. So, the characters A, E, R, W, X, Y, and z are coded as shown in Table 9.3.

| Character | Code |
|---|---|
| A | 00 |
| E | 01 |
| R | 11 |
| W | 1010 |
| X | 1000 |
| Y | 1001 |
| Z | 1011 |

![](bbox=[0.5, 0.62, 0.75, 0.78])

Thus, we see that frequent characters have a shorter code and infrequent characters have a longer code.

# 9.6 APPLICATIONS OF TREES

+   Trees are used to store simple as well as complex data. Here simple means an integer value, character value and complex data means a structure or a record.