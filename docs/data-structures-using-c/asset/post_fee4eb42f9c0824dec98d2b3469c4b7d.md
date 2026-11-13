
program to create an array of specified size for storing marks of 60 students in the class. Use STL algorithm ‘count’ and compute the total number of failures in the subject.

and update the information. Write a program that uses list from STL to implement the same. Use iterator.

- 9. The students’ club members (MemberID, name, phone, email) list is to be maintained. The common operations performed include these: add member, search member, delete member,

- 10. Implement double-ended queue using STL. Use it for processing members queue of jobs submitted to printer. Make use of deque for stacking the members and process them as LIFO.

## Answers to multiple choice questions

- 1. (b)
- 2. (c)
- 3. (d)
- 4. (d)

## 16 ALGORITHM ANALYSIS AND DESIGN

### OBJECTIVES

After completing this chapter, the reader will be able to understand the following:

- Basic tools needed to develop and analyse algorithms
- Methods to compute the efficiency of algorithms
- Ways to make a wise choice among many solutions for a given problem

The study of algorithms is fundamental to computer science. An algorithm can be defined as a set of steps to solve a particular problem effectively and efficiently. The study of algorithms includes learning tools for algorithm development, various design strategies, and analysis of algorithms.

The intention of this chapter is to present the foundation for these aspects associated with algorithm study.

### 16.1 INTRODUCTION

We have discussed data structures, programming languages, algorithms, and their analysis in Chapter 1. Software development desires to utilize each of these efficiently. The basic programming style influenced by typical design approaches called algorithmic strategies. An algorithmic strategy (also known as design technique or paradigm) is a general approach to solving problems algorithmically. This methodology is appropriate for various problems suitable for different areas of computing.

It is true that devising an algorithm is an art that may never be fully automated. We shall study various design techniques that have proven to be useful to devise new algorithms. Dynamic programming is one such technique along with others such as divide-and-conquer, greedy, and backtracking.

More than one technique may be applicable to a specific problem, but it is often the case that an algorithm constructed using a particular approach is clearly superior to equivalent solutions built using alternative techniques. Hence, the choice of the design paradigm is an important feature of algorithm synthesis.

### 16.1.1 Algorithm Analysis

In computer science, an algorithm is a way to formulate a stepwise solution to a problem. It outlines the initial conditions, processing steps/sequence, and final outcome of the problem. For any specific problem definition, more than one solution approach may exist. In other words, a problem can have multiple algorithms for its solution. If multiple algorithms provide solutions to the same problem, their performance will surely vary over a wide range of performance measuring parameters.

In practice, each algorithm's performance is unique. Each algorithm's way of solving a problem, its prerequisites, and presentation of the final solution is independent. Thus, suitability to each algorithm for problem solving varies from application to application. To measure the performance of each algorithm, we need analysis, and based on the appropriate analysis design, selection of efficient or better algorithms is possible. Hence, the study of algorithms and their analysis plays a vital role in software development.

The performance measuring parameters have been highlighted in Chapter 1. We can evaluate an algorithm's efficiency in terms of its time and space consumption. These parameters are measured in terms of asymptotic complexity bounds of the algorithms. Let us discuss a few fundamental algorithmic strategies in relation with asymptotic complexities in the following sections.

### 16.1.2 Asymptotic Notations (Ω, θ, O)

More than one solution may exist for a single problem. To identify the best among them, we need to quantify their performances with factors such as time and space complexities. Asymptotic complexity helps us to quantify the performance of the algorithms. Big O, omega (Ω), and theta (θ) are the asymptotic notations used in this algorithmic analysis.

### Big O or Oh

### Definition

The function f(n) = O(g(n)) is called ‘f(n) is the big O of g(n)’ if and only if there exist positive constants c and N, such that f(n) <= c * g(n) for all n >= N.

Big O formally represents the upper bound of the algorithm's time complexity as it suggests the maximum value or upper limit of the time taken by an algorithm to execute.

If an algorithm's time complexity is represented as O(g(n)), then it indicates that in all possible data considerations of size n, at any instance, the algorithm would consume f(n) time, which is always less than constant c times g(n).

Let us consider an example of linear search. Linear search will consume maximum time if the element we want to search for, say x, lies either at the last location or is absent. In such situations, linear search will take n comparisons, where n is the data size. So, in the case of linear search, the upper limit for time complexity will be n in the worst possible situation. This is represented as O(n).

### Big Omega (Ω)

Definition The function f(n) = Ω(g(n)) is called 'f(n) is omega of g(n)' if and only if there exist positive constants c and N such that f(n) ≥ c × g(n) for all n ≥ N.

### Big Theta (Θ)

Definition The function f(n) = Θ(g(n)) is called 'f(n) is theta of g(n)', if and only if there exist positive constants c and N such that f(n) ≤ c × g(n) for n ≥ N.

Algorithms can be iterative or recursive; can make decisions randomly or approximately; can propagate the decision-making policies in the forward or backward manner. The algorithmic strategies work on all such characteristics and are broadly classified as follows:

- 1. Divide-and-conquer
- 2. Greedy method
- 3. Dynamic programming

The study of algorithm and design strategies

- 1. makes available templates suitable for solving a set of diverse problems;
- 2. can be translated into common control and data structures provided by most high-level languages;
- 3. analyses the temporal and spatial requirements of the algorithms in a precise manner.

### 16.2 DIVIDE-AND-CONQUER

Divide-and-conquer is one of the most popular algorithmic strategies. It works in two phases. In the first phase, the problem is divided into subproblems of smaller size till each problem can be easily solved. In the latter phase, the solutions to all such subproblems are gathered together to get the final solution. This approach, especially when used recursively, often yields efficient solutions to problems in which the subproblems are smaller versions of the original problem and can be independently solved.

Often, even the subproblems are relatively large, and the divide-and-conquer strategy is reapplied. In addition, the subproblems resulting from a divide-and-conquer design are of the same type as the original problem. For those cases, applying this design again is naturally expressed by a recursive procedure. The process of splitting the input into distinct subsets continues till these smaller subproblems, which are of the same kind, are small enough to be solved without further splitting.

### 16.2.1 Unique Characteristics and Use

Popularly, the divide-and-conquer strategy is designed keeping in mind a single processor computer. However, it is ideally suited for parallel computations as each subproblem can be solved simultaneously by its own processor. The following are some unique characteristics of the divide-and-conquer method:

- 1. The divide-and-conquer technique is well suited when a data set can be divided into smaller subsets of data elements and each data set can be independently processed.
