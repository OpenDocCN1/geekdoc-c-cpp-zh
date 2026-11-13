The running time of the above algorithm is proportional to the number of times the Step 2 loop is executed. The worst case occurs when all of the text T is read, i.e., when the loop is executed n = LENGTH(T) times. Accordingly, we can state the following: The complexity of this pattern matching algorithm is equal to O(n).

Remark: A combinatorial problem is said to be solvable in polynomial time if there is an algorithmic solution with complexity equal to O(n^m) for some m, and it is said to be solvable in linear time if there is an algorithmic solution with complexity equal to O(n), where n is the size of the data. Thus the second of the two pattern matching algorithms described in this section is solvable in linear time. (The first pattern matching algorithm was solvable in polynomial time.)

# SOLVED PROBLEMS

# Terminology; Storage of Strings

+   3.1 Let W be the string ABCD. (a) Find the length of W. (b) List all substrings of W. (c) List all the initial substrings of W.

+   (a) The number of characters in W is its length, so 4 is the length of W.

+   (b) Any subsequence of characters of W is a substring of W. There are 11 such substrings:
+   Substrings: ABCD, ABC, BCD, AB, BC, CD, A, B, C, D, Λ
+   Lengths: 4 3 2 1 0
+   (Here Λ denotes the empty string.)

+   (c) The initial substrings are ABCD, ABC, AB, A, Λ; that is, both the empty string and those substrings that begin with A.

+   3.2 Assuming a programming language uses at least 48 characters—26 letters, 10 digits and a minimum of 12 special characters—give the minimum number and the usual number of bits to represent a character in the memory of the computer.

Since 2^5 < 48 < 2^6, one requires at least a 6-bit code to represent 48 characters. Usually a computer uses a 7-bit code, such as ASCII, or an 8-bit code, such as EBCDIC, to represent characters. This allows many more special characters to be represented and processed by the computer.

+   3.3 Describe briefly the three types of structures used for storing strings.

+   (a) Fixed-length-storage structures. Here strings are stored in memory cells that are all of the same length, usually space for 80 characters.

+   (b) Variable-length storage with fixed maximums. Here strings are also stored in memory cells all of the same length; however, one also knows the actual length of the string in the cell.

+   (c) Linked-list storage. Here each cell is divided into two parts; the first part stores a single character (or a fixed small number of characters), and the second part contains the address of the cell containing the next character.