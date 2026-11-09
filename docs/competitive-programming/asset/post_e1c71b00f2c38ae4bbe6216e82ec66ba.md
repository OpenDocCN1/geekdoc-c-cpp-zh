
## 1.2 Tips to Be Competitive

The goal is not just to map problems into categories as in Table 1.1. After you are familiar with most of the topics in this book, you can classify the problems into just four types as in Table 1.3.

**Table 1.3: Problem Types (Compact Form)**

| No | Category | Confidence and Expected Solving Speed |
|---|---|---|
| A. | I have solved this type before | Confident that I can solve it again now (and fast) |
| B. | I have solved this type before | But I know coding the solution takes time |
| C. | I have seen this type before | But that time I have not or cannot solve it |
| D. | I have not seen this type before | I may or may not be able to solve it now |

To be competitive, you must frequently classify the problems that you read in the problem set into type A (or at least type B).

### 1.2.2 Tip 2: Do Algorithm Analysis

Once you have designed an algorithm to solve a particular problem in a programming contest, you must now ask this question: Given the maximum input bound (usually given in a good problem description), can the currently developed algorithm, with its time/space complexity, pass the time/memory limit given for that particular problem?

Sometimes, there are more than one way to attack a problem. However, some of them may be incorrect and some of them are not fast enough... The rule of thumb is: Brainstorm many possible algorithms - then pick the **simplest that works** (fast enough to pass the time and memory limit, yet still produce correct answer!).

For example, the maximum size of input n is 100K, or 10⁵ (1K = 1,000), and your algorithm is of order O(n²). Your common sense told you that (100K)² is an extremely big number, it is 10¹⁰. So, you will try to devise a faster (and correct) algorithm to solve the problem, say of order O(n log₂ n). Now 10⁵ log₂ 10⁵ is just 1.7 × 10⁶ ... Since computers nowadays are quite fast and can process up to order 1M, or 10⁶ (1M = 1,000,000) operations in seconds, your common sense told you that this one is likely able to pass the time limit.

Now how about this scenario. You can only devise an algorithm of order O(n⁴). Seems pretty bad right? But if n ≤ 10... then you are done. Just directly implement your O(n⁴) algorithm since 10⁴ is just 10K and your algorithm will only use relatively small computation time.

So, by analyzing the complexity of your algorithm with the given input bound and stated time/memory limit, you can do a better job of judging whether you should try coding your algorithm (which will take your time, especially in the time-constrained ICPCs and IOIs), or attempt to improve your algorithm first or switch to other problems in the problem set.

In this book, we will not discuss the concept of algorithm analysis. We assume that you have this basic skill. Please check this reference book: “Introduction to Algorithms” [4] and make sure you understand how to:

- Prove correctness of an algorithm (especially for Greedy algorithms, see Section 3.3).
- Analyze time/space complexity for iterative and recursive algorithms.
- Perform amortized analysis (see [4], Chapter 17) – although rarely used in contests.
- Do output-sensitive analysis, to analyze algorithms which depend on output size, example: the O(|Q| + occ) complexity for finding an exact string matching of query string Q with help of Suffix Tree (see Section 6.4).

Many novice programmers usually skip this phase and are tempted to directly code the first algorithm that they can think of (usually the naïve version), and then they end up realizing that the chosen data structure is not efficient or their algorithm is not fast enough (or wrong). **Our advice: refrain from coding until you are sure that your algorithm is both correct and fast enough.**

To help you in judging how fast is ‘enough’, we produce Table 1.4. Variants of such Table 1.4 can also be found in many algorithm books. However, we put another one here from programming contest perspective. Usually, the input size constraints are given in the problem description. Using the logical assumptions that a typical year 2010 CPU can do 1M operations in 1s and time limit of 3s (typical time limit used in most UVA online judge [17] problems), we can predict the ‘worst’ algorithm that can still pass the time limit. Usually, the simplest algorithm has poor time complexity, but if it can already pass the time limit, just use it!

| $n$ | Worst AC Algorithm | Comment |
|---|---|---|
| $\le 10$ | $O(n!), O(n^6)$ | e.g. Enumerating a Permutation |
| $\le 20$ | $O(2^n), O(n^5)$ | e.g. DP + Bitmask Technique |
| $\le 50$ | $O(n^4)$ | e.g. DP with 3 dimensions + $O(n)$ loop, choosing $\binom{n}{k=4}$ |
| $\le 100$ | $O(n^3)$ | e.g. Floyd Warshall's |
| $\le 1K$ | $O(n^2)$ | e.g. Bubble/Selection/Insertion Sort |
| $\le 100K$ | $O(n\log_2 n)$ | e.g. Merge Sort, Building Segment Tree |
| $\le 1M$ | $O(n), O(\log_2 n), O(1)$ | Usually, contest problem has $n < 1M$ (e.g. to read input) |

Table 1.4: Rule of Thumb for the ‘Worst AC Algorithm’ for various input size $n$ (single test case only), assuming that a year 2010 CPU can compute 1M items in 1s and Time Limit of 3s.

Additionally, we have a few other rules of thumb:

- $2^{10} \approx 10^3$, $2^{20} \approx 10^6$.
- Max 32-bit signed integer: $2^{31}-1 \approx 2 \times 10^9$ (or up to $\approx 9$ decimal digits);  
  Max 64-bit signed integer (long long) is $2^{63}-1 \approx 9 \times 10^{18}$ (or up to $\approx 18$ decimal digits).  
  Use ‘unsigned’ if slightly higher positive number is needed $[0 \ldots 2^{64}-1]$.  
  If you need to store integers $\ge 2^{64}$, you need to use the Big Integer technique (Section 5.4).
- Program with nested loops of depth $k$ running about $n$ iterations each has $O(n^k)$ complexity.
- If your program is recursive with $b$ recursive calls per level and has $L$ levels, the program has roughly $O(b^L)$ complexity. But this is an upper bound. The actual complexity depends on what actions are done per level and whether some pruning is possible.
- Dynamic Programming algorithms which fill a 2-D matrix in $O(k)$ per cell are in $O(k \times n^2)$.
- The best time complexity of a comparison-based sorting algorithm is $\Omega(n\log_2 n)$.
- Most of the time, $O(n\log_2 n)$ algorithms will be sufficient for most contest problems.

As an exercise for this section, please answer the following questions:

- 1. There are \(n\) webpages \(1 \leq n \leq 10M\). Each webpage \(i\) has different page rank \(r_i\). You want to pick top 10 pages with highest page ranks. Which method is more feasible?
  - (a) Load all \(n\) webpages’ page rank to memory, sort (Section 2.2.1), and pick top 10.
  - (b) Use priority queue data structure (heap) (Section 2.2.2).

- 2. Given a list L of up to \(10K\) integers, you want to frequently ask the value of \(\operatorname{sum}(i,j)\), i.e. the sum of L[i] + L[i+1] + ... + L[j]. Which data structure should you use?
  - (a) Simple Array (Section 2.2.1).
  - (b) Balanced Binary Search Tree (Section 2.2.2).
  - (c) Hash Table (Section 2.2.2).
  - (d) Segment Tree (Section 2.3.3).
  - (e) Suffix Tree (Section 6.4).
  - (f) Simple Array that is pre-processed with Dynamic Programming (Section 2.2.1 & 3.4).

- 3. You have to compute the ‘shortest path’ between two vertices on a weighted Directed Acyclic Graph (DAG) with \(|V|, |E| \leq 100K\). Which algorithm(s) can be used?
  - (a) Dynamic Programming + Topological Sort (Section 3.4, 4.2, & 4.9.2).
  - (b) Breadth First Search (Section 4.3).
  - (c) Dijkstra’s (Section 4.5).
  - (d) Bellman Ford’s (Section 4.6).
  - (e) Floyd Warshall’s (Section 4.7).

- 4. Which algorithm is faster (based on its time complexity) for producing a list of the first \(10K\) prime numbers? (Section 5.3.1)
  - (a) Sieve of Eratosthenes (Section 5.3.1).
  - (b) For each number \(i \in [1 - 10K]\), test if \(i\) is a prime with prime testing function.

### 1.2.3 Tip 3: Master Programming Languages

There are several programming languages allowed in ICPC, including C/C++ and Java. Which one should we master? Our experience gives us the following answer: although we prefer C++ with built-in Standard Template Library (STL), we still need to master Java, albeit slower, since this language has a powerful BigInteger, String Processing, and GregorianCalendar API. Simple illustration is shown below (part of the solution for UVa problem 623: 500!):

Compute 25! (factorial of 25). The answer is very large: 15,511,210,043,330,985,984,000,000.

This is way beyond the largest built-in data structure (unsigned long long: \(2^{64} - 1\)) in C/C++. Using C/C++, you will have a hard time coding this simple problem as there is no native support for Big Integer data structure in C/C++ yet. Meanwhile, the Java code is simply this:

