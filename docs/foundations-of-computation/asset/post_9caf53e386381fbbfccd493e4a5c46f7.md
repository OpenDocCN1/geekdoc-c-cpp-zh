
- 4. Let \( A \) be a subset of some given universal set \( U \). Verify that \( \overline{A} = A \) and that \( A \cup \overline{A} = U \).

- 5. Verify the second of DeMorgan's Laws for sets, \( \overline{A \cap B} = \overline{A} \cup \overline{B} \). For each step in your verification, state why that step is valid.

- 6. The subset operator, \( \subseteq \), is defined in terms of the logical implication operator, \( \rightarrow \). However, \( \subseteq \) differs from the \( \cap \) and \( \cup \) operators in that \( A \cap B \) and \( A \cup B \) are sets, while \( A \subseteq B \) is a statement. So the relationship between \( \subseteq \) and \( \rightarrow \) isn't quite the same as the relationship between \( \cup \) and \( \lor \) or between \( \cap \) and \( \land \). Nevertheless, \( \subseteq \) and \( \rightarrow \) do share some similar properties. This problem shows one example.

  - a) Show that the following three compound propositions are logically equivalent: \( p \rightarrow q \), \( (p \land q) \rightarrow p \), and \( (p \lor q) \rightarrow q \).

  - b) Show that for any sets \( A \) and \( B \), the following three statements are equivalent: \( A \subseteq B \), \( A \cap B = A \), and \( A \cup B = B \).

- 7. DeMorgan's Laws apply to subsets of some given universal set \( U \). Show that for a subset \( X \) of \( U \), \( \overline{X} = U \setminus X \). It follows that DeMorgan's Laws can be written as \( U \setminus (A \cup B) = (U \setminus A) \cap (U \setminus B) \) and \( U \setminus (A \cap B) = (U \setminus A) \cup (U \setminus B) \). Show that these laws hold whether or not \( A \) and \( B \) are subsets of \( U \). That is, show that for any sets \( A \), \( B \), and \( C \), \( C \setminus (A \cup B) = (C \setminus A) \cap (C \setminus B) \) and \( C \setminus (A \cap B) = (C \setminus A) \cup (C \setminus B) \).

- 8. Show that \( A \cup (A \cap B) = A \) for any sets \( A \) and \( B \).

- 9. Let \( X \) and \( Y \) be sets. Simplify each of the following expressions. Justify each step in the simplification with one of the rules of set theory.

  - a) \( X \cup (Y \cap X) \)
  - b) \( (X \cap Y) \cap \overline{X} \)
  - c) \( (X \cup Y) \cap Y \)
  - d) \( (X \cup Y) \cup (X \cap Y) \)

- 10. Let \( A \), \( B \), and \( C \) be sets. Simplify each of the following expressions. In your answer, the complement operator should only be applied to the individual sets \( A \), \( B \), and \( C \).

  - a) \( \overline{A \cup B \cup C} \)
  - b) \( \overline{A \cup B \cap C} \)
  - c) \( \overline{A \cup B} \)
  - d) \( \overline{B \cap C} \)
  - e) \( \overline{A \cap B \cap C} \)
  - f) \( \overline{A \cap A \cup B} \)

- 11. Use induction to prove the following generalized DeMorgan's Law for set theory: For any natural number \( n \ge 2 \) and for any sets \( X_1, X_2, \dots, X_n \), \(\overline{X_1 \cap X_2 \cap \cdots \cap X_n} = \overline{X_1} \cup \overline{X_2} \cup \cdots \cup \overline{X_n}\).

- 12. State and prove generalized distributive laws for set theory.

## 2.3 Application: Programming with Sets

On a computer, all data are represented, ultimately, as strings of zeros and ones. At times, computers need to work with sets. How can sets be represented as strings of zeros and ones?

A set is determined by its elements. Given a set \( A \) and an entity \( x \), the fundamental question is, does \( x \) belong to \( A \) or not? If we know the answer to this question for each possible \( x \), then we know the set. For a given \( x \), the answer to the question, “is \( x \) a member of \( A \),” is either yes or no. The answer can be encoded by letting 1 stand for yes and 0 stand for no. The answer, then, is a single bit, that is, a value that can be either zero or one. To represent the set \( A \) as a string of zeros and ones, we could use one bit for each possible member of \( A \). If a possible member \( x \) is in the set, then the corresponding bit has the value one. If \( x \) is not in the set, then the corresponding bit has value zero.

Now, in cases where the number of possible elements of the set is very large or infinite, it is not practical to represent the set in this way. It would require too many bits, perhaps an infinite number. In such cases, some other representation for the set can be used. However, suppose we are only interested in subsets of some specified small set. Since this set plays the role of a universal set, let’s call it \( U \). To represent a subset of \( U \), we just need one bit for each member of \( U \). If the number of members of \( U \) is \( n \), then a subset of \( U \) is represented by a string of \( n \) zeros and ones. Furthermore, every string of \( n \) zeros and ones determines a subset of \( U \), namely that subset that contains exactly the elements of \( U \) that correspond to ones in the string. A string of \( n \) zeros and ones is called an \( n \)-bit binary number. So, we see that if \( U \) is a set with \( n \) elements, then the subsets of \( U \) correspond to \( n \)-bit binary numbers.

To make things more definite, let \( U \) be the set \( \{0, 1, 2, \dots, 31\} \). This set consists of the 32 integers between 0 and 31, inclusive. Then each subset of \( U \) can be represented by a 32-bit binary number. We use 32 bits because most computer languages can work directly with 32-bit numbers. For example, the programming languages Java, C, and C++ have a data type named int. A value of type int is a 32-bit binary number. 1 Before we get a definite correspondence between subsets of \( U \) and 32-bit numbers, we have to decide which bit in the number will correspond to each member of \( U \). Following tradition, we assume that the bits are numbered from right to left. That is, the rightmost bit corresponds to the element 0 in \( U \), the second bit from the right corresponds to 1, the third bit from the right to 2, and so on. For example, the 32-bit number

```
100000000000000000000100110110
```

corresponds to the subset \( \{1, 2, 4, 5, 6, 9, 31\} \). Since the leftmost bit of the

1 Actually, in some versions of C and C++, a value of type int is a 16-bit number. A 16-bit number can be used to represent a subset of the set \( \{0, 1, 2, \dots, 15\} \). The principle, of course, is the same.

| Hex. | Binary | Hex. | Binary |
| :--- | :--- | :--- | :--- |
| 0 | 0000₂ | 8 | 1000₂ |
| 1 | 0001₂ | 9 | 1001₂ |
| 2 | 0010₂ | A | 1010₂ |
| 3 | 0011₂ | B | 1011₂ |
| 4 | 0100₂ | C | 1100₂ |
| 5 | 0101₂ | D | 1101₂ |
| 6 | 0110₂ | E | 1110₂ |
| 7 | 0111₂ | F | 1111₂ |

Figure 2.3: The 16 hexadecimal digits and the corresponding binary numbers. Each hexadecimal digit corresponds to a 4-bit binary number. Longer binary numbers can be written using two or more hexadecimal digits. For example, 101000011111₂ = 0xA1F.

number is 1, the number 31 is in the set; since the next bit is 0, the number 30 is not in the set; and so on.

From now on, I will write binary numbers with a subscript of 2 to avoid confusion with ordinary numbers. Furthermore, I will often leave out leading zeros. For example, 1101₂ is the binary number that would be written out in full as

```
000000000000000000000000000000000101
```

and which corresponds to the set {0, 2, 3}. On the other hand 1101 represents the ordinary number one thousand one hundred and one.

Even with this notation, it can be very annoying to write out long binary numbers—and almost impossible to read them. So binary numbers are never written out as sequences of zeros and ones in computer programs.

An alternative is to use hexadecimal numbers. Hexadecimal numbers are written using the sixteen symbols 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, A, B, C, D, E, and F. These symbols are known as the hexadecimal digits. Each hexadecimal digit corresponds to a 4-bit binary number, as shown in Figure 2.3. To represent a longer binary number, several hexadecimal digits can be strung together. For example, the hexadecimal number C7 represents the binary number 11000111₂. In Java and many related languages, a hexadecimal number is written with the prefix “0x”. Thus, the hexadecimal number C7 would appear in the program as 0xC7. I will follow the
