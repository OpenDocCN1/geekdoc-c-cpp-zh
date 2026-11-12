
You now must establish that property is true for an arbitrary k => property is true for k + 1

### Inductive hypothesis.
Assume that the property is true for n = k. That is, assume that factorial(k) = k! = k x (k - 1) x (k - 2) x ... x 1

### Inductive conclusion.
Show that the property is true for n = k + 1. That is, you must show that fact(k + 1) returns the value

(k + 1) x k x (k - 1) x (k - 2) x ... x 2 x 1

By definition of the function fact, fact(k + 1) returns the value

(k + 1) x factorial(k)

But by the inductive hypothesis, fact(k) returns the value

k x (k - 1) x (k - 2) x ... x 2 x 1

Thus, fact(k + 1) returns the value

(k + 1) x k x (k - 1) x (k - 2) x ... x 2 x 1

which is what you needed to show to establish that property is true for an arbitrary k => property is true for k + 1

The inductive proof is thus complete.

## 5.4.2 The Cost of Towers of Hanoi

In Chapter 2, you saw the following solution to the Towers of Hanoi problem:

```
solveTowers(count, source, destination, spare)
    if (count == 1)
        Move a disk directly from source to destination
    else
        solveTowers(count - 1, source, spare, destination)
        solveTowers(1, source, destination, spare)
        solveTowers(count - 1, spare, destination, source)
}
```

We now pose the following question: If you begin with N disks, how many moves does solveTowers make to solve the problem?

Let moves(N) be the number of moves made starting with N disks. When N = 1, the answer is easy:

moves(1) = 1

When N > 1, the value of moves(N) is not so apparent. An inspection of the solveTowers algorithm, however, reveals three recursive calls. Therefore, if you knew how many moves solveTowers made starting with N - 1 disks, you could figure out how many moves it made starting with N disks; that is,

moves(N) = moves(N-1) + moves(1) + moves(N-1)

Thus, you have a recurrence relation for the number of moves required for N disks:

```
moves(1) = 1
moves(N) = 2 × moves(N-1) + 1   if N > 1
```

> A recurrence relation for the number of moves that solve Towers requires for N disks

For example, you can determine moves(3) as follows:

```
moves(3) = 2 × moves(2) + 1
         = 2 × (2 × moves(1) + 1) + 1
         = 2 × (2 × 1 + 1) + 1
         = 7
```

> A closed-form formula for the number of moves that solve Towers requires for N disks

Although the recurrence relation gives you a way to compute moves(N), a closed-form formula—such as an algebraic expression—would be more satisfactory, because you could substitute any given value for N and obtain the number of moves made. However, the recurrence relation is useful because there are techniques for obtaining a closed-form formula from it. Because these techniques are not relevant to us right now, we simply pull the formula out of the blue and use mathematical induction to prove that it is correct.

The solution to the previous recurrence relation is

```
moves(N) = 2^N - 1   for all N >= 1
```

Notice that 2^3 - 1 agrees with the value 7 that was just computed for moves(3).

The proof that moves(N) = 2^N - 1 is by induction on N.

### Basis.
Show that the property is true for N = 1. Here 2^1 - 1 = 1, which is consistent with the recurrence relation specification that moves(1) = 1.

You now must establish that

```
property is true for an arbitrary k => property is true for k + 1
```

### Inductive hypothesis.
Assume that the property is true for N = k. That is, assume

```
moves(k) = 2^k - 1
```

### Inductive conclusion.
Show that the property is true for N = k + 1. That is, you must show that moves(k + 1) = 2^(k+1) - 1. Now

```
moves(k + 1) = 2 × moves(k) + 1    from the recurrence relation
             = 2 × (2^k - 1) + 1    by the inductive hypothesis
             = 2^(k+1) - 1
```

which is what you needed to show to establish that

```
property is true for an arbitrary k => property is true for k + 1
```

The inductive proof is thus complete.

Do not get the false impression that proving properties of programs is an easy matter. These two proofs are about as easy as any will be. However, well-structured programs are far more amenable to these techniques than are poorly structured programs.

Appendix E provides more information about mathematical induction.

> Note: The subtleties of some of the algorithms you encountered in this chapter indicate the need for mathematical techniques to prove their correctness. The application of these techniques during the design of the various components of a solution can help to eliminate errors in logic before they appear in the program. One such technique is mathematical induction; another is the use of loop invariants, which Appendix F discusses.

## SUMMARY

- 1. A grammar is a device for defining a language, which is a set of strings of symbols. By using a grammar to define a language, you often can construct a recognition algorithm that is directly based on the grammar. Grammars are frequently recursive, thus allowing you to describe vast languages concisely.
- 2. To illustrate the use of grammars, we defined several different languages of algebraic expressions. These languages have their relative advantages and disadvantages. Prefix and postfix expressions, though difficult for people to use, have simple grammars and eliminate ambiguity. On the other hand, infix expressions are easier for people to use but require parentheses, precedence rules, and rules of association to eliminate ambiguity. Therefore, the grammar for infix expressions is more involved.
- 3. Backtracking is a solution strategy that involves both recursion and a sequence of guesses that ultimately lead to a solution. If a particular guess leads to an impasse, you retrace your steps in reverse order, replace that guess, and try to complete the solution again.
- 4. A close relationship between mathematical induction and recursion exists. You can use induction to prove properties about a recursive algorithm. For example, you can prove that a recursive algorithm is correct, and you can derive the amount of work it requires.

## EXERCISES

- 1. Trace the following recursive functions:
  - a. isPal with the string abcdeba
  - b. isAnBn with the string AABB
  - c. endPre with the expression -*abcd
- 2. Consider the language that the following grammar defines:
  ```
  <S> = $|<W> | $<S>
  <W> = abb<a | <W> bb
  ```
  Write all strings that are in this language and that contain seven or fewer characters.
- 3. Write a recursive grammar for the language of strings of one or more letters. The first letter of each string must be uppercase, and all other letters in the string must be lowercase.
- 4. Consider a language of character strings that contain only dots and dashes. All strings in this language contain at least four characters and begin with either two dots or two dashes. If the first two characters are dots, the last one must be a dash; if the first two characters are dashes, the last one must be a dot. Write a recursive grammar for this language.
- 5. Consider a language of strings that contains only X's, Y's, and Z's. A string in this language must begin with an X. If a Y is present in a string, it must be the final character of the string.
  - a. Write a recursive grammar for this language.
  - b. Write all the possible two-character strings of this language.
- 6. Consider a language of words, where each word is a string of dots and dashes. The following grammar describes this language:
  ```
  <word> = <dot>|<dash><word>|<word><dot>
  <dot> = .
  <dash> = -
  ```
  - a. Write all three-character strings that are in this language.
  - b. Is the string ...--- in this language? Explain.
  - c. Write a seven-character string that contains more dashes than dots and is in the language. Show how you know that your answer is correct.
  - d. Write pseudocode for a recursive recognition function isIn(str) that returns true if the string str is in this language and returns false otherwise.
- 7. Consider the following grammar:
  ```
  <word> = R|<D><D><word><S>
  <D> = Q|P
  <S> = 1
  ```
  Write pseudocode for a recursive function that returns true if a string is in this language and returns false otherwise.
- 8. Consider the following grammar:
  ```
  <G> = empty string |<E><V><E>|<E><G><V>
  <E> = &|#
  <V> = W|A
  ```
  - a. Write pseudocode for a recursive function that returns true if a string is in this language and returns false otherwise.
  - b. Is the string &W#W in this language?
- 9. Let L be the language L = {S | S is of the form A^n B^2n, for some n > 0}

  Thus, a string is in L if and only if it starts with a sequence of A's and is followed by a sequence of twice as many B's. For example, AABBBB is in L, but ABBB, ABBABB, and the empty string are not.
  - a. Give a grammar for the language L.
  - b. Write a recursive function that determines whether the string strExp is in L.
- 10. Is *a+b-c++/de-fg a prefix expression? Explain in terms of the grammar for prefix expressions.
- 11. Is ab!c*efg*h/+d- a postfix expression? Explain in terms of the grammar for postfix expressions.
- 12. Consider the language that the following grammar defines:
  ```
  <S> = <L>|<D><S><S>
  <L> = A|B
  <D> = 1|2
  ```
  - a. Write all three-character strings that are in this language.
  - b. Write one string in this language that contains more than three characters.
