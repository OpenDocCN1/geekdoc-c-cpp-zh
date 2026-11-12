> Note: The subtleties of some of the algorithms you encountered in this chapter indicate the need for mathematical techniques to prove their correctness. The application of these techniques during the design of the various components of a solution can help to eliminate errors in logic before they appear in the program. One such technique is mathematical induction; another is the use of loop invariants, which Appendix F discusses.

# SUMMARY

+   1. A grammar is a device for defining a language, which is a set of strings of symbols. By using a grammar to define a language, you often can construct a recognition algorithm that is directly based on the grammar. Grammars are frequently recursive, thus allowing you to describe vast languages concisely.
+   
+   2. To illustrate the use of grammars, we defined several different languages of algebraic expressions. These languages have their relative advantages and disadvantages. Prefix and postfix expressions, though difficult for people to use, have simple grammars and eliminate ambiguity. On the other hand, infix expressions are easier for people to use but require parentheses, precedence rules, and rules of association to eliminate ambiguity. Therefore, the grammar for infix expressions is more involved.
+   
+   3. Backtracking is a solution strategy that involves both recursion and a sequence of guesses that ultimately lead to a solution. If a particular guess leads to an impasse, you retrace your steps in reverse order, replace that guess, and try to complete the solution again.
+   
+   4. A close relationship between mathematical induction and recursion exists. You can use induction to prove properties about a recursive algorithm. For example, you can prove that a recursive algorithm is correct, and you can derive the amount of work it requires.

# EXERCISES

+   1. Trace the following recursive functions:
+      a. isPal with the string abcdeba
+      b. isAnBn with the string AABB
+      c. endPre with the expression -*abcd
+   
+   2. Consider the language that the following grammar defines:
+      <S> = $|<W> | $<S>
+      <W> = abb<a | <W> bb
+      Write all strings that are in this language and that contain seven or fewer characters.
+   
+   3. Write a recursive grammar for the language of strings of one or more letters. The first letter of each string must be uppercase, and all other letters in the string must be lowercase.
+   
+   4. Consider a language of character strings that contain only dots and dashes. All strings in this language contain at least four characters and begin with either two dots or two dashes. If the first two characters are dots, the last one must be a dash; if the first two characters are dashes, the last one must be a dot. Write a recursive grammar for this language.
+   
+   5. Consider a language of strings that contains only X's, Y's, and Z's. A string in this language must begin with an X. If a Y is present in a string, it must be the final character of the string.
+      a. Write a recursive grammar for this language.
+      b. Write all the possible two-character strings of this language.