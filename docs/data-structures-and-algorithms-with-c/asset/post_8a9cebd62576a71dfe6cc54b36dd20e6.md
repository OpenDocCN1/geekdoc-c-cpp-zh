
## ANALYSIS OF ALGORITHM

> "Programming is the art of telling another human being what one wants the computer to do". – Donald Knuth

An algorithm is a well-defined computational procedure that transforms inputs into outputs achieving the desired input-output relationship. We must design a process to solve a specific problem before programming. This process must be formulated as a detailed sequence of basic steps, which is called an algorithm. An algorithm can perform the calculation, data processing and automated reasoning task in a finite time.

- Algorithm
- Types of Algorithm
- Time Complexity
- Space Complexity
- Asymptotic Notations

The word «algorithm» is a Persian word algorism derived from the name of the Persian author and great mathematician «Abu Abd Allah Jafar Mohammad bin Musa al Khowarizmi» (Born in 780 A.D. in Baghdad). He worked on algebra, geometry, and astronomy. He designs the first algorithm for adding numbers represented in the numerical system.

### ALGORITHM

**Definition:** Algorithm is a finite sequence of instructions/steps, each of which is very elementary that must be followed to solve a problem.

- **Input:** There are some inputs (zero or more quantities), which are externally supplied.
- **Output:** The result (at least one quantity) should be produced after completion of the job to the user.
- **Definiteness:** The instructions should be unique, concise, clear and unambiguous.
- **Finiteness:** The instructions should be relative in nature and should not be of an infinite type. Should be terminated after a finite number of steps.
- **Effectiveness:** Every instruction must be elementary, so that it can be carried out, in principle, by a person using only pencil and paper. Repetition of same steps should be avoided. It must be feasible.

### Types of Algorithms

Algorithms that use a similar problem-solving approach can be grouped together. This classification scheme is neither exhaustive nor disjoint. The purpose of this classification is to highlight the various ways in which a problem can be solved. Using different techniques, one can develop many algorithms for the same problem. These techniques are not only applicable in Computer Science but also to other fields such as Operation Research, Electrical Engineering etc. We can formulate/develop a good algorithm by studying all the techniques.

### Algorithm types we will consider

- Divide and conquer
- Dynamic programming
- Greedy Method
- Backtracking
- Branch and Bound
- Serial or parallel or distributed algorithm
- Deterministic or non-deterministic algorithm

### Algorithm Development Life Cycle

In the life cycle of an algorithm for the development of an algorithm, the following phases are involved:

- i) Algorithm design / Design Phase
- ii) Writing Phase
- iii) Testing / Experiment Phase
- iv) Analysis of Algorithm / Analysing Phase

### Algorithm Design

Algorithmic design patterns, which provide general techniques for designing algorithms, including divide-and-conquer, dynamic programming, greedy method, backtracking, and branch-and-bound. In the design phase of an algorithm, one of the algorithmic design techniques and the data structure is used.

### Writing Phase

An algorithm generally is written in a modular approach. An algorithm may have the following structures or steps:

Input Step, Initialization Step, Assignment Step, Decision Step, Repetition Step and Output Step.

To make each and every step clear in the algorithm, comments are written whenever necessary.

An algorithm is written using the following basic methods:

- Sequential: Steps are performed sequentially.
- Selection/Decision: One of the several alternative actions is selected.
- Repetition: One or more than one step(s) are performed repeatedly.

The following example describes a formal representation of an algorithm that converts temperature from Celsius to Fahrenheit.

### Algorithm to convert temperature from Celsius to Fahrenheit.

```
Algorithm: Convert(C, F)
[The variable C is used as Celsius value and F is used as Fahrenheit value]
1. Read C
2. Set F = 1.8 * C + 32
3. Print F
4. Return
```

The following algorithm calculates the summation of N natural numbers. First, we have to read the value of N.

### Algorithm to calculate the sum of N natural numbers.

```
Algorithm: Sum (N)
[The variable N is represented the number of natural numbers.]
1. Set S = 0 and I = 1
2. Read N
3. S = S + I
4. I = I + 1
5. If I<=N Goto Step 3
6. Print S
7. Return
```

Searching refers to the operation of finding the location of any element in the array. The search is successful if the item is found; otherwise, it is unsuccessful. Linear search is a method where the search starts from the beginning of the array until the desired key is found or the end of the array is reached.

### Algorithm of Linear search.

```
Algorithm: Linear_Search (A, N, Key)
[An array A with N elements and an item Key are given. This algorithm searches the location of the Key in the array A]
1. Set I = 1
2. Repeat Steps 3 while I <= N and A[I] != Key
3. I = I + 1
   [End of while]
4. If I <= N then
   Print: Item found at location I
   Else
   Print: Item not found
   [End of IF]
5. Return
```

### Testing Phase

After writing an algorithm, it is necessary to check whether the algorithm is correct or not. One must perform each step using paper and pencil by some required valid input, use the algorithm and get the required output in a finite time. Testing or Experiment is another step in the development of the algorithm. When any error is found, then go back to the algorithm design phase and redesign the algorithm.

### Analysis of Algorithms

Algorithms are to be analysed to compute the objective criteria for different input size before actual implementation. Suppose P is a problem and A & B are two different algorithms to solve the problem P. There must have some performance measurement system to decide that which algorithm is better than the other.

Suppose M is an algorithm and n is the size of the input data. The time and space used by the algorithm M are two main measures for the efficiency of M.

The complexity of an algorithm M is the function f (n) which gives the running time and/or storage space requirement of the algorithm in terms of the size n of the input data.

There are some qualitative aspects of algorithms, e.g., simplicity, readability, modularity, modifiability, well documented, etc. However, based on these, there can only be some subjective judgment about algorithms. Moreover, the objective criteria for the qualities of an algorithm are the amount of memory used and execution time.

Therefore, the performance of the algorithm can be measured on the scales of time and space. Time means, we are looking for the fastest algorithm for the problem. Space means we are looking for an algorithm that consumes or needs minimum memory space for its execution.

When performance is measured in terms of space, it is known as space complexity and when performance is measured in terms of time, it is termed as time complexity.

There are two kinds of analysis of algorithm may be possible:

- i) Apriori Analysis
- ii) Posteriori Analysis

### Theoretical / Apriori Analysis

Apriori meaning “from the earlier”. It is on a theoretical basis, independent of programming languages and machine structures. Here, we do analysis (space and time) of an algorithm prior to running it on a specific system. That means we can determine time and space complexity of an algorithm of getting the algorithm rather than running it on a particular system (with different processor and compiler). The stress is laid on the frequency of execution of statements in the algorithm.

### Empirical / Posteriori Analysis

Posteriori means “from the latter”. The actual amount of space and time taken by the algorithms are recorded during execution. It is dependent on the programming language used and machine structure. Here, we do an analysis of the algorithm only after running it on the system. It directly depends on the system and changes from system to system.

In real-life, we cannot do posteriori analysis as software is generally made for an anonymous user, which runs it on a system different from those present in the industry. Therefore, in Apriori analysis, we use asymptotic notations to determine time and space complexity as they change from computer to computer but asymptotically they are same

### Space Complexity

The space complexity is the amount of space (memory) is needed for an algorithm to solve the problem. An efficient algorithm takes space as small as possible.

Space needed by a program is the sum of the following components:

- 1. Instruction space: Space needed to store the executable version of the program and it is fixed.
- 2. Data Space: Space needed to store all constants, variable values and has further following components.
  - a) Space needed by constants and simple variables. This space is fixed.
  - b) Space needed by fixed sized structured variables, such as arrays and structure.
  - c) Dynamically allocated space from memory pool called heap. This space usually varies.
- 3. In-built stack space: Space needed to store the information needed to resume the suspended functions. Each time a function, the following data is saved on the in-built stack.
