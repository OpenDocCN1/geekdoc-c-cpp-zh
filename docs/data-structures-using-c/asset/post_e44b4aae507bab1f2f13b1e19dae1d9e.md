
m = size of the string parameter of the operation
d = alphabet size

Another example is shown in Fig. 16.8.

![](img/a99ec79093c067f0bed8f1086197950e_767_0.png)

Fig. 16.8 Another example of standard trie

### 16.6.2 Compressed Tries

Similar to the standard trie, a compressed trie (Fig. 16.9) is a tree-based data structure for storing strings in order to make pattern matching much faster. This is an optimized approach for pattern matching specially suitable for applications where time is a more crucial factor. Following are the unique characteristics of compressed trie:

- 1. A compressed trie (or Patricia trie) has internal nodes of degree at least 2.
- 2. It is obtained from standard trie by compressing chains of redundant nodes.

![](img/a99ec79093c067f0bed8f1086197950e_767_1.png)

Fig. 16.9 Compressed trie

### 16.6.3 Suffix Tries

A suffix trie is a compressed trie for all the suffixes of a text. This is a compressed trie, and hence, possesses all features a compressed trie and makes it more powerful for making a search faster as it includes all suffixes of a text. Let us consider an example as in Fig. 16.10.

![](img/a99ec79093c067f0bed8f1086197950e_768_0.png)

## RECAPITULATION

- Algorithms are used as design tools for solving real world problems.
- Asymptotic notation helps us to define lower and upper bounds of time complexity.
- Commonly used algorithm strategies are divide-and-conquer, greedy method, and dynamic programming, each strategy has a set of unique characteristics.
- Control abstraction is a procedure that mirrors the way an actual problem based on the said strategy will look like.
- Dynamic programming is an algorithm design method that can be used when the solution to a problem may be viewed as the result of a sequence of decisions.
- Pattern matching can be defined as the process of finding the presence of a particular string (pattern) from the given string (text).
- A trie is a tree-based data structure for storing strings to make the pattern matching faster. A trie helps in pattern matching in time that is proportional to the length of the pattern.

## KEY TERMS

**Asymptotic analysis** In computer science, the analysis of algorithms considers the performance of algorithms when applied to very large datasets. Asymptotic complexity helps us quantify the performance measures of an algorithm.

**Divide-and-conquer method** This method is an algorithm design paradigm in which a problem is broken down into two or more subproblems of the same type, which are then solved independently. These solutions are then combined to provide a solution to the parent problem.

**Dynamic programming** Dynamic programming is well suited to problems where a recursive algorithm would solve many of the subproblems repeatedly. The dynamic programming algorithm stores results, or solutions, for small subproblems. Later on, it uses these stored solutions instead of recomputing them to solve larger subproblems.

**Greedy method** Greedy method is defined as an algorithm paradigm that follows the problem-solving heuristic of making the locally optimal choice at each stage with the hope of finding the optimum solution.

**Pattern matching** It is the process of finding the presence of a particular string (pattern) from a given string (text).

**Trie** A trie is a tree-based data structure for storing strings to make pattern matching faster. It helps in pattern matching in time that is proportional to the length of pattern. It is useful in performing prefix query for information retrieval.

## EXERCISES

### Multiple choice questions

- 1. Which of the following algorithm design techniques is used in quicksort algorithm?
- (a) Dynamic programming
- (b) Backtracking
- (c) Divide-and-conquer
- (d) Greedy

- 2. Merge sort uses
- (a) triangulization
- (b) quicksort
- (c) n-queens
- (d) heuristics

- 3. Dynamic programming is based on the principle of
- (a) optimality
- (b) heuristics
- (c) regularity
- (d) none of the above

- 4. The complexity function of which of the following strategies is generally in the form of a recurrence relation?
- (a) Dynamic
- (b) Divide-and-conquer
- (c) Both (a) and (b)
- (d) None of the above

- 5. Time complexity of ternary search is
- (a) log n
- (b) log2 3
- (c) log3 n

- 6. Time complexity is
- (a) the space required by a program
- (b) an amount of machine time necessary for running a program
- (c) the time required for a programmer to code a program
- (d) all of the above

- 7. The worst case complexity is (for instance, of size n)
- (a) a function defined by maximum number of steps taken
- (b) a function defined by average number of steps taken
- (c) a function defined by minimum number of steps taken
- (d) all of the above

- 8. The best case complexity (for instance, of size n) is
- (a) a function defined by maximum number of steps taken
- (b) a function defined by average number of steps taken
- (c) a function defined by minimum number of steps taken
- (d) all of the above

### Review questions

- 1. What is an algorithm? Write the essential properties and the performance measures of an algorithm.

- 2. Explain the characteristics and uses of greedy and dynamic programming algorithmic strategies.

- 3. What is big O notation? Arrange the following functions by growth value: \(N, \sqrt{N}, N^2, NlogN, N \log_2 N, N^2, 2^N\)

- 4. Write a C program for binary search and compute its time complexity.

- 5. Write a C program for ternary search and compute its time complexity.

- 6. What do you mean by best case, average case, and worst case, and worst case time complexity? Give suitable examples.

- 7. Find the frequency count of the following programs:
  (a) for(i = 1; i <= n; i++)
      for(j = 1; j <= i; j++)
          x = x + 1;
  (b) i = 1;
      while(i <= n)
      {
          x = x + 1;
          i = i + 1;
      }

- 8. Find the frequency count of the following programs:
  (a) for(i = 1; i <= n; i++)
      for(j = 1; j <= n; j++)
          a = a + 2;
  (b) i = 1;
      do {
          x = x + 2;
          i++;
      } while(i <= n);
  (c) for i = 1 to n do
      for j = i + 1 to n do
          for k = j + 1 to n do
              x = x + 1;
  (d) i = 1
      do
      {
          x++;
          if(i == 10)
              break;
          i++;
      } while(i <= n);

- 9. Write the control abstraction for the following algorithm strategies:
  (a) Divide-and-conquer
  (b) Greedy method
  (c) Dynamic programming

- 10. Compare greedy and dynamic strategies.

- 11. Give typical applications in which the divide-and-conquer is the best suitable algorithmic strategy.

- 12. Describe each of the following with respect to their unique characteristics, control abstraction, and an example:
  (a) Divide-and-conquer
  (b) Dynamic
  (c) Greedy

- 13. Write a quicksort algorithm. Analyse the same with respect to time complexity.

- Answers to multiple choice questions
- 1. (c) 2. (c) 3. (a) 4. (c) 5. (a) 6. (b) 7. (a) 8. (c)

## FEATURES OF THE BOOK

- **OBJECTIVES**
- After completing this chapter, the reader will be able to understand the following:
- • The power of recursion and its working
- • Identification of the base case and the general case of a recursively defined problem
- • Comparison of iterative and recursive solutions
- • The study of the importance of base and debug recursive functions
- • The method of implementing recursion using stacks

**Objectives**

Each chapter begins with a list of topics that the readers can expect to learn from that chapter.

**Algorithms**

All chapters contain plenty of algorithms to support the theoretical concepts. Each algorithm is depicted in a step-wise manner along with a description of its function and significance.

```
**ALGORITHM 4.2**
An iterative version of the algorithm to compute the factorial of a number.
1. start
2. Let n be the number whose factorial is to be computed and let Factorial = 1
3. for I = 1 to n do begin Factorial = Factorial * I end end
4. stop
```

**PROGRAM CODE 4.1**

```cpp
int Factorial(int n)
{
if(n == 1) // end condition
return 1;
else
return Factorial(n - 1) * n;
}
```

**Program Codes**

Numerous program codes in C++ provide implementation of the concepts. Comments are provided wherever necessary thus making the code self-explanatory and easy to understand.

**Flowcharts**

Flowcharts are provided wherever required. They provide readers with a step-wise and clear representation of algorithms and concepts.

![](img/a99ec79093c067f0bed8f1086197950e_771_0.png)
