
# Appendix B = Solutions to Exercises 541

the second row begins with NT, and the third row begins with TLY. In that case, it's likely that the third row should follow the first row.

This is an example in what seems like a perfectly reasonable attempt to add one encryption method to another doesn't really help much. Although adding row transpositions to column transpositions increases the number of possible combinations, it doesn't greatly increase the number of combinations the attacker must consider.

- 5. Example program SwapRowsAndColumns does this.
- 6. Example program CaesarSubstitution does this. The encryption of “Nothing but gibberish” with a shift of 13 is ABGUV ATOHG TVOOR EFV.
- 7. Example program LetterFrequency displays the relative frequencies of the letters in a message. That program finds the following values for the three most common letters in the ciphertext:

| Letter | Frequency | Offset |
| --- | --- | --- |
| K | 18.5% | 6 |
| V | 14.8% | 17 |
| R | 13.0% | 13 |

The CaesarSubstitution example program again with offset 12 to decipher the messages gibberish. Using the text WASAT IMEWH ENCAE SARS BUSTIT UTION WASH ESTAT EOF EARTH (There was a time when Caesar substitution was the state of the art.

- 8. Example program VigenereCipher does this. The decrypted message is AVIGE NERC ISHER ECOMP LICAT EDTHNA CAEAS ARUB STIU TION (A Vigenere cipher is more complicated than Caesar substitution.)
- 9. If you use a one-time pad, you are essentially using a Vigenere cipher where the keyword is the pad. You might get away with this for a while, but eventually, the attacker knows that you are reusing the pad, the cipher may be broken.
- 10. This would happen if a message was lost or you received messages out of order so you're not using the right letters in the pad. You can decrypt the message by starting at different positions in the pad until you find a position that produces a readable message. The number of letters in the pad that you need to tell you how long the message was that you missed. You can either ignore that message or send a message (encrypted, of course) asking for the missing message to be repeated.
- 11. Not much. It would give the attacker information about the length and frequency of the messages you are sending, but the attacker can learn anyway by looking at the lengths of intercepted messages (assuming all messages are intercepted).

# Appendix B — Solutions to Exercises

12. Example program OneTime does this.

13. If you have a cryptographically secure random-number generator, you can use it to generate one-time pads and use those for encryption. A one-time pad is unbreakable because any message letter could become any ciphertext

Conversely, suppose you have an unbreakable encryption scheme. You could use it to encrypt a message consisting of nothing but instances of the letter A to generate a sequence of random letters. You could then use those letters to generate the random numbers for a secure random-number generator.

14. Always sends a message of the same length at the same time every day. If you have nothing to say, just say that. Pad the messages to the same length with random characters. If the encryption is secure, the attacker cannot tell when a message contains important information and when it contains random characters.

15. For this scenario, the answers are as follows:

```
n = 22,577
φ(n) = 106 × 210 = 22,260
d = 18,899
C = 1,3374^{199} mod 22,577 = 13,400
M = 19,905^{189} mod 22,577 = 12,345
```

# Chapter 17: Complexity Theory

- 1. Countingsort and bucketsort don't use comparisons. Instead, they perform mathematical calculations to find where in the sorted list each value should go.
2. This can be reduced to the two-coloring problem. If the graph is two-colorable, it is bipartite. To use a two-coloring algorithm to solve the bipartite detection problem, try to color the graph. If a two-coloring is possible, the graph is bipartite. The two-coloring gives you the node sets for the bipartite graph. Just put nodes with one color in one set and nodes with the other color in the other set.
The two-coloring algorithm described in Chapter 14 runs in polynomial time (actually, it's quite fast), so it's in P, and bipartite detection is in P.
3. The three-cycle problem can be reduced to the bipartite detection problem. If a graph has a cycle of length 3, it is not bipartite. To solve the three-cycle problem, use a bipartite detection algorithm to see if the graph is bipartite. If the graph is bipartite, it does not contain any cycles of length 3.
Note that the converse is not necessarily true. If the graph has cycles of length 3, it is still not bipartite if it has a cycle with an odd length.

Exercise 2 shows that the bipartite detection problem is in P, so the three-cycle problem is also in P.

- 4. The odd-cycle problem also can be reduced to the bipartite problem. If a graph has a cycle with odd length, it is not bipartite. To solve the odd-cycle problem, use a bipartite detection algorithm to see if the graph is bipartite. If the graph is bipartite, it does not contain any cycles of odd length.

Note that for each case, the converse is also true. If the graph has cycles of odd length, it is bipartite.

Exercise 2 shows that the bipartite detection problem is in P, so the odd-cycle problem is also in P.

- 5. A nondeterministic algorithm for solving HAM is as follows: Guess the order in which the nodes can be visited, and then verify (in polynomial time) that the ordering gives a Hamiltonian path. To do that, you need to verify that every node is in the ordering exactly once and that there is a link between the adjacent pairs nodes in the ordering.

- 6. You can use a nondeterministic algorithm similar to the one described in the solution to Exercise 5: Guess the order in which the nodes can be visited, and then verify (in polynomial time) that the ordering gives a Hamiltonian cycle. The only difference is that for this you also need to verify that the first and last nodes are the same.

- 7. HAM and HAMC are very related, but they don't instantly solve each other, because a network can contain a Hamiltonian path without containing a cycle.

To reduce HAMC to HAM, you must find a way to use a HAM algorithm to solve HAMC. In other words, if a network contains a Hamiltonian cycle, you must use a HAM algorithm to detect it.

Unfortunately, you can extend a Hamiltonian path to form a cycle only if the last node in the path has a link leading to the first node in the path. A HAM algorithm might find a path that does not have such a link, so it could not form a cycle.
