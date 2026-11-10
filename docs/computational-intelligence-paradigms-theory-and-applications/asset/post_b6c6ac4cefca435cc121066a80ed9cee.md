
![](img/d9a4cc12c48f7466f309cbd3c4549c73_620_0.png)

**FIGURE 14.1:** Main Loop of Genetic Programming

![](img/d9a4cc12c48f7466f309cbd3c4549c73_620_1.png)

**FIGURE 14.2:** Basic Tree-Like Program Representation Used in Genetic Programming

Lisp programming is required to understand the representations and programming of genetic programming. A brief description about Lisp programming is discussed in Section 14.3. In prefix notation, functions always precede their arguments. In this notation, it is easy to see the correspondence between expressions and their syntax trees. Simple recursive procedures can convert prefix-notation expressions into infix-notation expressions and vice versa.

## 14.2 Growth of Genetic Programming

The emergence of Genetic Programming started with the utilization of evolutionary algorithms by Nils Aall Barricelli in 1954. The application demanded evolutionary simulations and evolutionary algorithms which were widely accepted as standard optimization methods with reference to the work of Ingo Rechenberg in the 1960s and early 1970s. His team was capable of solving complex engineering problems through evolution strategies. In addition to Rechenberg’s work, John Holland’s work was the extremely influential one during the early 1970s.

The introductory results on the GP methodology were described by Stephen F. Smith in 1980. Later during 1981 Forsyth reported the evolution of small programs in forensic science for the UK police. The initial statement of modern Genetic Programming stating that, “GP are procedural languages coordinated in tree-based structures and functioned by suitably defined GA-operators”, was contributed by Michael L. Cramer in 1985, and independently by Jürgen Schmidhuber in 1987. Based on these works, John R. Koza, a primary proponent of GP, initiated the practical application of genetic programming in several complex optimization and search problems. It ought to be noted that Koza states GP as a generalization of genetic algorithms rather than a specialization.

GP is computationally more intensive and therefore in the 1990s it was primarily employed to work out fundamental elementary problems. Recently due to the exponential growth in CPU power, GP has produced numerous novel and more prominent results in fields such as quantum computing, electronic design, game playing, sorting, searching, and many others. These consequences admit the replication or growth of several post-year-2000 inventions. GP has also been employed to evolvable hardware in addition to computer programs. Initially, formulating a hypothesis for GP has been really difficult and so in the 1990s GP was considered a sort of outcast among search techniques. Just afterwards, a series of breakthroughs occurred in the early 2000s, the theory of GP has had an impressive and fast development, therefore it has been feasible to build precise probabilistic models of GP.

## 14.3 The Lisp Programming Language

During the late 1950s, a family of programming languages named as Lisp was framed by John McCarthy. The basic computation mechanism of Lisp programs is recursion. The language is implemented to support a wide range of platforms. Based on the computer available, the user can execute Lisp in several methods. Likewise there are a few minimal modifications between the LISP interpreters. The two basic types of data structures available in Lisp are the atom and the list. Atoms can be either symbols or numbers. Lists are linked lists where the elements of the list are either atoms or other lists. Lists of atoms are written as follows:

(1 B D 5)

Nested list structures (lists with lists as elements) are written as follows:

(A (1 2) D (4 (6 G)))

This example is a list of four elements. The first is the atom A; the second is the sublist (1 2); the third is the atom D, and the fourth is the sublist (4 (6 G)). Internally, lists are usually represented as single-linked lists. Each node of the list consists of two pointers. The first pointer points either to the corresponding atom or to the corresponding sublist. The second pointer points to the next node in the list.

Pure Lisp is a functional programming language. In a functional program is computed by application of functions to arguments. Parameters such as symbols, numbers, or other function calls can be used as arguments. There is no need of assignment statements or variables for computation. Thus, a Lisp program is just a collection of functions that can call each other. Functions in Lisp are represented in the same way as data, namely as nested list structures. Here is a function that squares its argument x:

```lisp
(defun square (x) (* x x))
```

The defun can be thought of as a key word that indicates that a function definition follows. The name of the function is square. Then follows a list of arguments (dummy parameters). Finally is the body of the function. The function returns the value resulting from multiplying x times x.

Here is a slightly more complex example that uses the function square:

```lisp
(defun hypotenuse (a b)
  (sqrt (+ (square a) (square b))))
```

The function to find the length is defined as:

```lisp
(defun list-length (x)
  (if (null x)
      0
      (+ 1 (length (rest x)))))
```

If the list is null (i. e., empty), then the length is 0. Otherwise, the length is 1 plus the length of the list with the first element removed. Since Lisp functions are stored as data, it is very easy to write functions that define and manipulate other functions. This is exactly what genetic programming does. It is relatively easy to write a simple genetic programming package in Lisp.

## 14.4 Functionality of Genetic Programming

The operational steps such as creating an individual, creating a random population, fitness test, functions and terminals, the genetic operations, selection functions, crossover operation, mutation and user decisions of a typical genetic programming are described in this section (Figure 14.3).

### 14.4.1 Generation of an Individual and Population

The basic elements of an individual are its genes. These genes are combined together to form a program. An individual’s program is a tree-like structure and as such there are two types of genes: *functions* and *terminals*.

Terminals are defined as leaves or nodes without branches and functions are defined as the nodes with children. The node’s children provide the arguments for the function. In the example (Figure 14.4) there are three functions (−, + and /) and four terminals (x, 3, y and 6). The / (division) function requires two arguments: the return value of “−” and the return value of the subtree whose root is “+”. The − (subtraction) function takes two arguments which are provided by x and 3. The + (addition) function also takes two arguments which are provided by y and 6.

![](img/d9a4cc12c48f7466f309cbd3c4549c73_624_0.png)

**FIGURE 14.3:** Functionality of Genetic Programming

The example may be interpreted as (x−3)/(y+6). The genes that will be available to the GP system must be selected or created by the user. This is an important decision as poor selection may well render the system incapable of evolving a solution.

### 14.4.2 Creating a Random Population

Once the genes are chosen, a random population is created. To create random population there are three basic techniques such as grow, full, and ramped-half-and-half:

- 2. All functions have a number (equal to the arity of the function) of child nodes appended, and the algorithm starts again. Thus, only if d is specified as one, could this method produce a one-node tree.

### Ramped-half-and-half

This technique was used by Koza. To increase the variation in structure both grow and full methods can be used in creating the population—this technique, ramped-half-and-half, is the sole method. Only a maximum depth, md, is specified but the method generates a population with a good range of randomly sized and randomly structured individuals.

- 1. The population is evenly divided into parts: a total of md-1.
- 2. One half of the population is produced by the grow method and the other half is produced using the full method. For the first part, the argument for the grow method, m, and the argument for the full method, is d. This continues to part md-1, where the number md is used. Thus a population is created with good variation, utilizing both grow and full methods.

### 14.4.3 Fitness Test

After the initial random population has been created, the individuals are required to be evaluated for their fitness. Evaluating the fitness function of a program requires how well a program performs into a numerical value. Generally, this requires executing the program several times with different parameters, and evaluating the output each time.

### 14.4.4 Functions and Terminals

The most important components of genetic programming are the terminal and function sets. All the variables and constants defined by the user are contained in the terminal set while all the functions and subroutines are in the function set. The functions can be any mathematical functions, such as addition, subtraction, division, multiplication, and other more complex functions.

### 14.4.5 The Genetic Operations

The evolutionary process starts, as soon as the fitness test to all the individuals in the initial random population is completed. The individuals in the new population are formed by genetic operators like reproduction, crossover, and selection. Whenever a new population is created, the old population is destroyed.
