# 4.4.1 Notation and Data Structures

Prolog uses notation almost identical to that developed earlier for Horn clauses, except that the implication arrow, ←, is replaced by a colon followed by a dash (or minus sign) (:-). Thus, the sample ancestor program from the previous section would be written in Prolog syntax as follows:

```
ancestor(X, Y) :- parent(X, Z), ancestor(Z, Y).
ancestor(X, X).
parent(amy, bob).
```

and Example 4 would be written as follows:

```
natural(0).
natural(successor(X)) :- natural(X).
```

Note that the variables X and Y are written in uppercase. Prolog distinguishes variables from constants and names of predicates and functions by using uppercase for variables and lowercase for constants and names. It is also possible in most Prolog systems to denote a variable by writing an underscore before the name, as in ancestor(_x,_y).

In addition to the comma connective that stands for and, Prolog uses the semicolon for or. However, the semicolon is rarely used in programming, since it is not a standard part of Horn clause logic.

Basic data structures are terms like parent(X, Z) or successor(successor(0)). Prolog also includes the list as a basic data structure. A Prolog list is written using square brackets (like ML and Haskell, with the list consisting of items x, y, and z written as [x,y,z]. Lists may contain terms or variables.

It is also possible to specify the head and tail of a list using a vertical bar. For example, [H|T] means that H is the first item in the list and T is the tail of the list. As in ML and Haskell, this type of notation can be used to extract the components of a list via pattern matching. Thus, if [H|T] = [1,2,3], then H = 1 and T = [2,3]. It is also possible to write as many terms as one wishes before the bar. For example, [X,Y|Z] = [1,2,3] gives X = 1, Y = 2, and Z = [3]. The empty list is denoted by [] and does not have a first element.

Prolog has a number of standard predicates that are always built in, such as not, =, and the I/O operations read, write, and nl (for newline). One anomaly in Prolog is that the less than or equal to operator is usually written =< instead of <= (perhaps because the latter is too easily confused with implication).

# 4.4.2 Execution in Prolog

Prolog compilers exist, but most systems are run as interpreters. A Prolog program consists of a set of Horn clauses in Prolog syntax, which is usually entered from a file and stored in a dynamically maintained database of clauses. Once a set of clauses has been entered into the database, goals can be entered either from a file or from the keyboard to begin execution. Thus, once a Prolog system has begun to execute, it will provide the user with a prompt for a query, such as

```
?-
```