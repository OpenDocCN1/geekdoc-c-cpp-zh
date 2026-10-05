| Letter | Frequency | Letter | Frequency |
| A | 77 | N | 67 |
| B | 17 | O | 67 |
| C | 32 | P | 20 |
| D | 42 | Q | 5 |
| E | 120 | R | 59 |
| F | 24 | S | 67 |
| G | 17 | T | 85 |
| H | 50 | U | 37 |
| I | 76 | W | 12 |
| J | 4 | X | 22 |
| K | 7 | Y | 22 |
| L | 42 | Z | 2 |
| M | 24 | | |

**Figure 5.23** Relative frequencies for the 26 letters of the alphabet as they appear in a selected set of English documents. "Frequency" represents the expected frequency of occurrence over 1000 letters, ignoring case.

amount of space (four bytes). It would seem that words such as "DEED," which are composed of relatively common letters, should be stored in less space than words such as "MUCK," which are composed of relatively uncommon letters.

If some characters are used more frequently than others, it is possible to take advantage of this fact and somehow assign shorter codes? The price could be that other characters require longer codes, but this might be worthwhile if such characters appear rarely enough. This concept is at the head of file compression techniques used today. The next section presents one approach to assigning **variable-length codes**, called Huffman coding. While it is not commonly used in its simplest form for compression schemes (there are better methods), Huffman coding gives the favor of such coding schemes. One motivation for studying Huffman coding is that it provides our first opportunity to see a type of tree structure referred to as a **search trie**.

# 5.6.1 Building Huffman Coding Trees

Huffman coding assigns codes to characters such that the length of the code depends on the relative frequency or **weight** of the corresponding character. Thus, it is a variable-length code. If the estimated frequencies for letters match the actual frequency found in an encoded message, the length of that message would typically be less than a fixed-length code used. The Huffman code for each letter is derived from a full binary tree called the **Huffman tree**, or simply the **Huffman tree**. Each leaf of the Huffman tree corresponds to a letter, and we define the weight of the leaf node to be the weight (frequency) of its associated