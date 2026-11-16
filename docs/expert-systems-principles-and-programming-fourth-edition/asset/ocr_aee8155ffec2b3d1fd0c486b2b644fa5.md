ancestor(ann, Z) and ancestor(Z, john) must be proven true. PROLOG tries to match the subgoals in a left-to-right manner starting with ancestor(ann, Z). Starting from the top, this first match’s statement (1) and so PROLOG tries to prove the body of (1), parent(ann, Z). Starting to search from the top again, this body first matches statement (3) and so PROLOG sets Z to mary. Now PROLOG tries to match the second subgoal of (2) as ancestor(mary, john). This matches (1) and so PROLOG tries to satisfy its body, parent(mary, john). However, there is no parent(mary, john) in the statements (3) through (6) and so this search fails.

PROLOG then reconsiders its guess that Z should be mary. Since this choice did not work, it tries to find another value that will work. Another possibility arises from (4) by setting Z to susan. This technique of going back to try a different search path when one path fails is called backtracking, and is often used for problem solving.

With the choice of Z as susan, PROLOG attempts to prove that ancestor(susan, john) is true. By (1), the body parent(susan, john) must be proven true. Indeed, the fact (3) does match and so the query:

```
:- ancestor(ann, john)
```

is proven true since its conditions have been proven true.

Notice that the control structure of PROLOG is of the Markov algorithm type, where searching for pattern matching is normally determined by the order that the Horn clauses are entered. This contrasts with rule-based expert systems, which normally follow the Post paradigm, in which the order that rules are entered does not affect the search.

PROLOG has many other features and capabilities not mentioned here. From an expert systems point of view, the backtracking and pattern matching are especially relevant. The declarative nature of PROLOG is also useful because a program specification is an executable program.

# ## 2.7 DIFFICULTIES WITH SEMANTIC NETS

Although semantic nets can be very useful in representing knowledge, they have limitations, such as the lack of link name standards discussed previously. This makes it difficult to understand what the net is really designed for and whether it was designed in a consistent manner. A complementary problem of naming links is the naming of nodes. If a node is labeled "chair," for example, does it represent:

+   - a specific chair
+   - the class of all chairs
+   - the concept of a chair
+   - the person who is the chair of a meeting

or something else? For a semantic net to represent definitive knowledge, that is, knowledge that can be defined, the link and node names must be