# Sec. 5.6 Huffman Coding Trees

This can be reorganized as

```
$c_1f_1 + c_2f_2 + \dots + c_nf_n \over f_T$
```

where $f_i$ is the (relative) frequency of letter $i$ and $f_T$ is the total for all letter frequencies. For this set of frequencies, the expected cost per letter

$[(1\times120)+(3\times121)+(4\times32)+(5\times24)+(6\times9)]/306 = 785/306 \approx 2.57$

A fixed-length code for these eight characters would require $\log 8 = 3$ bits per letter as opposed to about 2.57 bits per letter for Huffman coding. Thus, Huffman coding is expected to save 14% for this set of letters.

Huffman coding for all ASCII symbols would do better than this. The letters of Figure 5.31 are atypical as there are too many common letters compared to the number of rare letters. Huffman coding for 26 letters would yield an expected cost of 4.29 bits per letter. This is somewhat unfair to fixed-length coding because there is actually 32 codes in five bits, but only 26 letters. More generally, Huffman coding of a typical text file will save around 40% over ASCII coding at eight bits per character. Huffman coding for a binary file (such as a compiled) would have a very different set of distribution frequencies and would have a different space savings. Most commercial compression programs use two or three schemes to adapt to different types of files.

In the preceding example, "DEED" was coded in 8, a saving of 35% over the twelve bits by a fixed-length coding. However, "MUCK" requires 18 bits, more space than required by the corresponding fixed-length coding. The problem is that "MUCK" is composed of letters that are not expected to occur often. If the message does not match the expected frequencies of the letters, than the length of the encoding will not be as expected.

# 5.6.3 Search in Huffman Trees

When we decode a character using the Huffman coding tree, we follow a path through the tree dictated by the bits in the code. Each '0' indicates a left branch while '1' indicates a right branch. Now look at Figure 5.26 and consider this structure in terms of searching for a given letter, whose key value is its Huffman code. We see that all letters codes beginning with '0' are stored in the left branch, while all letters with codes beginning with '1' are stored in the right branch. Contrast this with storing records in a BST. There, all records with key value less than the root value are stored in the left branch, while all records with key values greater than the root are stored in the right branch.