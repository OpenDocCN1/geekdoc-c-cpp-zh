

(c) 如果本问题中描述的条件存在，这对 P = NP 的问题意味着什么？

## 17.13

这里是背包问题的另一个版本，我们称之为 EXACT KNAPSACK。给定一组每件物品都有给定整数大小的物品，以及大小为整数 k 的背包，是否存在一组物品恰好装满背包？假设 EXACT KNAPSACK 是 NP-完全的，使用归约论证证明 KNAPSACK 是 NP-完全的。

## 17.14

第 17.2.3 节的最后一段讨论了一种通过在寻找多项式时间解和证明问题 NP-完全之间交替来为新问题开发解决方案的策略。完善第 15.1 节中的“算法设计算法”以纳入识别和处理 NP-完全问题。

## 17.15

证明实数集是不可数的。使用与第 17.3.1 节中证明整数函数集不可数类似的证明。

## 17.16

使用与第 17.3.2 节中给出的类似的归约论证，证明确定任意程序是否会打印任何输出是不可判定的。

## 17.17

使用与第 17.3.2 节中给出的类似的归约论证，证明确定任意程序是否在其程序中执行特定语句是不可判定的。

## 17.18

使用与第 17.3.2 节中给出的类似的归约论证，证明确定两个任意程序是否在完全相同的输入上停机是不可判定的。

## 17.19

使用与第 17.3.2 节中给出的类似的归约论证，证明确定是否存在某个输入使得两个任意程序都会在该输入上停机是不可判定的。

## 17.20

使用与第 17.3.2 节中给出的类似的归约论证，证明确定任意程序是否在所有输入上停机是不可判定的。

## 17.21

使用与第 17.3.2 节中给出的类似的归约论证，证明确定任意程序是否计算指定函数是不可判定的。

## 17.22

考虑一个名为 COMP 的程序，它接受两个字符串作为输入。如果字符串相同，则返回 TRUE。如果字符串不同，则返回 FALSE。为什么我们用来证明停机问题无解程序不存在的论证不能用来证明 COMP 不存在？

## 17.6 项目

## 17.1

实现 VERTEX COVER；即，给定图 G 和整数 k，回答是否存在大小为 k 或更小的顶点覆盖。开始时使用暴力算法检查所有大小为 k 的顶点集合以找到可接受的顶点覆盖，并测量在若干输入图上的运行时间。然后尝试使用你能想到的任何启发式方法来减少运行时间。接下来，尝试以找到形成顶点覆盖的最小顶点集合的意义来寻找该问题的近似解。

- 17.2 实现 KNAPSACK（见第 16.1 节）。测量其在若干输入上的运行时间。对于此问题，最大实际输入大小是多少？
- 17.3 实现 TRAVELING SALESMAN 的近似解；即，给定具有所有边成本的图 G，找到访问 G 中所有顶点的最便宜的环路。尝试各种启发式方法以找到各种输入图的最佳近似解。
- 17.4 编写一个程序，给定正整数 n 作为输入，打印该数的 Collatz 序列。你能对具有长 Collatz 序列的整数类型说些什么？你能对各种类型整数的 Collatz 序列长度说些什么？

## PART VI

## APPENDIX

## 实用函数

以下是本教材中 C++ 示例程序使用的各种实用函数。

```
// Return true iff "x" is even
inline bool EVEN(int x) { return (x % 2) == 0; }
```

```
// Return true iff "x" is odd
inline bool ODD(int x) { return (x % 2) != 0; }
```

```
// Assert: If "val" is false, print a message and terminate the program
// the program
void Assert(bool val, string s) {
	if (!val) { // Assertion failed -- close the program
		cout << "Assertion Failed: " << s << endl;
		exit(-1);
	}
}
```

```
template<typename E>
inline void swap(E A[], int i, int j) {
	E temp = A[i];
	A[i] = A[j];
	A[j] = temp;
}
```

// 随机数生成器函数

```
// Seed the generator
inline void Randomize()
{	srand(1);
}
```

```
// Return a random value in range 0 to n-1
inline int Random(int n)
{	return rand() % (n);
}
```

## 参考文献

[AG06] Ken Arnold and James Gosling. *The Java Programming Language*. Addison-Wesley, Reading, MA, USA, fourth edition, 2006.
[Aha00] Dan Aharoni. Cogito, ergo sum! cognitive processes of students dealing with data structures. In *Proceedings of SIGCSE'00*, pages 26–30, ACM Press, March 2000.
[AHU74] Alfred V. Aho, John E. Hopcroft, and Jeffrey D. Ullman. *The Design and Analysis of Computer Algorithms*. Addison-Wesley, Reading, MA, 1974.
[AHU83] Alfred V. Aho, John E. Hopcroft, and Jeffrey D. Ullman. *Data Structures and Algorithms*. Addison-Wesley, Reading, MA, 1983.
[BB96] G. Brassard and P. Bratley. *Fundamentals of Algorithmics*. Prentice Hall, Upper Saddle River, NJ, 1996.
[Ben75] John Louis Bentley. Multidimensional binary search trees used for associative searching. *Communications of the ACM*, 18(9):509–517, September 1975. ISSN: 0001-0782.
[Ben82] John Louis Bentley. *Writing Efficient Programs*. Prentice Hall, Upper Saddle River, NJ, 1982.
[Ben84] John Louis Bentley. Programming pearls: The back of the envelope. *Communications of the ACM*, 27(3):180–184, March 1984.
[Ben85] John Louis Bentley. Programming pearls: Thanks, heaps. *Communications of the ACM*, 28(3):245–250, March 1985.
[Ben86] John Louis Bentley. Programming pearls: The envelope is back. *Communications of the ACM*, 29(3):176–182, March 1986.
[Ben88] John Bentley. *More Programming Pearls: Confessions of a Coder*. Addison-Wesley, Reading, MA, 1988.
[Ben00] John Bentley. *Programming Pearls*. Addison-Wesley, Reading, MA, second edition, 2000.
[BG00] Sara Baase and Allen Van Gelder. *Computer Algorithms: Introduction to Design & Analysis*. Addison-Wesley, Reading, MA, USA, third edition, 2000.

[BM85] John Louis Bentley and Catherine C. McGeoch. Amortized analysis of self-organizing sequential search heuristics. Communications of the ACM, 28(4):404–411, April 1985.
[Bro95] Frederick P. Brooks. The Mythical Man-Month: Essays on Software Engineering, 25th Anniversary Edition. Addison-Wesley, Reading, MA, 1995.
[BSTW86] John Louis Bentley, Daniel D. Sleator, Robert E. Tarjan, and Victor K. Wei. A locally adaptive data compression scheme. Communications of the ACM, 29(4):320–330, April 1986.
[CLRS09] Thomas H. Cormen, Charles E. Leiserson, Ronald L. Rivest, and Clifford Stein. Introduction to Algorithms. The MIT Press, Cambridge, MA, third edition, 2009.
[Com79] Douglas Comer. The ubiquitous B-tree. Computing Surveys, 11(2):121–137, June 1979.
[DD08] H.M. Deitel and P.J. Deitel. C++ How to Program. Prentice Hall, Upper Saddle River, NJ, sixth edition, 2008.
[ECW92] Vladimir Estivill-Castro and Derick Wood. A survey of adaptive sorting algorithms. Computing Surveys, 24(4):441–476, December 1992.
[ED88] R.J. Enbody and H.C. Du. Dynamic hashing schemes. Computing Surveys, 20(2):85–113, June 1988.
[Epp10] Susanna S. Epp. Discrete Mathematics with Applications. Brooks/Cole Publishing Company, Pacific Grove, CA, fourth edition, 2010.
[ES90] Margaret A. Ellis and Bjarne Stroustrup. The Annotated C++ Reference Manual. Addison-Wesley, Reading, MA, 1990.
[ESS81] S. C. Eisenstat, M. H. Schultz, and A. H. Sherman. Algorithms and data structures for sparse symmetric gaussian elimination. SIAM Journal on Scientific Computing, 2(2):225–237, June 1981.
[F BY92] W.B. Frakes and R. Baeza-Yates, editors. Information Retrieval: Data Structures & Algorithms. Prentice Hall, Upper Saddle River, NJ, 1992.
[FF89] Daniel P. Friedman and Matthias Felleisen. The Little LISPer. Macmillan Publishing Company, New York, NY, 1989.
[FFBS95] Daniel P. Friedman, Matthias Felleisen, Duane Bibby, and Gerald J. Sussman. The Little Schemer. The MIT Press, Cambridge, MA, fourth edition, 1995.
[FHCD92] Edward A. Fox, Lenwood S. Heath, Q. F. Chen, and Amjad M. Daoud. Practical minimal perfect hash functions for large databases. Communications of the ACM, 35(1):105–121, January 1992.
[FL95] H. Scott Folger and Steven E. LeBlanc. Strategies for Creative Problem Solving. Prentice Hall, Upper Saddle River, NJ, 1995.
[FZ98] M.J. Folk and B. Zoellick. File Structures: An Object-Oriented Approach with C++. Addison-Wesley, Reading, MA, third edition, 1998.

