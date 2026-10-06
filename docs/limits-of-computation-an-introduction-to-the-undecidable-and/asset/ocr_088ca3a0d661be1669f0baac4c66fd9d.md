# Example

Find an English language palindrome (phrase made up of legal words, that, ignoring spaces, punctuation, and upper/lowercase, is the same forwards as backwards).

Language problem $L_{palindrome} = \{string s | s is a palindrome according to the above definition\}$

Yes instances: Level; madam, I'm Adam; A man, a plan, a canal, panama

No instances: This is a palindrome; this is not a palindrome

# Example

“Find the nth prime P” can be restated as the decision problem: “Given n and P, is P the nth prime?” (Assume that 2 is the first prime).

Language problem: $L_{nth prime} = \{n, P | n, P are positive integer numbers and P is the nth prime\}$

Yes instances: 1, 2 (two is the first prime); 4, 7; 7, 17

No instances: 2, 8; 7, 19

# Example

“Add the integers n, m in binary to find their sum” is restated as “Given binary integers n, m, r, is r = n + m?”

Language problem: $L_{binary addition} = \{n, m, r | n, m, r are integers in binary and r = n + m\}$

Yes instances: 10, 10, 100; 1, 1, 10

No instances: 10, 10, 101; 1, 1000, 100

# Example

“Given a legal chess board configuration and that it is White’s move, which move should she make?” “Given this chess board and a suggested move, can White force a win by making this move?”

In all cases that we use, there are an infinite number of possible inputs, which are divided into the yes instances and the no instances.