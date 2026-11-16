+   4. Let \( A \) be a subset of some given universal set \( U \). Verify that \( \overline{A} = A \) and that \( A \cup \overline{A} = U \).
+   
+   5. Verify the second of DeMorgan's Laws for sets, \( \overline{A \cap B} = \overline{A} \cup \overline{B} \). For each step in your verification, state why that step is valid.
+   
+   6. The subset operator, \( \subseteq \), is defined in terms of the logical implication operator, \( \rightarrow \). However, \( \subseteq \) differs from the \( \cap \) and \( \cup \) operators in that \( A \cap B \) and \( A \cup B \) are sets, while \( A \subseteq B \) is a statement. So the relationship between \( \subseteq \) and \( \rightarrow \) isn't quite the same as the relationship between \( \cup \) and \( \lor \) or between \( \cap \) and \( \land \). Nevertheless, \( \subseteq \) and \( \rightarrow \) do share some similar properties. This problem shows one example.
+   
+   a) Show that the following three compound propositions are logically equivalent: \( p \rightarrow q \), \( (p \land q) \rightarrow p \), and \( (p \lor q) \rightarrow q \).
+   
+   b) Show that for any sets \( A \) and \( B \), the following three statements are equivalent: \( A \subseteq B \), \( A \cap B = A \), and \( A \cup B = B \).
+   
+   7. DeMorgan's Laws apply to subsets of some given universal set \( U \). Show that for a subset \( X \) of \( U \), \( \overline{X} = U \setminus X \). It follows that DeMorgan's Laws can be written as \( U \setminus (A \cup B) = (U \setminus A) \cap (U \setminus B) \) and \( U \setminus (A \cap B) = (U \setminus A) \cup (U \setminus B) \). Show that these laws hold whether or not \( A \) and \( B \) are subsets of \( U \). That is, show that for any sets \( A \), \( B \), and \( C \), \( C \setminus (A \cup B) = (C \setminus A) \cap (C \setminus B) \) and \( C \setminus (A \cap B) = (C \setminus A) \cup (C \setminus B) \).
+   
+   8. Show that \( A \cup (A \cap B) = A \) for any sets \( A \) and \( B \).
+   
+   9. Let \( X \) and \( Y \) be sets. Simplify each of the following expressions. Justify each step in the simplification with one of the rules of set theory.
+   
+   a) \( X \cup (Y \cap X) \)
+   b) \( (X \cap Y) \cap \overline{X} \)
+   c) \( (X \cup Y) \cap Y \)
+   d) \( (X \cup Y) \cup (X \cap Y) \)
+   
+   10. Let \( A \), \( B \), and \( C \) be sets. Simplify each of the following expressions. In your answer, the complement operator should only be applied to the individual sets \( A \), \( B \), and \( C \).
+   
+   a) \( \overline{A \cup B \cup C} \)
+   b) \( \overline{A \cup B \cap C} \)
+   c) \( \overline{A \cup B} \)
+   d) \( \overline{B \cap C} \)
+   e) \( \overline{A \cap B \cap C} \)
+   f) \( \overline{A \cap A \cup B} \)
+   
+   11. Use induction to prove the following generalized DeMorgan's Law for set theory: For any natural number \( n \ge 2 \) and for any sets \( X_1, X_2, \dots, X_n \), \(\overline{X_1 \cap X_2 \cap \cdots \cap X_n} = \overline{X_1} \cup \overline{X_2} \cup \cdots \cup \overline{X_n}\).
+   
+   12. State and prove generalized distributive laws for set theory.

# ## 2.3 Application: Programming with Sets

On a computer, all data are represented, ultimately, as strings of zeros and ones. At times, computers need to work with sets. How can sets be represented as strings of zeros and ones?