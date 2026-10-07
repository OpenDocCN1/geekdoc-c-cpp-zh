# 150

# Exercises

5.12. Suppose you implement the disjoint-sets data structure using union-rank but not path compression. Give a sequence of $m$ union and find operations on $n$ elements that take $\Omega(m \log n)$ time.

5.13. A long string consists of the four characters $A, C, G, T$; they appear with frequency $31\%, 20\%, 9$, and $40\%$, respectively. What is the Huffman encoding of these characters?

5.14. Suppose the symbols $a, b, c, d, e$ occur with frequencies $1/2, 1/4, 1/8, 1/16, 1/16$, respectively.

+   (a) What is the Huffman encoding of the alphabet?

+   (b) If this encoding is applied to a file consisting of 1,000,000 characters with the frequencies, what is the length of the encoded file in bits?

5.15. Use Huffman's algorithm to obtain an encoding of alphabet $\{a, b, c\}$ with frequencies $f_a, f_b, f_c$. In each of the following cases, either give an example of frequencies $(f_a, f_b, f_c)$ that would yield the specified code, or explain why the code cannot possibly be obtained (no matter what the frequencies are)

+   (a) Code: $[0, 10, 11]$

+   (b) Code: $[0, 1, 00]$

+   (c) Code: $[10, 01, 00]$

5.16. Prove the following two properties of the Huffman encoding scheme.

+   (a) If some character occurs with frequency more than $2/5$, then there is guaranteed to be a codeword of length 1

+   (b) If all characters occur with frequency less than $1/3$, then there is guaranteed to be no codeword of length 1

5.17. Under a Huffman encoding of $n$ symbols with frequencies $f_1, f_2, \dots, f_n$, what is the longest codeword could be? Give an example set of frequencies that would produce this code.

5.18. The following table gives the frequencies of the letters of the English language (including the blank spaces) in a particular corpus.

| | 18.3% | r | 4.8% | y | 1.6% |
|---|---|---|---|---||
| e | 10.2% | d | 3.5% | p | 1.6% |
| t | 7.7% | l | 3.4% | b | 1.3% |
| a | 6.8% | c | 2.6% | v | 0.9% |
| | 5.9% | u | 2.4% | k | 0.6% |
| i | 5.8% | m | 2.1% | j | 0.2% |
| n | 5.5% | w | 1.9% | x | 0.2% |
| s | 5.1% | f | 1.8% | q | 0.1% |
| h | 4.9% | g | 1.7% | z | 0.1% |

+   (a) What is the optimum Huffman encoding of this alphabet?

+   (b) What is the expected number of bits per letter?