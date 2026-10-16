(take 0 (intlist (+ 1 2) 100)) is then evaluated and returns the empty list '() without forcing the evaluation of (intlist (+ 1 2) 100).

5. The result of (cons 2 '()) is finally evaluated, returning the list (2). Thus, the rest of the integer list is never computed.

The scenario we have just described, together with memoization, is called lazy evaluation. This mechanism of evaluating expressions can be achieved in a functional language without explicit calls to delay and force by requiring the runtime environment to adhere to the following rules:

+   1. All arguments to user-defined functions are delayed.
+   2. All bindings of local names in let and letrec expressions are delayed.
+   3. All arguments to constructor functions (such as cons) are delayed.
+   4. All arguments to other predefined functions, such as the arithmetic functions "1, "*"; and so on, are forced.
+   5. All function-valued arguments are forced.
+   6. All conditions in selection forms such as if and cond are forced.

According to these rules, operations on long lists can only compute as much of the list as is necessary. Lazy evaluation also makes it possible to include potentially infinite lists in languages, because only a part of the list would ever be computed at any one time. Lists that obey lazy evaluation rules are often called streams. This name is suggestive of the infinite nature of lists. A stream can be thought of as a partially computed list whose remaining elements can continue to be computed up to any desired number. Streams are an important mechanism in functional programming. To eliminate side effects completely, input and output must be introduced into functional languages as streams. Note that both Scheme and ML have ad hoc stream constructions (besides the manual delay and force procedures mentioned earlier).14

The primary example of a functional language with lazy evaluation is Haskell (again, named after Haskell B. Curry). Lazy evaluation supports a style of functional programming known as generator-filter programming. The programmer can separate a computation into procedures that generate streams and other procedures that take streams as arguments, without worrying about the efficiency of each step. Procedures that generate streams are called generators, and procedures that modify streams are called filters. For example, the intlist procedure in a previous Scheme example is a generator, and the take procedure is a filter.

A famous problem in functional programming that requires generator-filter programming is the same-fringe problem for lists. Two lists have the same fringe if they contain the same non-null atoms in the same order, or, to put it another way, when they are written as trees, their non-null leaves taken in left-to-right order are the same. For example, the lists ((2 (3)) 4) and (2 (3 4 ())) have the same fringe. To determine whether two lists have the same fringe, we must flatten them to just lists of their atoms:

14 Haskell has replaced I/O streams with a more general construct called a monad, which we also do not study here.