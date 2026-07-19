![](cover.jpg)

![cover](cover.jpg)

A Collection of Dynamic Programming Interview Questions Solved in C++

Antonio Gulli

Copyright © 2014 Antonio Gulli

All rights reserved.

ISBN:1495320480

ISBN-13:978-1495320484

Dynamic programming is the first of a series or 25 mini books devoted to algorithms, problem solving, and c++ programming

DEDICATION

To Lorenzo, my first child.

With the hope that you will enjoy mathematics for the rest of your life, as much as you enjoyed solving problem 8 when you were 10 years old

ACKNOWLEDGMENTS

Thanks to Gaetano Mendola for code reviewing

Table of Contents

[Table of Contents](#part0000.html__Toc382123405)

[Dynamic programming: the art of solving simple problems first](#part0000.html__Toc382123406)

[1. Fibonacci numbers](#part0000.html__Toc382123407)

[2. Binomial Coefficient](#part0000.html__Toc382123408)

[3. Max sub-array problem - given an array of integers, compute the largest sum continuous sub array](#part0000.html__Toc382123409)

[4. Catalan Numbers](#part0000.html__Toc382123410)

[5. Integer Knapsack – A knapsack has max capacity ![](1/images/00001.jpeg) and there are ![](1/images/00002.jpeg) items each with weight ![](1/images/00003.jpeg) and value![](1/images/00004.jpeg). Maximize the value in the knapsack without exceeding its max capacity](#part0000.html__Toc382123411)

[6. Edit Distance -– Given two strings, compute the edit distance between them](#part0000.html__Toc382123412)

[7. Neat Print – Given a sequence of words and a max number of words which can be put in a line, print the sequence of words neatly. Assume that no word is split across lines.](#part0000.html__Toc382123413)

[8. Eggs Drop – Given ![](1/images/00005.jpeg) eggs and ![](1/images/00002.jpeg) floors in a building, find the minimum number of trials required to determine the lowest floor from which an egg can be dropped without getting broken.](#part0000.html__Toc382123414)

[9. Jump Stairs – There is a stair with ![](1/images/00002.jpeg) steps. You can climb either one step or two steps at a time. How many different ways there are to climb the stair?](#part0000.html__Toc382123415)

[10. Jumping Array – Given an array of non-negative numbers, start at the first element and reach the end with a minimum number of jumps. A jump cannot exceed the length contained in the current position.](#part0000.html__Toc382123416)

[11. Dice -– Given n dice, count how many ways to get sum s.](#part0000.html__Toc382123417)

[12. Coin Change – Given ![](1/images/00002.jpeg) dollars, how many different ways there are to make the change into a set of coins![](1/images/00006.jpeg)?](#part0000.html__Toc382123418)

[13. Longest Palindrome String – Given a string, compute the longest palindromic substring](#part0000.html__Toc382123419)

[14. String Palindromes -– Given a string, find the minimum number of characters to be inserted for converting the string into a palindrome](#part0000.html__Toc382123420)

[15. LCS -– Given two strings S1 and S2, find the longest common substring](#part0000.html__Toc382123421)

[16. LCS – Given two strings, find the longest common subsequence](#part0000.html__Toc382123422)

[17. LIS – Given an array of integers, find the longest increasing subsequence](#part0000.html__Toc382123423)

[18. Bridge Matching – n cities are on the northern bank of a river and n cities are on the southern bank. You can build a bridge only between cities with the same number](#part0000.html__Toc382123424)

[19. LBS – Given an array of integers, find the longest bitonic sequence](#part0000.html__Toc382123425)

[20. Box Stacking – Given a set of ![](1/images/00007.jpeg) boxes, compute the largest stack of boxes. A box can be stacked only on top of another box with larger base.](#part0000.html__Toc382123426)

[21. Sum Subset -– Given an array of integers of size![](1/images/00008.jpeg), partition it in such a way that the two subsets have equal sum ![](1/images/00009.jpeg)](#part0000.html__Toc382123427)

[22. Partition Set – partition a multiset S of positive integers into two subsets ![](1/images/00010.jpeg) and![](1/images/00011.jpeg), such that the sum of the numbers in ![](1/images/00012.jpeg)equals the sum of the numbers in ![](1/images/00013.jpeg)](#part0000.html__Toc382123428)

[23. Segment Partition -– Given a segment of integer length![](1/images/00008.jpeg), cut it into different integer parts in such a way to maximize the product of the lengths of all parts.](#part0000.html__Toc382123429)

[24. Cutting a Rod – given a rod of length n and a vector of prices for different lengths, cut the rod for maximizing the gain](#part0000.html__Toc382123430)

[25. Bellman-Ford – Given a graph ![](1/images/00014.jpeg) and a source vertex, find the shortest paths from the source ![](1/images/00015.jpeg) to all vertices. The graph may contain negative edges](#part0000.html__Toc382123431)

[26. Max Submatrix 0/1 - Given a matrix consisting only of ![](1/images/00016.jpeg) and![](1/images/00017.jpeg), find the maximum size square sub-matrix with all ![](1/images/00018.jpeg)](#part0000.html__Toc382123432)

[27. Matrix Parenthesization -- Given a set of ![](1/images/00019.jpeg) Matrices find the most efficient way of multiplying them](#part0000.html__Toc382123433)

[28. Max Submatrix – Given a matrix of size ![](1/images/00020.jpeg) find the maximum sum rectangle](#part0000.html__Toc382123434)

[29. Given a Binary Search Tree, find the size of the largest independent set of nodes](#part0000.html__Toc382123435)

[30. Optimal Binary Tree – given a set ![](1/images/00021.jpeg) of tuples ![](1/images/00022.jpeg) , where ![](1/images/00005.jpeg) is an integer and ![](1/images/00023.jpeg) is the number of times that ![](1/images/00005.jpeg) has been observed, build a binary search three such that the total cost of all single searches is minimized](#part0000.html__Toc382123436)

[31. Boolean Parenthesization – given a Boolean expression of and, or, xor, true, false, find the number of ways to parenthesize and evaluate to true](#part0000.html__Toc382123437)

[32. Games of Coins – a set of coins are aligned and two players can pick one coin from each side in turn. Maximize the value of the coins picked by the first player](#part0000.html__Toc382123438)

[33. Maximum value contiguous subsequence – given an array of real numbers, find a contiguous subsequence with max sum ![](1/images/00009.jpeg)](#part0000.html__Toc382123439)

[34. Balanced partition – given an array of integers between 0 and![](1/images/00024.jpeg), divide the integers into two sets such that the difference of their sums is minimized](#part0000.html__Toc382123440)

[35. Scheduling – given ![](1/images/00002.jpeg) jobs, each one with a processing time ![](1/images/00025.jpeg), a profit ![](1/images/00026.jpeg) and a deadline ![](1/images/00027.jpeg), maximize the profit](#part0000.html__Toc382123441)

[36. Stock prices – Given a histogram array of unsigned integers encoding the price of a stock title during the previous year, compute the area for the largest rectangle contained in this histogram](#part0000.html__Toc382123442)

[37. Ship Battle – Given a matrix M and an array V, match the array in the matrix](#part0000.html__Toc382123443)

[Appendix](#part0000.html__Toc382123444)

# Dynamic programming: the art of solving simple problems first

Dynamic programming (DP) solves intricate problems by breaking them down into simpler components. DP can be applied to problems exhibiting two properties: overlapping subproblems and optimal substructure.

Overlappingsubproblems means that any recursive algorithm solving the problem should solve the same subproblems over and over, rather than generating new subproblems.  Optimal substructure means that any optimal solution can be constructed efficiently from the optimal solutions of its subproblems. In other words, suppose that each subproblem has its own cost function: the optimal substructure implies that the minima of each of these cost functions can be found as the minima of the global cost function restricted to the samesubsets.

DP pursues to solve each subproblem only once, as a result reducing the number of computations. After the solution to a given subproblem has been computed, it is stored in a table or "memoized". Next time the same solution is required, it is simply looked up. DP solves problems in either two methods:

a) Top-down approach: This is a consequence of the recursive mathematical definition associated to many DP problems. 

b) Bottom-up approach: This requires a reformulation of the recursive mathematical definition where subproblems are solved first and their solutions used to build-on and achieve solutions for bigger subproblems

In this book we will review a collection of Dynamic programming problems, their solution, and the C++ code related to them. Many of those problems are commonly asked during interviews and can be frequently found on Internet web sites devoted to interviews’ preparation.

# 1. Fibonacci numbers

Solution

The first two numbers in the Fibonacci sequence are 0 and 1, and each subsequent number is the sum of the previous two. By describing the numbers in his book [Liber Abaci](http://en.wikipedia.org/wiki/Liber_Abaci), [Leonardo Fibonacci](http://en.wikipedia.org/wiki/Leonardo_Fibonacci) introduced the sequence to Western European mathematics in 1200, although the sequence had been described earlier in [Indian mathematics](http://en.wikipedia.org/wiki/Indian_mathematics).  

Fibonacci numbers are mathematically defined as

![](1/images/00028.jpeg)

Code

It is trivial to write a recursive solution directly derived from the mathematical formulation. Here we provide an implementation where Fibonacci is computed at compile time leveraging the power of templates.

template <int N>

struct CTFibonacci {

 static constexpr int value() {

 return CTFibonacci<N-1>::value() +

CTFibonacci<N-2>::value();

  }

};

template <>

struct CTFibonacci<1> {

 static constexpr int value() {

 return 1;

  }

};

template <>

struct CTFibonacci<0> {

 static constexpr int value() {

 return 0;

  }

};

Complexity

Complexity is here exponential since ![](1/images/00029.jpeg) . An alternative and more efficient solution memorizes the intermediate results and it avoids to recompute the same sub-problem for multiple times. A solution is:

Code

unsigned  int Fibonacci(unsigned  int n)

{

 int a, b, sum;

  a = 0; b = 1; sum = a + b;

 if (n <= 1) return n;

 for (unsigned  int i = 2; i < n; ++i)

  {

    a = b;

    b = sum;

    sum = a + b;

  }

 return sum;

}

Complexity

Linear in time and constant in space

# 2. Binomial Coefficient

The binomial coefficient indexed by ![](1/images/00002.jpeg) and ![](1/images/00005.jpeg) and denoted by ![](1/images/00030.jpeg) is the coefficient of the ![](1/images/00031.jpeg) term in the polynomial expansion of the binomial power![](1/images/00032.jpeg). The value of this coefficient is given by![](1/images/00033.jpeg).

Solution

Computing the binomial coefficient directly from the closed formula ![](1/images/00034.jpeg) would be inefficient. However, we can prove by induction that  ![](1/images/00030.jpeg) = ![](1/images/00035.jpeg)  and we know that ![](1/images/00036.jpeg)  and![](1/images/00037.jpeg)  .Therefore, we have a direct way to compute the binomial coefficient with dynamic programming. Note that Matrix is a class defined in the appendix.

Code

unsigned  int bin(unsigned  int n, unsigned  int k,

Matrix<int> & table)

{

std::cout << "n=" << n << " k=" << k << std::endl;

 if (n == 0) return 0;

 if (!table(n - 1, k - 1))

    table(n - 1, k - 1) = bin(n - 1, k - 1, table);

 if (!table(n - 1, k))

    table(n - 1, k) = bin(n - 1, k, table);

 return table(n - 1, k - 1) + table(n - 1, k);

}

unsigned  int binomial(unsigned  int n, unsigned  int k)

{

 if (k == 0) return 1;

 if (n == 0) return 0;

  Matrix<int> table(n + 1, k + 1, 0);

 for (unsigned  int i = 0; i <= n; i++)

    table(i , 0) = 1;

 return bin(n, k, table);

}

Complexity

Linear in time![](1/images/00038.jpeg)). Space occupancy is ![](1/images/00039.jpeg)

# 3. Max sub-array problem - given an array of integers, compute the largest sum continuous sub array

Solution

This problem is a little gem. An elegant solution has been provided by Kadane.[[1]](#part0000.html__ftn1) The key intuition for this algorithm is illustrated by this picture

 ![](1/images/00040.jpeg)![](1/images/00041.jpeg)![](1/images/00042.jpeg)

![](1/images/00043.jpeg) represents the maximum value computed before analysing the current subsequence, while ![](1/images/00044.jpeg) represents the maximum for the current subsequence. If ![](1/images/00045.jpeg) , we violate the sequence continuity and therefore we can safely reset![](1/images/00046.jpeg) , a value which represents the empty string. If![](1/images/00047.jpeg), then we have found a new maximum and we can update the ![](1/images/00048.jpeg)accordingly:

Code

int maxSubArraySum(const std::vector<int> & v)

{

 int max_so_far = 0, max_ending_here = 0;

 for (unsigned  int i = 0; i < v.size(); ++i)

  {

    max_ending_here = max_ending_here + v[i];

 if (max_ending_here < 0)

      max_ending_here = 0;

 if (max_so_far < max_ending_here)

      max_so_far = max_ending_here;

  }

 return max_so_far;

}

The second implementation also returns the start and the end point for the max continuous sequence:

int kadane(const std::vector<int> & v,

int & start, int & finish)

{

 int maxSum = -std::numeric_limits<int>::max(), sum = 0;

 unsigned  int left = 0, right = 0;

  start = finish = 0;

 for (unsigned  int i = 0; i < v.size(); ++i) {

    sum += v[i];

 if (sum > maxSum) {

      maxSum = sum;

      finish = right = i;

      start  = left;

} else  if (sum < 0) {

      sum = 0;

      left = right = i+1;

    }

  }

 return maxSum;

}

Complexity

Linear in the size of the input ![](1/images/00049.jpeg)

# 4. Catalan Numbers

Catalan numbers are mathematically defined as:

![](1/images/00050.jpeg)

Those numbers have multiple applications in combinatorics.  For example:  ![](1/images/00051.jpeg) counts the number of expressions containing![](1/images/00002.jpeg)pairs of parentheses which are correctly matched (e.g. ![](1/images/00052.jpeg) represents  ((()))     ()(())     ()()()     (())()     (()()) ).  Also, ![](1/images/00051.jpeg) is the number of different ways ![](1/images/00053.jpeg) factors can be completely parenthesized (e.g. ![](1/images/00052.jpeg) represents ((ab)c)d     (a(bc))d     (ab)(cd)     a((bc)d)     a(b(cd))) ). In addition, ![](1/images/00051.jpeg) is also the number of full binary trees with ![](1/images/00054.jpeg) leaves. For a complete description of the applications please refer Wikipedia[[2]](#part0000.html__ftn2).

Solution

The solution provided is directly implementing the recursive definition.

Code

unsigned  int cat(unsigned  int n,

std::vector<unsigned  int> & table)

{

 if (n == 0) return 1;

 for (unsigned  int i = 0; i < n; i++)

  {

 if (!table[i])

      table[i] = cat(i, table);

 if (!table[n - 1 - i])

      table[n - 1 - i] = cat(n - 1 - i, table);

    table[n] += table[i] * table[n - 1 - i];

  }

 return table[n];

}

Complexity

Linear in the size of the input, ![](1/images/00055.jpeg)

Solution

Notice that we can leverage the symmetry in the definition. For instance![](1/images/00056.jpeg). This observation leads to the following recursive implementation.

Code

unsigned  int catalan2(unsigned  int n)

{

 if (n == 0) return 1;

 unsigned  int sum = 0;

 for (unsigned  int i = 0; i < n/2; ++i) {

 sum += catalan(i)*catalan(n-1-i);

 }

  sum *= 2;

 if (n % 2) {

 unsigned  int c = catalan(n/2);

    sum += c*c;

  }

 return sum;

}

# 5. Integer Knapsack – A knapsack has max capacity C and there are n items each with weight w[i] and value![](1/images/00057.jpeg)v[i]. Maximize the value in the knapsack without exceeding its max capacity

Solution

An item can be inserted in the knapsack or not: if the ![](1/images/00058.jpeg) item is inserted, then the total value contained in the knapsack will increase of ![](1/images/00059.jpeg) and the capacity ![](1/images/00060.jpeg)will decreases of![](1/images/00061.jpeg). If the item is not inserted, than the capacity will remain unchanged.  This means that the solution can be then obtained recursively. Mathematically, we can define:

![](1/images/00062.jpeg)

![](1/images/00063.jpeg)

In the remaining, we provide two different solutions: the first is top-down and recursive, while the second is based on dynamic programming and it is built bottom-up by storing partial results in a support array![](1/images/00064.jpeg).

Code

unsigned  int knapRecursive(const  unsigned  int C,

 const  unsigned  int w[],

 const  unsigned  int v[],

 const  unsigned  int n)

{

 if (n == 0 || C == 0)

 return 0;

 if (w[n - 1] > C)

 return knapRecursive(C, w, v, n - 1);

 else  return std::max(v[n - 1] +

knapRecursive(C - w[n - 1], w, v, n - 1),

             knapRecursive(C, w, v, n - 1));

}

unsigned  int knapSack(const  unsigned  int C,

 const  unsigned  int w[],

 const  unsigned  int v[],

 const  unsigned  int n)

{

  Matrix<unsigned  int> table(n + 1, C + 1);

 for (unsigned  int i = 0; i <= n; ++i)

 for (unsigned  int j = 0; j <= C; ++j)

    {

 if (i == 0 || j == 0)

        table(i, j) = 0;

 else  if (w[i - 1] <= j)

        table(i, j) =

          std::max(v[i - 1]  + table(i - 1, j - w[i - 1]),

                    table(i - 1, j));

 else

        table(i, j) = table(i - 1, j);

    }

 return table(n, C);

}

Complexity

Pseudolinear in time ![](1/images/00065.jpeg) and Pseudolinear in space ![](1/images/00065.jpeg)

# 6. Edit Distance -– Given two strings, compute the edit distance between them

Solution

The edit distance is the minimum number of edits required to convert one string into another. For simplicity, we assume that the cost of insertion and deletion is 1\. Consider two strings ![](1/images/00066.jpeg) and![](1/images/00067.jpeg), we can define a cursor ![](1/images/00068.jpeg) for scanning S1 and a cursor ![](1/images/00069.jpeg) for scanning S2\. The edit distance ![](1/images/00070.jpeg) is defined as it follows:

![](1/images/00071.jpeg)

In other words: if the characters are aligned, the edit distance for the problem ![](1/images/00072.jpeg) will not increase, otherwise we need to align the strings by reducing the size of S1, or S2 or both.

Now let’s consider the base cases. Clearly, ![](1/images/00073.jpeg) because this case represents the empty strings. We can also define ![](1/images/00074.jpeg) and ![](1/images/00075.jpeg) , because in this case we are comparing a string of length ![](1/images/00076.jpeg) (respectively ![](1/images/00077.jpeg)) with the empty string. We can use the above definition for computing the edit distance by tabulating all the values ![](1/images/00078.jpeg) with complexity![](1/images/00079.jpeg).

However, we can significantly improve the complexity by taking into account that we only need the input from the previous column in the table for computing the current column. This will allow us to require only![](1/images/00080.jpeg). The code uses initialize the column ![](1/images/00081.jpeg) for each![](1/images/00082.jpeg) and this represents the maximum cost for position![](1/images/00083.jpeg). Then, we have two loops. The most external loop scans the string ![](1/images/00010.jpeg) for each ![](1/images/00068.jpeg) and it initializes ![](1/images/00084.jpeg) which the maximum cost for the position. The internal loop scans the string ![](1/images/00013.jpeg) for each ![](1/images/00069.jpeg) and updates the edit distance value by directly applying the recursive definition. When the internal loop is concluded the columns ![](1/images/00085.jpeg) and ![](1/images/00086.jpeg) are swapped and the scan of ![](1/images/00010.jpeg) continues.

There are situations where it is appropriate to have different costs according to the specific edit operations (delete, insert) required to align the strings. Those changes are left as an exercise for the reader.

Code

unsigned  int editDistance(const std::string &s1,

const std::string & s2)

{

 const  size_t len1 = s1.size(), len2 = s2.size();

 std::vector<unsigned  int> col(len2 + 1),

prevCol(len2 + 1);

 std::iota(prevCol.begin(), prevCol.end(), 0);

 for (unsigned  int i = 0; i < len1; ++i) {

               col[0] = i + 1;

 for (unsigned  int j = 0; j < len2; ++j)

                             col[j + 1] = std::min(1 + col[j],

                                           std::min(1 + prevCol[j],

                                                                       prevCol[j] +

(s1[i] == s2[j] ? 0 : 1)));

               col.swap(prevCol);

 }

 return prevCol[len2];

}

Complexity

Complexity is  ![](1/images/00087.jpeg)

# 7. Neat Print – Given a sequence of words and a max number of words which can be put in a line, print the sequence of words neatly. Assume that no word is split across lines.

Solution

Let ![](1/images/00088.jpeg) be the length of  word![](1/images/00089.jpeg). Intuitively, the cost of the first word is ![](1/images/00090.jpeg) and for the remaining words we can initially define![](1/images/00091.jpeg). Also, let ![](1/images/00092.jpeg) and consider the following recurrence, where we build the optimal cost for word![](1/images/00093.jpeg), by considering the optimal cost for word![](1/images/00094.jpeg):

![](1/images/00095.jpeg)

However this definition is not yet meeting our goal for two reasons. First, ![](1/images/00096.jpeg) only considers the cost of the previous word, while it should consider all the words that can fit a line up to a maximal cost![](1/images/00097.jpeg). Therefore we need to redefine ![](1/images/00096.jpeg) in such a way to accumulate the cost of the previous words and stop before at the point where this cost becomes negative. Intuitively for each given word we need to scan no more than a ![](1/images/00098.jpeg) position backwards. This can be addressed by defining ![](1/images/00099.jpeg) for a leftmost word ![](1/images/00100.jpeg)  such that![](1/images/00101.jpeg). Second, the cost should be non-linear because we want to balance across lines  (e.g. leaving two positions in one same line should intuitively cost more than leaving a position in one and the other position in another line). This requirement can be fulfilled in multiple ways, for instance by defining ![](1/images/00102.jpeg) or more conveniently for bitwise computation: ![](1/images/00103.jpeg). To summarize our goal is to find:

![](1/images/00104.jpeg) such that![](1/images/00105.jpeg). In the code the vector ![](1/images/00106.jpeg) will contain final decreasing values containing the residuals for each word added to a given line. The values will increase again anytime that there is a need to change line.

Code

void neatPrint(std::vector<unsigned  int> & M,

  const std::vector<unsigned  int> & length,

  unsigned  int  max, int  n)

{

int penalty;

  for (int i = 0; i < n; i++)

               {

 penalty = max - length[i];

  M[i] = std::min(M[i], (i - 1 < 0 ? 0 : M[i - 1]) +

                                           (1 << penalty));

  for (int j = i - 1; j >= 0; j--)

                             {

                                           penalty -= (length[j] + 1);

  if (penalty < 0)

  break; // generate next line

  M[i] = std::min(M[i],

((j - 1 < 0) ? 0 : M[j - 1]) +

                                                         (1 << penalty));

                             }

               }

}

void solveNeatPrint(const std::vector<unsigned  int> & length, unsigned  int  max)

{

 int n = length.size();

 std::vector<unsigned  int> M(n,

std::numeric_limits<unsigned  int>::max());

 neatPrint(M, length, max, n);

 for (int i = 0; i < n; ++i)

 std::cout << M[i] << ' ';

 std::cout << std::endl;

}

Complexity

Note that ![](1/images/00107.jpeg) can be computed in linear time of the input size, while ![](1/images/00108.jpeg) can be computed in ![](1/images/00109.jpeg) time.

# 8. Eggs Drop – Given k eggs and n floors in a building, find the minimum number of trials required to determine the lowest floor from which an egg can be dropped without getting broken.

Solution

This is a classical puzzle, frequently asked during interviews. Let ![](1/images/00110.jpeg) be the minimum number of attempts given ![](1/images/00005.jpeg)  eggs and n floors. A dynamic solution can be computed by considering that when we drop an egg from floor f there are only two possible outcomes:

a) If the egg breaks, then we have ![](1/images/00111.jpeg) eggs and we need to check the ![](1/images/00112.jpeg) floor

b) If the egg does not break, then we have ![](1/images/00005.jpeg) eggs  and the remaining ![](1/images/00113.jpeg) floors left

Since we want to minimize the number of attempts, in the worst scenario we have to consider the maximum between a) and b). The relation then becomes:

![](1/images/00114.jpeg)

![](1/images/00115.jpeg)

The base case are: ![](1/images/00116.jpeg)because if we have only one egg then we have no other option but to climb the floors one by one, and ![](1/images/00117.jpeg) because if we have only one floor then we just need to check it. In addition, we can define![](1/images/00118.jpeg) and![](1/images/00119.jpeg) because those are borderline cases.

This characterization leads to a straightforward recursion implementation given below where we memorize partial solutions in a support ![](1/images/00120.jpeg) for avoiding the recompute those solutions again and again.

Code

int eggDropHelper(unsigned  int  k, unsigned  int  n,

Matrix<int> & table)

{

 if (n == 1 || n == 0)

  return  n;

 if (k == 1)

  return  n;

 if (!k)

  return 0;

 unsigned  int min =

               std::numeric_limits<unsigned  int>::max();

 unsigned  int res;

 for (unsigned  int f = 1; f <= n; ++f)

 {

               res = std::max(

                             ((table(k - 1, f - 1) == -1) ?

  table(k - 1, f - 1) =

                                                         eggDropHelper(k - 1, f - 1, table) :

  table(k - 1, f - 1)

                                           ),

                                          (table(k, n - f) == -1) ?

  table(k, n - f) =

                                                         eggDropHelper(k, n - f, table) :

  table(k, n - f)

                                           );

 if (res < min)

                             min = res;

 }

 return min + 1;

}

int eggDrop(unsigned  int  k, unsigned  int  n)

{

 Matrix<int> table(k+1, n+1, -1);

 return eggDropHelper(k, n, table);

}

Complexity

The DP solution is left as exercise. A straightforward implementation needs ![](1/images/00121.jpeg) entries in a table where each entry is computed at most![](1/images/00008.jpeg)  times. Therefore, the algorithm runs in ![](1/images/00122.jpeg) time. Time complexity can be reduced to ![](1/images/00123.jpeg) , if we consider that the optimal floor  ![](1/images/00124.jpeg) for ![](1/images/00125.jpeg) is certainly equal or larger than the one for![](1/images/00126.jpeg), so we can avoid to restart the minimum computation from 1\. Also, it could be useful to prove that the function ![](1/images/00127.jpeg)  is convex in f so the minimum is unique and can be computed with a linear scan.

# 9. Jump Stairs – There is a stair with n steps. You can climb either one step or two steps at a time. How many different ways there are to climb the stair?

Solution

Let’s try a number of examples: If we have only one step, then there is only a way to climb the stair; if we have two steps, then there are two ways (e.g. 1 step, 1 step, or 2 steps); if we have three steps, then there are three ways. More examples are given in the following table:

| Steps | #Confs | Configurations |
| 1 | 1 | 1 |
| 2 | 2 | (1, 1); (2) |
| 3 | 3 | (1, 1, 1); (1, 2) ; (2, 1) |
| 4 | 5 | (1, 1, 1, 1); ( 2, 1, 1); (1, 2, 1); (1, 1, 2); (2, 2) |
| 5 | 8 | (1, 1, 1, 1, 1); ( 2, 1, 1, 1); (1, 2, 1, 1); (1, 1, 2, 1); (1, 1, 1, 2);(2, 2, 1); (1, 2, 2), (2, 1, 2) |

We notice that there is a pattern: at each step the number of configurations is the sum of the number of configurations of the previous and last steps but one. Mathematically:

![](1/images/00128.jpeg)

This formula has a straightforward interpretation: we jump to the n step either from the ![](1/images/00129.jpeg) step or from the ![](1/images/00130.jpeg) step. Note that the base cases are different with respect to Fibonacci.

Code

unsigned  long jump(unsigned  int  n)

{

 if (n == 1) return 1;

 if (n == 2) return 2;

 unsigned  long current = 0, prev = 2, prevPrev = 1;

 for (unsigned  int i = 3; i <= n; i++)

  {

    current = prev + prevPrev;

    prevPrev = prev;

    prev = current;

  }

 return current;

}

Complexity

Linear in the input size.

# 10.  Jumping Array – Given an array of non-negative numbers, start at the first element and reach the end with a minimum number of jumps. A jump cannot exceed the length contained in the current position.

Solution

Given the array![](1/images/00131.jpeg)], the base cases are when ![](1/images/00132.jpeg) or when![](1/images/00133.jpeg). For those cases, we have no solution. Otherwise, the mathematical formulation can be computed for each  position ![](1/images/00076.jpeg)  by finding the maximum jump length for position ![](1/images/00134.jpeg) such that the required constrain ![](1/images/00135.jpeg) is not violated. Mathematically![](1/images/00136.jpeg).

Code

unsigned  int jump(const  unsigned  int  a[], unsigned  int  n)

{

              std::vector<unsigned  int> result(n);

 if (n == 0 || a[0] == 0)

  return std::numeric_limits<unsigned  int>::max();

              result[0] = 0;

 for (unsigned  int i = 1; i < n; ++i)

 {

               result[i] =

std::numeric_limits<unsigned  int>::max();

  for (unsigned  int j = 0; j < i; j++)

 if ((a[j] >= (i - j)) &&

(result[j] + 1 < result[i]))

                                          result[i] = result[j] + 1;

 }

 return result[n - 1];

}

Complexity

Linear in time and space

# 11.  Dice -– Given n dice, count how many ways to get sum s.

Solution

Let’s suppose that each die has m faces and define a function ![](1/images/00137.jpeg) which counts how many ways we have to get sum ![](1/images/00138.jpeg)for ![](1/images/00002.jpeg)  dices with ![](1/images/00019.jpeg)  faces.  We can compute this function starting from the result with ![](1/images/00129.jpeg)  dices. In particular, if we get a sum ![](1/images/00139.jpeg) from ![](1/images/00129.jpeg) dice we need to add ![](1/images/00140.jpeg)from the ![](1/images/00141.jpeg) die for each![](1/images/00142.jpeg):

![](1/images/00143.jpeg)

Note that we have![](1/images/00144.jpeg) terms in this sum. We use a support table ![](1/images/00145.jpeg) where we store the current sum and the current dice. The base case is with only one die and in this case there is only one way to get the sum![](1/images/00146.jpeg)  therefore ![](1/images/00147.jpeg) for![](1/images/00148.jpeg). Then, for each possible sum value ![](1/images/00149.jpeg) and for each possible dice ![](1/images/00150.jpeg) and for each possible valid value produced by a die ![](1/images/00151.jpeg) we update ![](1/images/00145.jpeg) according to the above definition.

Code

unsigned  long playDices(unsigned  int  n, unsigned  int  m, unsigned  int  s)

{

 if ((n == 0) ||  (m < 2) || (s == 0) || (n*m < s) )

  return 0;

 Matrix<int> mem(s + 1, n + 1, 0);

  for (unsigned i = 1; i <= m && i <= s; ++i)

               mem(i, 1) = 1;

 for (unsigned i = 1; i <= s; ++i)

  for (unsigned j = 2; j <= n; ++j)                 

  for (unsigned k = 1; k <= m && k < i; ++k)

                                           mem(i, j) += mem(i - k, j - 1);

 return mem(s, n);

}

Complexity

Complexity is ![](1/images/00152.jpeg)

# 12.  Coin Change – Given n dollars, how many different ways there are to make the change into a set of coins![](1/images/00153.jpeg)S?

Solution

Let’s define ![](1/images/00154.jpeg) and let ![](1/images/00155.jpeg) be the change for ![](1/images/00002.jpeg) dollars given a set ![](1/images/00156.jpeg)of![](1/images/00157.jpeg) coins. We suppose to a have an infinite amount of each type of coin![](1/images/00158.jpeg). A coin ![](1/images/00159.jpeg) can either be part of the change or not. This simple observation is used for a dynamic programming solution

![](1/images/00160.jpeg)

where ![](1/images/00161.jpeg) counts when the coin ![](1/images/00159.jpeg) has been not selected, while ![](1/images/00162.jpeg) counts the selection of a new coin![](1/images/00158.jpeg). The base cases are for ![](1/images/00163.jpeg) where the only solution is not to change any money, ![](1/images/00164.jpeg) for ![](1/images/00165.jpeg) where there is no solution because we have a negative amount of money![](1/images/00166.jpeg) and ![](1/images/00164.jpeg)  ![](1/images/00167.jpeg) because we have money but there is no change available. The first implementation is recursive, while the second is based on dynamic programming.

Code

int changeCoin(int  n, const  unsigned  int  S[], int  t)

{

 if (n == 0)

  return 1;

  if ((n<0) || (t < 0 && n > 0))

  return 0;

 return changeCoin(n, S, t - 1)

               + changeCoin(n - S[t], S, t);

}

int changeCoinDP(unsigned  int  n, const  unsigned  int  S[],

 unsigned  int  t)

{

 Matrix<unsigned  int> table(n + 1, t);

 for (unsigned  int j = 0; j < t; ++j)

               table(0, j) = 1;

 for (unsigned  int i = 1; i <= n; ++i)

  for (unsigned  int j = 0; j < t; ++j)

                             table(i, j) =

 ((i >= S[j]) ? table(i - S[j], j) : 0) +

                                           ((j>0) ? table(i, j - 1) : 0);

 return table(n, t-1);

}

Complexity

Time complexity is ![](1/images/00168.jpeg)

# 13.  Longest Palindrome String – Given a string, compute the longest palindromic substring

A string is palindromic if it is read the same backward and forward, as Madam, I’m Adam or Poor Dan is in a droop.

Solution

A solution can be computed for the string ![](1/images/00169.jpeg)  by considering that![](1/images/00170.jpeg) and

![](1/images/00171.jpeg)

This definition computes the longest palindromic substring by starting from the whole string![](1/images/00172.jpeg) and it is easy to directly write the code implementing this recursive formulation.

However, another more convenient approach is to define ![](1/images/00173.jpeg) if the string is palindromic for![](1/images/00174.jpeg) . The following base cases hold for single characters and for couple of characters:

![](1/images/00175.jpeg)

In addition, we can define the recurrence![](1/images/00176.jpeg) for increasing lengths ![](1/images/00177.jpeg) where ![](1/images/00178.jpeg) and![](1/images/00179.jpeg).

Note that with this definition the interval ![](1/images/00180.jpeg) is contained in the interval ![](1/images/00181.jpeg) and therefore we just need to test the two characters in the border![](1/images/00182.jpeg)). The code keep tracks of the starting position where the palindromic string begins (![](1/images/00183.jpeg)) and its length (![](1/images/00184.jpeg)).

Code

std::string longestPalindrome(const std::string & s) {

 unsigned  int n = s.length();

 if (n == 0)

  return  s;

 unsigned  int longestStart= 0;

 unsigned  int maxLen = 1;

 Matrix<unsigned  int> table(n, n, false);

 for (unsigned  int i = 0; i < n; ++i)

 table(i, i) = true;

 for (unsigned  int i = 0; i < n - 1; ++i) {

  if (s[i] == s[i + 1]) {

 table(i, i + 1) = true;

                             longestStart = i;

                             maxLen = 2;

               }

 }

 for (unsigned  int len = 3; len <= n; ++len) {

  for (unsigned  int i = 0; i < n - len + 1; ++i) {

  unsigned  int j = i + len - 1;

  if (table(i + 1, j - 1) && s[i] == s[j])

                             {             

 table(i, j) = true;

 if (len > maxLen)

                                           {

                                                         longestStart = i;

                                                         maxLen = len;

                                           }

                             }

               }

 }

 return  s.substr(longestStart, maxLen);

}

Complexity

Complexity is![](1/images/00185.jpeg) and space is![](1/images/00185.jpeg). Providing a solution with reduced space is left as exercise.

# 14.  String Palindromes -– Given a string, find the minimum number of characters to be inserted for converting the string into a palindrome

Solution

Consider the string ![](1/images/00186.jpeg) and define ![](1/images/00187.jpeg) as the number of characters to be inserted for getting a palindrome. We have:

![](1/images/00188.jpeg)

The base case are ![](1/images/00189.jpeg) if ![](1/images/00190.jpeg)  and

![](1/images/00191.jpeg)

A dynamic programming implementation can be realized by adopting a ![](1/images/00192.jpeg) which stores the minimum number of insertions needed to convert ![](1/images/00186.jpeg) into a palindrome. The table is filled in by incremental gap such that![](1/images/00193.jpeg) and by considering the subintervals contained between the positions![](1/images/00194.jpeg),![](1/images/00195.jpeg)

Code

unsigned  int numInsertionPaly(const std::string & str,

unsigned  int  l, unsigned  int  r)

{

 if (r <= l)

  return 0;

 if (l == r - 1)

  return (str[l] == str[r]) ? 0 : 1;

 if (str[l] == str[r])

  return numInsertionPaly(str, l + 1, r - 1);

 else

  return (std::min(numInsertionPaly(str, l + 1, r),

               numInsertionPaly(str, l, r - 1)) + 1);

}

int minInsertionsPalyndromeDP(const std::string & str)

{

 unsigned  int n = str.length();

 Matrix<unsigned  int> table(n + 1, n + 1, 0);

 unsigned  int gap, left, right;

 for (gap = 1; gap < n; ++gap)

  for (left = 0, right = gap;

right < n; ++left, ++right)

                                          table(left, right) =

                             (str[left] == str[right]) ?

                                           table(left + 1, right - 1) :

                                           (std::min(table(left, right - 1),

                                                         table(left + 1, right)) + 1);

 return table(0, n - 1);

}

Complexity

Complexity is ![](1/images/00196.jpeg) in time and space

# 15.  LCS -– Given two strings S1 and i, find the longest common substring

The longest common substring problem consists in finding the longest string that is a substring of two strings.[[3]](#part0000.html__ftn3)

Solution

On way to solve the problem is to find the longest common suffix for all the pairs of prefixes for the strings  ![](1/images/00010.jpeg) and S2\. The longest common suffix is:

![](1/images/00197.jpeg)

Given![](1/images/00198.jpeg), we can compute the longest common substring because the maximal of the longest common suffixes of all possible prefixes is the longest common substring of S1 and T1.

![](1/images/00199.jpeg)

![](1/images/00200.jpeg)

Code

int LCSubStr(const std::string & S1, const std::string & S2)

{

 unsigned  int m = S1.length();

 unsigned  int n = S2.length();

 unsigned  int result = 0;

 Matrix<unsigned  int> LCSuff(m + 1, n + 1);

 for (unsigned  int i = 0; i <= m; i++) {

 for (unsigned  int j = 0; j <= n; j++) {

 if (i == 0 || j == 0) {

        LCSuff(i, j) = 0;

} else  if (S1[i - 1] == S2[j - 1]) {

        result = std::max(

            (LCSuff(i, j) = LCSuff(i - 1, j - 1) + 1),

            result

            );

} else {

        LCSuff(i, j) = 0;

      }

    }

  }

 return result;

}

Complexity             

Complexity is ![](1/images/00123.jpeg) and space is![](1/images/00201.jpeg). Reducing the space to ![](1/images/00202.jpeg) is left as an exercise.

# 16.  LCS – Given two strings, find the longest common subsequence

Given the two strings, two subsequences are in common if they appear in the same order but not necessarily contiguous. The main difference with the previous problem is that here the terms are not consecutive.

Solution

A dynamic programming solution can be computed for the string ![](1/images/00203.jpeg)  and the string ![](1/images/00204.jpeg)1] by defining a recursive function ![](1/images/00205.jpeg) on the prefixes ![](1/images/00206.jpeg) and ![](1/images/00207.jpeg) of length ![](1/images/00076.jpeg) and ![](1/images/00077.jpeg)

![](1/images/00208.jpeg)

A dynamic programming solution can be built by using a table where we store the partial results of the above computation (function![](1/images/00209.jpeg)). In addition we store the direction that generated the table for reconstructing the common subsequence in a next step (function![](1/images/00210.jpeg))

Code

enum  where{DiagonalUpward, Upward, Downward};

void printLCS(const  Matrix<where>& directions, const std::string& str,

  unsigned  int  i, unsigned  int  j)

{

 if (i == 0 || j == 0)return;

 if (directions(i, j) == DiagonalUpward)

 {

               printLCS(directions, str, i - 1, j - 1);

 std::cout << str[i];

 }

 else  if (directions(i, j) == Upward)

               printLCS(directions, str, i - 1, j);

 else

               printLCS(directions, str, i, j - 1);

}

void LCS(const std::string& s1, const std::string& s2)

{

 const  unsigned  int m = s1.size() + 1;

 const  unsigned  int n = s2.size() + 1;

 Matrix<unsigned  int> table(m, n, 0);

 Matrix<where> directions(m, n);

 for (unsigned  int i = 1; i<m; i++)

  for (unsigned  int j = 1; j<n; j++)

  if (s1[i] == s2[j])

                             {

                                           table(i, j) = table(i - 1, j - 1) + 1;

 directions(i, j) = DiagonalUpward;

                             }

  else

  if (table(i - 1,j) >= table(i, j - 1))

                                           {

                                                         table(i, j) = table(i - 1, j);

 directions(i, j) = Upward;

                                           }

  else

                                           {

                                                         table(i, j) = table(i, j - 1);

 directions(i, j) = Downward;

                                           }

printLCS(directions, s1, m-1, n-1);

}

Complexity

Complexity is![](1/images/00201.jpeg) and space is![](1/images/00201.jpeg).

# 17.  LIS – Given an array of integers, find the longest increasing subsequence

Solution

The solution can be quickly identified by dynamic programming. Suppose that we scan the array A, then at position ![](1/images/00076.jpeg) we have that ![](1/images/00211.jpeg)   

Code

unsigned  int LIS(const std::vector<unsigned  int> & v)

{

 unsigned  int max;

 unsigned  int n = v.size();

 std::vector<unsigned  int> maxHere(n, 0);

 for (unsigned  int k = 0; k < n; ++k)

 {

               max = 0;

  for (unsigned  int j = 0; j < k; ++j)

  if (v[k] > v[j])

  if (maxHere[j] > max)

                                                         max = maxHere[j];

               maxHere[k] = max + 1;

 }

 max = 0;

 for (unsigned  int k = 0; k < n; ++k)

  if (maxHere[k] > max)

                             max = maxHere[k];

 return max;

}

Complexity

Complexity is ![](1/images/00212.jpeg) and space is![](1/images/00213.jpeg).  An ![](1/images/00214.jpeg) algorithm is described here[[4]](#part0000.html__ftn4).

# 18.  Bridge Matching – n cities are on the northern bank of a river and n cities are on the southern bank. You can build a bridge only between cities with the same number

Solution

Let ![](1/images/00215.jpeg) be the number of cit![](1/images/00216.jpeg) on the northern bank and ![](1/images/00217.jpeg) the number of cit![](1/images/00218.jpeg) on the southern bank. The problem can be reduced to the one of finding the longest common subsequence. Suppose to sort the bridges built by their first city. If two bridges cross, then we have one bridge ![](1/images/00219.jpeg) and another bridge ![](1/images/00220.jpeg) such that either ![](1/images/00221.jpeg) and ![](1/images/00222.jpeg) or ![](1/images/00223.jpeg) and![](1/images/00224.jpeg). We can sort the tuples by increasing ![](1/images/00225.jpeg) indexes and then compute the longest increasing sequence (LIS) on the sequence of![](1/images/00158.jpeg).

Code

Left as exercise

Complexity

Since we need to sort the complexity is ![](1/images/00226.jpeg)

# 19.  LBS – Given an array of integers, find the longest bitonic sequence

Solution

A sequence is bitonic, if it initially increases and then decreases. For an array ![](1/images/00227.jpeg)  we can compute the longest increasing sequence ![](1/images/00228.jpeg) ending at position ![](1/images/00076.jpeg) and the longest decreasing sequence ![](1/images/00229.jpeg) starting at position![](1/images/00093.jpeg). For each position ![](1/images/00076.jpeg) we define:

![](1/images/00230.jpeg)

and

![](1/images/00231.jpeg)

Code

Left as exercise

Complexity

Complexity is![](1/images/00232.jpeg).

# 20.  Box Stacking – Given a set of 3d boxes, compute the largest stack of boxes. A box can be stacked only on top of another box with larger base.

Solution

This problem is a variation of the longest increasing sequence. Each box![](1/images/00093.jpeg) has three dimensions ![](1/images/00233.jpeg) which can be rotated to form the base: either (![](1/images/00234.jpeg)), or![](1/images/00235.jpeg), or![](1/images/00236.jpeg). If we suppose having infinite amount of each box types, then we can solve this problem by computing the LIS for the remaining dimensions of the box.

Code

Left as exercise

Complexity

Complexity is![](1/images/00237.jpeg).

# 21.  Sum Subset -– Given an array of integers of size![](1/images/00153.jpeg)n, partition it in such a way that the two subsets have equal sum s

Solution

Sum subset problem is and important problem in computer science with application in cryptography and complexity[[5]](#part0000.html__ftn5). The problem is NP-Complete. The most naïve solution generates all the subsets and for each of them it checks whether the sum is the right number. The complexity is ![](1/images/00238.jpeg) where ![](1/images/00239.jpeg)the size of the array.  

We can use Dynamic programming for providing a pseudo-polynomial solution. First, if the sum is odd there is no solution, while if the sum is even we can try to find a subset. Second, if the current element is larger than the sum we must skip it, otherwise we can decide whether we want to include it or not. Therefore ![](1/images/00240.jpeg) depends on![](1/images/00241.jpeg), if we don't include the element ![](1/images/00242.jpeg) for the position ![](1/images/00243.jpeg) and for the current sum value![](1/images/00244.jpeg). While it depends on ![](1/images/00245.jpeg) if we include the element.

![](1/images/00246.jpeg)

The base cases are ![](1/images/00247.jpeg) because there is always a subset with zero sum, and ![](1/images/00248.jpeg) because the empty set cannot have a subset of sum![](1/images/00093.jpeg). The code implements a recursive and a dynamic programming solution

Code

bool isSubsetSum(const std::vector<unsigned  int> & v,

const  unsigned  int  n, unsigned  int  sum)

{

 if (n == 0 && sum != 0)

  return  false;

 if (sum == 0)

  return  true;

 if (v[n - 1] > sum)

  return isSubsetSum(v, n - 1, sum);

 return isSubsetSum(v, n - 1, sum) ||

isSubsetSum(v, n - 1, sum - v[n - 1]);

}

bool partition(const std::vector<unsigned  int> & v,

unsigned  int  n)

{

 int sum = std::accumulate(v.begin(), v.end(), 0);

 if (sum % 2 != 0)

  return  false;

 return isSubsetSum(v, n, sum / 2);

}

bool isSubsetSumDP(const std::vector<unsigned  int> & v,

const  unsigned  int  n, unsigned  int  sum)

{

 Matrix<bool> subset(sum + 1, n + 1);

 for (unsigned  int j = 0; j <= n; j++)

 subset(0, j) = true;

 for (unsigned  int i = 1; i <= sum; i++)

 subset(i, 0) = false;

 for (unsigned  int i = 1; i <= sum; i++)

 for (unsigned  int j = 1; j <= n; j++) {

               subset(i, j) = subset(i, j - 1);

  if (i >= v[j - 1]) {

                             subset(i, j) = subset(i, j) ||

subset(i - v[j - 1], j - 1);

               }

 }

 return subset(sum, n);

}

Complexity

Complexity is pseudo-polynomial ![](1/images/00249.jpeg)

# 22.  Partition Set – partition a multiset S of positive integers into two subsets S1 and S2, such that the sum of the numbers in S1 equals the sum of the numbers in S2

Solution

This is a variant of the previous problem with a similar pseudo linear solution based on dynamic programming.

Code

bool isPartitionDP(const std::vector<unsigned  int> & v)

{

 unsigned  int sum = std::accumulate(v.begin(), v.end(), 0);

 return isSubsetSumDP(v, v.size(), sum / 2);

}

void testPartition()

{

 int v1[] = { 3, 1, 1, 2, 2, 1 };

  std::vector<unsigned  int> vec1(v1,

v1 + sizeof(v1) / sizeof(int));

 if (isPartitionDP(vec1) == true)

std::cout << "Found a partition";

 else

std::cout << "No partition";

}

Complexity

Complexity is pseudo-polynomial![](1/images/00250.jpeg)), where ![](1/images/00251.jpeg) is the sum of elements in the vector.

# 23.  Segment Partition -– Given a segment of integer length![](1/images/00153.jpeg)n, cut it into different integer parts in such a way to maximize the product of the lengths of all parts.

Solution

We can split the segment for all the integer positions and compute the max product of the two parts. If we split it in position![](1/images/00093.jpeg), then the product is![](1/images/00252.jpeg). In addition, the part![](1/images/00253.jpeg) can be further split. So the product can be reclusively computed as![](1/images/00254.jpeg). The base cases are![](1/images/00255.jpeg).

Code

unsigned  int segment(unsigned  int  n)

{

 if (n == 0 || n == 1) return 0;

 unsigned  int m = 0;

 for (unsigned  int i = 1; i < n; i++)

               m = std::max(m, std::max(i * (n - i),

                             segment(n - i) * i));

 return m;

}

unsigned  int segmentDPhelper(unsigned  int  n,

 std::vector<unsigned  int> & seg)

{

 unsigned  int m = 0;

 for (unsigned  int i = 1; i < n; i++)

 {

  if (!seg[n - i])

  seg[n - i] = segmentDPhelper(n - i, seg);

               m = std::max(m, std::max(i * (n - i),

 seg[n - i] * i));

 }

 return m;

}

unsigned  int segmentDP(unsigned  int  n)

{

 if (n == 0 || n == 1) return 0;

 std::vector<unsigned  int> seg(n, 0);

 return segmentDPhelper(n, seg);

}

Complexity

Linear in time and space

# 24.  Cutting a Rod – given a rod of length n and a vector of prices for different lengths, cut the rod for maximizing the gain

Solution

The idea is very similar to the one of the previous problem. Let’s suppose to have an array of ![](1/images/00256.jpeg) we can define ![](1/images/00257.jpeg) for ![](1/images/00258.jpeg)

Code

unsigned  int cutDPhelper(

  const std::vector<unsigned  int> & price,

  unsigned  int  n, std::vector<unsigned  int> & cut)

{

 unsigned  int m = 0;

 for (unsigned  int i = 1; i < n; i++)

 {

  if (!cut[n - i - 1])

  cut[n - i - 1] =

  cutDPhelper(price, n - i - 1, cut);

 m = std::max(m, price[i] + cut[n - i - 1]);

 }

 return m;

}

unsigned  int cutDP(const std::vector<unsigned  int> & price,

 unsigned  int  n)

{

 if (n <= 0) return 0;

 std::vector<unsigned  int> seg(n, 0);

 return cutDPhelper(price, n, seg);

}

Complexity

Linear in time and space.

# 25.  Bellman-Ford – Given a graph G and a source vertex, find the shortest paths from the source src to all vertices. The graph may contain negative edges

Solution

This is a classical dynamic programming problem and the solution is due to Bellman-Ford[[6]](#part0000.html__ftn6). Let’s suppose that ![](1/images/00259.jpeg) is the weight associated to the![](1/images/00260.jpeg) for each edge in a directed graph![](1/images/00261.jpeg). For our computation we need a support array ![](1/images/00262.jpeg) of size![](1/images/00263.jpeg). The first step is to initialize all entries in ![](1/images/00262.jpeg) to infinite with the only exception of ![](1/images/00264.jpeg) because ![](1/images/00015.jpeg) is reachable with zero distance. Then, for ![](1/images/00265.jpeg) times we compute:

![](1/images/00266.jpeg)

![](1/images/00267.jpeg)

![](1/images/00268.jpeg)

At the end a negative edge can be detected by checking for each edge whether![](1/images/00269.jpeg) , if ![](1/images/00270.jpeg)

Code

void BellmanFord(const  Graph & g, int  src)

{

              std::vector<int> dist(g.numNodes(),

                             std::numeric_limits<int>::max());

 std::vector<int> predecessor(g.numNodes(), -1);

              dist[src] = 0;

 for (nodeID u = 0; u < g.numNodes(); u++)

  for (auto  const & e : g.edges(u))

               {

  if (dist[u] + e.w < dist[e.v])

                             {

                                           dist[e.v] = dist[u] + e.w;

                                           predecessor[e.v] = u;

                             }

               }

 for (nodeID u = 0; u < g.numNodes(); u++)

  for (auto  const & e : g.edges(u))

  if (dist[u] + e.w < dist[e.v])

 std::cout << "negative cycle";

 for (nodeID v = 0; v < g.numNodes(); ++v)

 std::cout << predecessor[v] << "->"

<< v << " d=" << dist[v] << std::endl;

}

Complexity

Time complexity is![](1/images/00271.jpeg)

# 26.  Max Submatrix 0/1 - Given a matrix consisting only of 0s and![](1/images/00153.jpeg)1s, find the maximum size square sub-matrix with all 1s

Solution

A dynamic programming solution can be defined as follows. Let ![](1/images/00106.jpeg) be the matrix of 0s and 1s of size ![](1/images/00272.jpeg) and consider another matrix ![](1/images/00156.jpeg)of same size. If ![](1/images/00273.jpeg), then it can contribute to either position ![](1/images/00274.jpeg)[j], or![](1/images/00275.jpeg), or![](1/images/00276.jpeg)] which can be expressed as![](1/images/00277.jpeg). If ![](1/images/00278.jpeg) then![](1/images/00279.jpeg). Here is the code

Code

void FindMaxSubSquare(const  Matrix<bool> & m,

         int &maxI, int &maxJ, int &size)

{

 Matrix<int> s(m.dim1(), m.dim2());

 for (unsigned i = 0; i < m.dim1(); i++)

 s(i, 0) = m(i, 0);

 for (unsigned j = 0; j < m.dim2(); j++)

 s(0, j) = m(0, j);

 for (unsigned  int i = 1; i < m.dim1(); i++)

  for (unsigned  int j = 1; j < m.dim2(); j++)

               {

  if (m(i,j))

                                           s(i,j) = std::min(std::min(s(i,j - 1),

                                                         s(i - 1, j)), s(i - 1,j - 1)) + 1;

  else

                                           s(i, j) = 0;

               }

 size = s(0, 0); maxI = 0; maxJ = 0;

 for (unsigned  int i = 0; i < m.dim1(); i++)

  for (unsigned  int j = 0; j < m.dim2(); j++)

  if (size < s(i, j))

                             {

  size = s(i, j);

  maxI = i;

  maxJ = j;

                             }

}

Complexity

Complexity is ![](1/images/00280.jpeg)

# 27.  Matrix Parenthesization -- Given a set of m Matrices find the most efficient way of multiplying them

Solution

Matrix multiplication is associative so there are multiple ways of performing the multiplication and therefore the number of operations (sum and multiplications) performed on scalars is different. Let’s suppose that the dimensions of the ![](1/images/00281.jpeg) matrix is contained in positions ![](1/images/00282.jpeg)  for a vector![](1/images/00283.jpeg).We can scan the vector and find a solution recursively.

Code

unsigned  int MatrixOrder(const std::vector<unsigned  int>&p,

int  i, int  j)

{

 if (i == j)

  return 0;

 unsigned  int min =

std::numeric_limits<unsigned  int>::max();

 unsigned  int res;

 for (int k = i; k <j; ++k)

 {

               res = MatrixOrder(p, i, k) +

MatrixOrder(p, k + 1, j) +

  p[i - 1] * p[k] * p[j];

 if (res < min)

                             min = res;

 }

 return min;

}

unsigned  int MatrixChainOrder(const std::vector<unsigned  int> & p)

{

 unsigned  int n = p.size();

 Matrix<unsigned  int> m(n, n);

 for (unsigned  int i = 0; i < n; ++i)

               m(i, i) = 0;

 unsigned  int j, cost;

 // len = 2,  1 <= i < n - 1 ; j = i + 1

 // len = 3,  1 <= i < n - 2;  j = i + 2

 //

 // len = n-2, i=1, i = 2 , j = i + n - 3

 // len = n-1, i=1        , j = n - 1

 for (unsigned  int len = 2; len < n; ++len)

  for (unsigned i = 1; i < n - len + 1; ++i)

               {

                             j = i + len - 1;

                             m(i, j) =

std::numeric_limits<unsigned  int>::max();

  for (unsigned  int k = i; k <= j - 1; ++k)

                             {

                                           cost = m(i, k) + m(k + 1, j) +

p[i - 1] * p[k] * p[j];

  if (cost < m(i, j)) {

                                                         m(i, j) = cost;

                                           }

                             }

               }

  return m(1, n - 1);

}

Complexity

Complexity is ![](1/images/00284.jpeg)

# 28.  Max Submatrix – Given a matrix of size n x n find the maximum sum rectangle

Solution

The problem is a natural generalization of the Kandane’s problem discussed previously. Suppose that we fix columns ![](1/images/00076.jpeg)  and![](1/images/00083.jpeg), then we can compute in linear time the top and bottom rows which maximize the rectangle.

Code

void findMaxSum(const  Matrix<int> & M)

{

 unsigned  int rows = M.dim1();

 unsigned  int columns = M.dim2();

 unsigned  int finalLeft, finalRight, finalUp, finalDown;

 int sum, start, stop, maxSum = std::numeric_limits<int>::min();

 for (unsigned  int left = 0; left < columns; ++left)

 {

               std::vector<int> temp(rows, 0);

  for (unsigned  int right = left; right < columns; ++right)

               {

  for (unsigned  int i = 0; i <rows; ++i)

 temp[i] += M(i, right);

                             sum = kadane(temp, start, stop);

 if (sum > maxSum)

                             {

                                           maxSum = sum;

                                           finalLeft = left; finalRight = right;

                                           finalUp = start; finalDown = stop;

                             }

               }

 }

 std::cout << "maxSum=" << maxSum <<

  " (Top, Left) (" << finalUp <<

  " ," << finalLeft <<

  ") (Bottom, Right) (" << finalDown <<

  "," << finalRight << ')' << std::endl;

}

Complexity

Complexity is ![](1/images/00285.jpeg) , because Kandane is linear.

# 29.  Given a Binary Search Tree, find the size of the largest independent set of nodes

Solution

A set of nodes in a tree is independent if there are no edges directly connecting them in a father-children relation. A dynamic programming solution is based on the consideration that a node can be either part of the largest independent set or not. In the former case the size of the largest set will be the sum of the largest set of grandchildren plus 1 because we skip the grandchildren’s father. In the latter case the size of the largest set is the sum of the largest set of children because by construction we do not add any new node to the set. Formally:

![](1/images/00286.jpeg)

If a node is null then![](1/images/00287.jpeg).For avoiding re-computing partial results we can store the LIS(x) inside the node X.

Code

template <typename  T>

struct  node

{

 T value;

 mutable  unsigned  int liss;

 struct  node* left, *right;

 node(T  v) : value(v), liss(0), left(NULL), right(NULL) {};

};

template <typename  T>

unsigned  int LargestIndipendentSet(const  node<T> * root)

{

 if (root == NULL)

  return 0;

 if (root->liss)

  return  root->liss;

 unsigned  int sizeWithThisNode = 1;

 if (root->left)

               sizeWithThisNode +=

               LargestIndipendentSet(root->left->left) +

               LargestIndipendentSet(root->left->right);

 if (root->right)

               sizeWithThisNode +=

               LargestIndipendentSet(root->right->left) +

               LargestIndipendentSet(root->right->right);

 unsigned  int sizeWithoutThisNode =

               LargestIndipendentSet(root->right) +

               LargestIndipendentSet(root->left);

 root->liss = std::max(sizeWithThisNode,

               sizeWithoutThisNode);

 return  root->liss;

}

Complexity

The total complexity is ![](1/images/00049.jpeg) where ![](1/images/00002.jpeg) is  the number of nodes in the binary search tree.

# 30.  Optimal Binary Tree – given a set S of tuples <k, freq[k]> , where k is an integer and freq[k] is the number of times that k has been observed, build a binary search three such that the total cost of all single searches is minimized

Solution

One key intuition is that the cost of accessing a key is ![](1/images/00288.jpeg) , where ![](1/images/00289.jpeg) is the depth of key![](1/images/00290.jpeg).  A tuple can be the root of the binary search tree (BST) provided that it respects the BST properties:

*   The left [subtree](http://en.wikipedia.org/wiki/Tree_(data_structure)#Subtree) of a node contains only nodes with keys less than the node's key
*   The right subtree of a node contains only nodes with keys greater than the node's key
*   For the left and right subtree: each one must also be a binary search tree
*   There must be no duplicate nodes

Therefore we can write the cost function for the keys in ![](1/images/00291.jpeg) as it follows:

![](1/images/00292.jpeg)

In other words: when the node ![](1/images/00293.jpeg) becomes a root and we need to minimize the cost of the left keys ![](1/images/00294.jpeg) and the right keys ![](1/images/00295.jpeg). In addition, all the nodes below the new root node will have an additional level of depth and therefore we need to sum all their frequencies. The code provided uses memorization for avoiding recomputation of the same values again and again. The solution is built bottom-up.

Code

int costBST_DP(const std::vector<unsigned  int> & freq)

{

 unsigned  int n = freq.size();

 Matrix<unsigned  int> cost(n, n);

 Matrix<unsigned  int> sumFreq(n, n);

 unsigned  int localCost;

 for (unsigned  int i = 0; i < n; ++i)

 cost(i, i) = freq[i];

 for (unsigned  int i = 0; i < n; ++i)

 for (unsigned  int j = i; j < n; ++j)

 {

               sumFreq(i, j) = 0;

  for (unsigned  int s = i; s <= j && s < n; ++s)

 sumFreq(i, j) += freq[s];

 }

 // range = 2 (0<=i<n-1) -> j=i+1 1<=j<=n-1

 // range = 3 (0<=i<n-2) -> j=i+2 0<=j<=n-1

 // range = n (i=0) -> j = n-1

 for (unsigned  int range = 2; range <= n; ++range)

 for (unsigned  int i = 0; i < n - range + 1; ++i)

 {

  unsigned  int j = i + range - 1;

               cost(i, j) = std::numeric_limits<unsigned  int>::max();

 for (unsigned  int k = i; k <= j; k++)

               {

                             localCost =

                                           ((k > i) ? cost(i, k - 1) : 0) +

                                           ((k < j) ? cost(k + 1, j) : 0) + sumFreq(i, j);

  if (localCost < cost(i, j))

                                           cost(i, j) = localCost;

               }

 }

 return cost(0, n - 1);

}

Complexity

The cost is ![](1/images/00296.jpeg) and space is ![](1/images/00212.jpeg)

# 31.  Boolean Parenthesization – given a Boolean expression of and, or, xor, true, false, find the number of ways to parenthesize and evaluate to true

Solution

Let ![](1/images/00297.jpeg) be the number of parenthesizations which are evaluated to true between positions ![](1/images/00076.jpeg) and![](1/images/00083.jpeg); and  ![](1/images/00298.jpeg)  be the number of parenthesization which are evaluated to false between positions ![](1/images/00076.jpeg) and![](1/images/00083.jpeg). Recursively

![](1/images/00299.jpeg)

Code

Left as exercise

Complexity

The running time is![](1/images/00300.jpeg), where ![](1/images/00002.jpeg) are the number of items in the expression.

# 32.  Games of Coins – a set of coins are aligned and two players can pick one coin from each side in turn. Maximize the value of the coins picked by the first player

Solution

Let suppose that the coins are represented in an array![](1/images/00301.jpeg). The value picked when the coins left are ![](1/images/00302.jpeg)must satisfy the recursive relation![](1/images/00303.jpeg):

![](1/images/00304.jpeg)

The key intuition is that the first player should select either coin ![](1/images/00305.jpeg) or coin ![](1/images/00306.jpeg) with the goal of maximizing his gain. For the sake of simplicity, let’s suppose he selects![](1/images/00307.jpeg): the other case is symmetric. We count ![](1/images/00308.jpeg) plus we aim at minimizing the value of the second player who can either pick another coin from the ![](1/images/00305.jpeg) side (position a+2) or pick a coin from the ![](1/images/00306.jpeg) side. The value is clearly 0 if![](1/images/00309.jpeg).

Code

Left as exercise

Complexity

There are ![](1/images/00310.jpeg) values for ![](1/images/00311.jpeg) and each single evaluation is ![](1/images/00312.jpeg), so the total run time is ![](1/images/00310.jpeg)

# 33.  Maximum value contiguous subsequence – given an array of real numbers, find a contiguous subsequence with max sum s

Solution

Let’s define ![](1/images/00313.jpeg)as the maximum value subsequence which ends at![](1/images/00093.jpeg). The element in position ![](1/images/00140.jpeg)can be either added or not. Recursively

![](1/images/00314.jpeg)

Code

Left as exercise

Complexity

There are ![](1/images/00239.jpeg)elements in ![](1/images/00106.jpeg) and the computing of each element requires to compute the maximum between two values. Therefore complexity is ![](1/images/00049.jpeg)

# 34.  Balanced partition – given an array of integers between 0 and M, divide the integers into two sets such that the difference of their sums is minimized

Solution

Let ![](1/images/00315.jpeg) , if the subset![](1/images/00316.jpeg)} sums to j. Recursively for the set of ![](1/images/00076.jpeg) elements we can start with a set of ![](1/images/00317.jpeg) elements and keep it as it is, or we can expand it by adding the element ![](1/images/00318.jpeg)

![](1/images/00319.jpeg)

Then considering the row ![](1/images/00320.jpeg) representing![](1/images/00321.jpeg)} we search the value![](1/images/00322.jpeg) such that ![](1/images/00323.jpeg) and the difference![](1/images/00324.jpeg) is minimized.

Code

Left as exercise

Complexity

There are ![](1/images/00002.jpeg) elements bounded by ![](1/images/00106.jpeg) while ![](1/images/00077.jpeg) needs to scan ![](1/images/00002.jpeg) elements. Therefore the complexity is ![](1/images/00325.jpeg)

# 35.  Scheduling – given n jobs, each one with a processing time ti a profit pi  and a deadline di, maximize the profit

Solution

Suppose that each job ![](1/images/00326.jpeg) has processing time ![](1/images/00327.jpeg) profit ![](1/images/00328.jpeg) and deadline ![](1/images/00329.jpeg) for ![](1/images/00330.jpeg) and that we get no profit, if the job is executed after its deadline. We want to maximize the profit ![](1/images/00331.jpeg) for ![](1/images/00330.jpeg) jobs executed at time![](1/images/00083.jpeg). Recursively,

![](1/images/00332.jpeg)

Code

Left as exercise

Complexity

If we assume that the processing time is bounded by![](1/images/00333.jpeg), then we need to compute ![](1/images/00077.jpeg) up to ![](1/images/00334.jpeg) and we have ![](1/images/00002.jpeg) jobs to consider. Therefore the total complexity is ![](1/images/00335.jpeg)

# 36.  Stock prices – Given a histogram array of unsigned integers encoding the price of a stock title during the previous year, compute the area for the largest rectangle contained in this histogram

Solution

Let A be the histogram array, we need to compute

![](1/images/00336.jpeg))

The most naïve implementation has complexity![](1/images/00337.jpeg). However we can achieve complexity![](1/images/00338.jpeg) by processing each element ![](1/images/00330.jpeg) and looking for the largest rectangle with height being at least![](1/images/00339.jpeg). Complexity can be further improved by considering that if we have ![](1/images/00340.jpeg)and ![](1/images/00341.jpeg) , then we can immediately discard ![](1/images/00342.jpeg) when processing the ![](1/images/00281.jpeg)entry and this can be efficiently achieved by using a stack.

Code

unsigned  int largestRectangle(

   const std::vector<unsigned  int> & H)

{

              std::stack<unsigned  int> stk;

 std::vector<unsigned  int> left;

 for (unsigned  int i = 0; i < H.size(); ++i)

 {

  while (!stk.empty() && H[stk.top()] > H[i])

                             stk.pop();

               stk.push(i);

               left.push_back(stk.empty() ? -1 : stk.top());

 }

 while (!stk.empty()) { stk.pop(); }

              std::vector<unsigned  int> right(H.size());

 for (int i = H.size() - 1; i >= 0; --i)

 {

  while (!stk.empty() && H[stk.top()] > H[i])

                             stk.pop();

 right[i] = stk.empty() ? H.size() : stk.top();

               stk.push(i);

 }

 unsigned  int maxArea = 0;

 for (unsigned  int i = 0; i < H.size(); ++i)

 {

               maxArea =

std::max(maxArea, H[i] * (right[i] - left[i] - 1));

 }

 return maxArea;

}

Complexity

Code runs in![](1/images/00338.jpeg).

# 37.  Ship Battle – Given a matrix M and an array V, match the array in the matrix

Solution

Let ![](1/images/00106.jpeg) be the matrix of size![](1/images/00343.jpeg), and ![](1/images/00227.jpeg) the array of size![](1/images/00344.jpeg). We can scan the matrix by rows ![](1/images/00330.jpeg) and by columns ![](1/images/00345.jpeg) and if ![](1/images/00346.jpeg)  , with vector at position![](1/images/00347.jpeg), we can recursively check, if there is a match for the eight positions adjacent to ![](1/images/00291.jpeg) with![](1/images/00348.jpeg).  Particular attention must be put for the corner cases as explained in the code. If we cache the situations where the match does not happen for tuples ![](1/images/00349.jpeg) , we can obtain complexity ![](1/images/00350.jpeg)

Code

// (i, j, k) -> v

typedef  Tensor<unsigned  int, unsigned  int,

unsigned  int, bool> Cache;

bool matchHelper(const  Matrix<int> &m,

 const std::vector<int> &v,

 Cache & doNot,

 int  i,

 int  j,

 unsigned  int  len)

{

//              std::cout << " matchHelper i=" << i

<< " j=" << j << " len=" << len << std::endl;

 if (v.size() == len)

  return  true;

if (i < 0 || i >= (int)m.dim1() ||

j < 0 || j >= (int)m.dim2() || doNot.exist(i, j, len))

  return  false;

if ((m(i, j) == v[len]) &&

               (matchHelper(m, v, doNot,

  i - 1, j, len + 1) || /* horizontal */

               matchHelper(m, v, doNot,

  i + 1, j, len + 1) || /* horizontal */

               matchHelper(m, v, doNot,

  i, j - 1, len + 1) || /* vertical */

               matchHelper(m, v, doNot,

  i, j + 1, len + 1) || /* vertical */

                            matchHelper(m, v, doNot,

  i - 1, j - 1, len + 1) || /* diagonal */

               matchHelper(m, v, doNot,

  i - 1, j + 1, len + 1) || /* diagonal */

               matchHelper(m, v, doNot,

  i + 1, j - 1, len + 1) || /* diagonal */

               matchHelper(m, v, doNot,

  i + 1, j + 1, len + 1) /* diagonal */

               ))

  return  true;

 doNot(i, j, len) = true;

  return  false;

}

bool matchVectorInMatrix(const  Matrix<int> & m,

const std::vector<int> & v)

{

 Cache c;

 for (unsigned  int i = 0; i < m.dim1(); ++i)

  for (unsigned  int j = 0; j < m.dim2(); ++j)

  if (matchHelper(m, v, c, i, j, 0))

  return  true;

 return  false;

}

Complexity

Code runs in![](1/images/00351.jpeg).

# Appendix

This appendix contains two support classes defined for solving a certain number of problems

Graph class

#include  <forward_list>

typedef  unsigned  int  nodeID;

typedef  int  weight;

struct  Edge

{

 nodeID v;

 weight w;

              Edge(nodeID  d, weight  wt) : v(d), w(wt) {};

};

typedef std::forward_list<Edge> edgesList; // list of edges leaving a node

typedef std::vector<edgesList> Edges;

class  Graph

{

public:

 // allocate |V| lists of edges

 Graph(unsigned  int  V) : _V(V), _E(0), _edges(new  Edges(V)) {};

 ~Graph(){ delete _edges; };

 void addEdge(nodeID  v1, nodeID  v2, weight  w)

 {

  if (v1 > _V || v2 > _V) return;

  Edge e(v2, w);

               (*_edges)[v1].push_front(e);

               _E++;

 }

 void addNode()

 {

  edgesList el;

               _edges->push_back(el);

               _V++;

 }

 edgesList & edges(nodeID  v) const { return (*_edges)[v]; };

 unsigned  int numNodes() const { return _V; };

 unsigned  int numEdges() const { return _E; };

private:

 unsigned  int _V, _E;

 Edges * _edges;

};

std::ostream & operator << (std::ostream & os,

const  Graph & g)

{

 for (nodeID u = 0; u < g.numNodes(); u++)

 {

  os << " node=" << u << std::endl;

  for (auto  const & e : g.edges(u))

  os << " ->" << e.v << " w=" << e.w << std::endl;

 }

 return  os;

}

Matrix class

template<typename  T>

class  Matrix

{

public:

 Matrix(const  Matrix&) = delete;

 Matrix& operator=(const  Matrix&) = delete;

              Matrix(unsigned  int  dim1, unsigned  int  dim2)

               : _M(new  T*[dim1]), _dim1(dim1), _dim2(dim2)

 {

  for (unsigned  int i = 0; i < dim1; ++i)

 _M[i] = new  T[dim2];

 }

 Matrix(unsigned  int  dim1, unsigned  int  dim2,

T  defaultValue)

 : Matrix(dim1, dim2)

 {

  for (unsigned  int i = 0; i < _dim1; ++i)

  for (unsigned  int j = 0; j < _dim2; ++j)

 _M[i][j] = defaultValue;

 }

              Matrix(Matrix&& aMatrix) {

 _dim1 = aMatrix._dim1;

 _dim2 = aMatrix._dim2;

 _M = aMatrix._M;

  aMatrix._dim1 = 0;

  aMatrix._dim2 = 0;

  aMatrix._M = nullptr;

 }

              ~Matrix()

 {

  for (unsigned  int i = 0; i < _dim1; ++i)

  delete[] _M[i];

  delete[] _M;

 }

 T & operator()(const  unsigned  int  i, const  unsigned  int  j)

 {

  return _M[i][j];

 }

 T & operator()(const  unsigned  int  i, const  unsigned  int  j) const

 {

  return _M[i][j];

 }

 unsigned  int dim1() const { return _dim1; };

 unsigned  int dim2() const { return _dim2; };

 friend std::ostream & operator <<(std::ostream & out,

const  Matrix<T>& m)

 {

  for (unsigned  int i = 0; i < m._dim1; ++i){

  for (unsigned  int j = 0; j < m._dim2; ++j)

  out << m._M[i][j] << ' ';

  out << std::endl;

               }

  return  out;

 }

 void swap(Matrix & other)

 {

 std::swap(_M, other._M);

 std::swap(_dim1, other._dim1);

 std::swap(_dim2, other._dim2);

 }

private:

 T** _M;

 unsigned  int _dim1, _dim2;

};

Tensor class

#include  <functional>

#include  <unordered_map>

template <typename  T1, typename  T2, typename  T3, typename  V>

class  Tensor

{

public:

 V & operator()(const  T1  i, const  T2  j, const  T3  k)

 {

  Point p(i, j, k);

  return _M[p];

 }

 V & operator()(const  T1  i, const  T2  j, const  T3  k)const

 {

  Point p(i, j, k);

  return _M[p];

 }

 bool exist(const  T1  i, const  T2  j, const  T3  k) const

 {

  Point p(i, j, k);

  return (_M.find(p) != _M.cend());

 }

 void swap(Tensor<T1, T2, T3, V> & other)

 {

 std::swap(_M, other._M);

 }

 Tensor & operator = (Tensor<T1, T2, T3, V> & other)

 {

               swap(other);

  return *this;

 }

 friend std::ostream & operator <<(std::ostream & out,

  const  Tensor<T1, T2, T3, V>& ts)

 {

  for (const  auto & p : ts._M)

 std::cout << "(" << p.first.i << "," <<

p.first.j << "," << p.first.k << ")=" <<

p.second << std::endl;

 return  out;

 }

private:

 struct  Point

 {

  T1 i; T2 j; T3 k;

               Point(T1  p, T2  q, T3  r) : i(p), j(q), k(r) {};

 bool operator == (const  Point & right) const

               {

  return (i == right.i) & (j == right.j) &

 (k == right.k);

               }

 };

 struct  hashPoint

 {

  size_t operator() (const  Point & p) const

               {

  return std::hash<T1>()(p.i) ^

std::hash<T2>()(p.j) ^

std::hash<T3>()(p.k);

               }

 };

              std::unordered_map<Point, V, hashPoint> _M;

};

ABOUT THE AUTHOR

An experienced data mining engineer, passionate about technology and innovation in consumers’ space. Interested in search and machine learning on massive dataset with a particular focus on query analysis, suggestions, entities, personalization, freshness and universal ranking. Antonio Gullì has worked in small startups, medium (Ask.com, Tiscali) and large corporations (Microsoft). His carrier path is about mixing industry with academic experience.

“Nowadays, you must have a great combination of research skills and a just-get-it-done attitude.”

* * *

[[1]](#part0000.html__ftnref1)  [http://en.wikipedia.org/wiki/Kadane%27s_algorithm](http://en.wikipedia.org/wiki/Kadane%27s_algorithm)

[[2]](#part0000.html__ftnref2)  [http://en.wikipedia.org/wiki/Catalan_number](http://en.wikipedia.org/wiki/Catalan_number)

[[3]](#part0000.html__ftnref3)  [http://en.wikipedia.org/wiki/Longest_common_substring_problem](http://en.wikipedia.org/wiki/Longest_common_substring_problem)

[[4]](#part0000.html__ftnref4)  [http://en.wikipedia.org/wiki/Longest_increasing_subsequence](http://en.wikipedia.org/wiki/Longest_increasing_subsequence)

[[5]](#part0000.html__ftnref5)  [http://en.wikipedia.org/wiki/Subset_sum_problem](http://en.wikipedia.org/wiki/Subset_sum_problem)

[[6]](#part0000.html__ftnref6)  [http://en.wikipedia.org/wiki/Bellman-Ford_algorithm](http://en.wikipedia.org/wiki/Bellman-Ford_algorithm)

A collection of Graph Programming Interview Questions Solved in C++

Antonio Gulli

Copyright © 2015 Antonio Gulli

All rights reserved.

ISBN:

ISBN-13:

“Graph” is the second of a series of 25 Chapters devoted to algorithms, problem solving and C++ programming.

DEDICATION

To my father Elio and my mother Maria.

For your priceless help during all my life

ACKNOWLEDGMENTS

Thanks to Gaetano Mendola  for code reviewing

Table of Contents

[1 Implementing a direct graph](#part0000_split_005.html__Toc415584877)

[Solution](#part0000_split_005.html__Toc415584878)

[Code](#part0000_split_005.html__Toc415584879)

[2 Choosing matrices or adjacency lists](#part0000_split_006.html__Toc415584880)

[Solution](#part0000_split_006.html__Toc415584881)

[3 Implementing a BFS visit](#part0000_split_007.html__Toc415584882)

[Solution](#part0000_split_007.html__Toc415584883)

[Code](#part0000_split_007.html__Toc415584884)

[Complexity](#part0000_split_007.html__Toc415584885)

[4 Erdős number](#part0000_split_008.html__Toc415584886)

[5 Implementing a DFS visit](#part0000_split_009.html__Toc415584887)

[Solution](#part0000_split_009.html__Toc415584888)

[Code](#part0000_split_009.html__Toc415584889)

[Complexity](#part0000_split_009.html__Toc415584890)

[6 How to detect a cycle in a graph](#part0000_split_010.html__Toc415584891)

[Solution](#part0000_split_010.html__Toc415584892)

[Code](#part0000_split_010.html__Toc415584893)

[Complexity](#part0000_split_010.html__Toc415584894)

[7 Given two nodes in an undirected graph, find the path connecting them](#part0000_split_011.html__Toc415584895)

[Solution](#part0000_split_011.html__Toc415584896)

[Code](#part0000_split_011.html__Toc415584897)

[Complexity](#part0000_split_011.html__Toc415584898)

[8 Solving mazes](#part0000_split_012.html__Toc415584899)

[Solution](#part0000_split_012.html__Toc415584900)

[9 Given a direct acyclic graph, implement a topological sort](#part0000_split_013.html__Toc415584901)

[Solution](#part0000_split_013.html__Toc415584902)

[Code](#part0000_split_013.html__Toc415584903)

[Complexity](#part0000_split_013.html__Toc415584904)

[10 Detecting a bipartite graph](#part0000_split_014.html__Toc415584905)

[Solution](#part0000_split_014.html__Toc415584907)

[Code](#part0000_split_014.html__Toc415584908)

[Complexity](#part0000_split_014.html__Toc415584909)

[11 Given a connected graph, compute the minimum spanning tree (MST)](#part0000_split_015.html__Toc415584910)

[Solution](#part0000_split_015.html__Toc415584911)

[Code](#part0000_split_015.html__Toc415584912)

[\](#part0000_split_015.html__Toc415584913)

[12](#part0000_split_016.html__Toc415584914)

[13 Find the strongly connected components in a direct graph](#part0000_split_017.html__Toc415584915)

[Solution](#part0000_split_017.html__Toc415584916)

[Code](#part0000_split_017.html__Toc415584917)

[Complexity](#part0000_split_017.html__Toc415584918)

[14 Covering DFS Trees](#part0000_split_018.html__Toc415584919)

[15 Find an Hamiltonian cycle](#part0000_split_019.html__Toc415584920)

[Solution](#part0000_split_019.html__Toc415584921)

[Code](#part0000_split_019.html__Toc415584922)

[16 Find the articulation points in a graph](#part0000_split_020.html__Toc415584923)

[Solution](#part0000_split_020.html__Toc415584924)

[Code](#part0000_split_020.html__Toc415584925)

[Complexity](#part0000_split_020.html__Toc415584926)

[17 Find the shortest path in a graph with non-negative edge weight](#part0000_split_021.html__Toc415584927)

[Solution](#part0000_split_021.html__Toc415584928)

[Code](#part0000_split_022.html__Toc415584929)

[Complexity](#part0000_split_022.html__Toc415584930)

[18 Find MST(Minimum Spanning Tree) using Kruskal Algorithm](#part0000_split_023.html__Toc415584931)

[Solution](#part0000_split_023.html__Toc415584932)

[Complexity](#part0000_split_023.html__Toc415584933)

[19 Find the longest path in a DAG](#part0000_split_024.html__Toc415584934)

[Solution](#part0000_split_024.html__Toc415584935)

[Code](#part0000_split_024.html__Toc415584936)

[Complexity](#part0000_split_024.html__Toc415584937)

[20 Find MST (Minimum Spanning Tree) using Prim Algorithm](#part0000_split_025.html__Toc415584938)

[Solution](#part0000_split_025.html__Toc415584939)

[Complexity](#part0000_split_025.html__Toc415584940)

[21 Find all pairs shortest paths using the Floyd-Warshall Algorithm](#part0000_split_026.html__Toc415584941)

[Solution](#part0000_split_026.html__Toc415584942)

[Complexity](#part0000_split_026.html__Toc415584943)

[22 Find all the single source shortest paths using Bellman Ford Algorithm](#part0000_split_027.html__Toc415584944)

[Solution](#part0000_split_027.html__Toc415584945)

[Complexity](#part0000_split_027.html__Toc415584946)

[23 Independent set of intervals](#part0000_split_028.html__Toc415584947)

[Solution](#part0000_split_028.html__Toc415584948)

[Complexity](#part0000_split_028.html__Toc415584949)

[24 Dominant set of intervals](#part0000_split_029.html__Toc415584950)

[Solution](#part0000_split_029.html__Toc415584951)

[Complexity](#part0000_split_029.html__Toc415584952)

[25 Weighted dominant set of intervals](#part0000_split_030.html__Toc415584953)

[Solution](#part0000_split_030.html__Toc415584954)

[26 Weighted shortest paths with cost associated to the nodes](#part0000_split_031.html__Toc415584955)

[Solution](#part0000_split_031.html__Toc415584956)

[27 Find the flow network using Ford–Fulkerson’Algorithm](#part0000_split_032.html__Toc415584957)

[Solution](#part0000_split_032.html__Toc415584958)

[Complexity](#part0000_split_032.html__Toc415584959)

[28 Assignment matching problem](#part0000_split_033.html__Toc415584960)

[Solution](#part0000_split_033.html__Toc415584961)

[29 Find an Eulerian circuit](#part0000_split_034.html__Toc415584962)

[Solution](#part0000_split_034.html__Toc415584963)

[Code](#part0000_split_034.html__Toc415584964)

[Complexity](#part0000_split_034.html__Toc415584965)

[30 Scheduling](#part0000_split_035.html__Toc415584966)

[Solution](#part0000_split_035.html__Toc415584967)

[Complexity](#part0000_split_035.html__Toc415584968)

## 1  Implementing a direct graph

A graph data structure ![](2/images/00001.jpeg) involves a finite set of nodes or vertices ![](2/images/00002.jpeg) and a set of ordered pairs ![](2/images/00003.jpeg) called edges or arcs connecting two nodes. A graph might have labels associated to the nodes and/or to the edges, thus denoting different attributes (such as names, costs, capacity, length, colours). A direct graph is a graph where the edges are associated to a direction, which is typically represented with an arrow.

 ![](2/images/00004.jpeg)![](2/images/00005.jpeg)

![](2/images/00006.jpeg) ![](2/images/00007.jpeg)

### Solution

The first direct graph implementation represents a node and an edge as a C++ struct. In addition a collection of nodes is memorized in a ![](2/images/00008.jpeg) and all the edges originating from each node are memorized in a![](2/images/00009.jpeg). This representation is known as Adjacency list. In this particular implementation each node has a unique identifier NodeID, a label NodeWeight and another label representing the name of the node.  Indeed each edge stores the destination NodeID, a label EdgeWeightI representing the weight of the edge and another label representing the name of the edge.

The second direct graph implementation represents a Graph using a matrix of size ![](2/images/00010.jpeg) where n is the number of nodes. This representation is known ad Adjacency Matrix.

### Code

const std::string emptyString;

//

// Direct Graph

// with Adjacent lists

class  Graph

{

public:

 typedef  unsigned  int  NodeID;

 typedef  unsigned  int  EdgeID;

 typedef  int  NodeWeight;

 typedef  int  EdgeWeight;

 struct  Edge

              {

                            Edge(NodeID  nid, EdgeWeight  wt,

 const std::string & lb)

                            : v(nid), w(wt), label(lb)  {};

 const  NodeID v;

 const  EdgeWeight w;

 const std::string label;

              };

 struct  Node

              {

                            Node(NodeWeight  wt, const std::string & l) :

                                          w(wt), label(l){};

 NodeWeight w;

                            std::string label;

              };

 // all nodes

 typedef std::vector<Node> Nodes;          

 // edges from a node

 typedef std::forward_list<Edge> EdgesList;

 // all edges (id -> edgeList)

 typedef std::vector<EdgesList> Edges;     

 // allocate |V| lists of edges

              Graph(NodeID  V = 0, EdgeID  E = 0)

              {

 if (V)

                            {

                                          _nodes.reserve(V); _outdegree.reserve(V);

                            }

 if (E)

                                          _edges.reserve(E);

              };

 void reserveNodes(NodeID  n)

              { _nodes.reserve(n); _outdegree.reserve(n); }

 void reserveEdges(EdgeID  n)

              { _edges.reserve(n); }

 //

 // we can have multiple edge (v1, v2)

 void addEdge(NodeID  v1,

 NodeID  v2,

 EdgeWeight  w = 0,

 const std::string & label = emptyString)

              {

 if (v1 > _nodes.size() || v2 > _nodes.size())

return;

 Edge e(v2, w, label);

                            _edges[v1].push_front(e);

                            _outdegree[v1]++;

              }

 //

 // nodes are unique

 void addNode(NodeWeight  w = 0,

 const std::string & label = emptyString)

              {

 EdgesList el;

 Node n(w, label);

_nodes.push_back(n); // another node

_edges.push_back(el); // with its EdgeList

                            _outdegree.push_back(0);

              }

 const  EdgesList & edges(NodeID  v) const

{ return _edges[v]; };

 Graph::NodeID outdegree(NodeID  v) const

{ return _outdegree[v]; }

 const  Nodes & nodes() const

{ return _nodes; };

 NodeID numNodes() const

{ return _nodes.size(); };

 EdgeID numEdges() const

{ return _edges.size(); };

private:

 Edges  _edges;

 Nodes  _nodes;

              std::vector<Graph::NodeID> _outdegree;

              Graph(const  Graph& g) = delete;

 Graph& operator=(const  Graph& g) = delete;

};

std::ostream & operator << (std::ostream & os,

 const  Graph & g)

{

 Graph::NodeID id = 0;

 for (const  auto & n : g.nodes())

              {

 os << " node=" << id << " weight=" << n.w <<

 " label=" << n.label << std::endl;

 for (const  auto & e : g.edges(id))

 os << " ->" << e.v << " w=" << e.w <<

 " label=" << n.label

<< " lableEdge=" << e.label << std::endl;

                            ++id;

              }

 return  os;

}

//

// Undirect Graph

// with Adjacency Matrix

template<typename  T>

class  Matrix

{

public:

              Matrix(const  Matrix&) = delete;

 Matrix& operator=(const  Matrix&) = delete;

              Matrix(unsigned  int  dim1, unsigned  int  dim2)

                            : _M(new  T*[dim1]), _dim1(dim1), _dim2(dim2)

              {

 for (unsigned  int i = 0; i < dim1; ++i)

_M[i] = new  T[dim2];

              }

              Matrix(unsigned  int  dim1, unsigned  int  dim2,

 T  defaultValue)

: Matrix(dim1, dim2)

              {

 for (unsigned  int i = 0; i < _dim1; ++i)

 for (unsigned  int j = 0; j < _dim2; ++j)

_M[i][j] = defaultValue;

              }

              Matrix(Matrix&& aMatrix) {

_dim1 = aMatrix._dim1;

_dim2 = aMatrix._dim2;

_M = aMatrix._M;

 aMatrix._dim1 = 0;

 aMatrix._dim2 = 0;

 aMatrix._M = nullptr;

              }

              ~Matrix()

              {

 for (unsigned  int i = 0; i < _dim1; ++i)

 delete[] _M[i];

 delete[] _M;

              }

 T & operator()(const  unsigned  int  i,

 const  unsigned  int  j)

              {

 return _M[i][j];

              }

 T & operator()(const  unsigned  int  i,

 const  unsigned  int  j) const

              {

 return _M[i][j];

              }

 unsigned  int dim1() const { return _dim1; };

 unsigned  int dim2() const { return _dim2; };

 friend std::ostream & operator <<(std::ostream & out,

 const  Matrix<T>& m)

              {

 for (unsigned  int i = 0; i < m._dim1; ++i){

 for (unsigned  int j = 0; j < m._dim2; ++j)

 out << m._M[i][j] << ' ';

 out << std::endl;

                            }

 return  out;

              }

 void swap(Matrix & other)

              {

std::swap(_M, other._M);

std::swap(_dim1, other._dim1);

std::swap(_dim2, other._dim2);

              }

private:

 T** _M;

 unsigned  int _dim1, _dim2;

};

//

// MatrixGraph

class  MatrixGraph{

 MatrixGraph& operator=(const  MatrixGraph&) = delete;

public:

 typedef  unsigned  int  NodeID;

 typedef  int  weight;

              MatrixGraph(NodeID  numNodes)

                            : n(numNodes)

              {

M = new  weight*[n];

 for (NodeID i = 0; i < n; ++i)

                            {

M[i] = new  weight[n];

 for (NodeID j = 0; j < n; ++j)

                                                        M[i][j] = 0;

                            }

              }

              ~MatrixGraph()

              {

 for (NodeID i = 0; i < n; ++i)

 delete[] M[i];

 delete[] M;

              }

              MatrixGraph(const  MatrixGraph& m)

              {

n = m.getNumNodes();

M = new  weight*[n];

 for (NodeID i = 0; i < n; ++i)

                            {

M = new  weight*[n];

memcpy(M[i], m.M[i], sizeof(int)*n);

                            }

              }

 NodeID size() const { return n; }

 const  weight & operator()(NodeID  i, NodeID  j) const

{ return M[i][j]; }

 weight & operator()(NodeID  i, NodeID  j)

{ return M[i][j]; }

 NodeID getNumNodes() const { return n; }

private:

 NodeID n;

 weight **M;

};

std::ostream& operator << (std::ostream & os, const  MatrixGraph & g)

{

 for (MatrixGraph::NodeID i = 0; i < g.size(); ++i){

 for (MatrixGraph::NodeID j = 0;

j < g.size(); ++j)

 os << g(i, j) << ' ';

 os << std::endl;

              }

 return  os;

}

void test()

{

 Graph G;

G.addNode(10, "donald duck");

G.addNode(1, "daisy duck");

G.addNode(1, "antonio");

G.addNode(1, "milena");

G.addNode(1, "lorena");

G.addNode(1, "mambo");

G.addNode(1, "salsa");

G.addNode(1, "adriana");

              G.addEdge(0, 2);

G.addEdge(1, 2, 10, "important");

              G.addEdge(1, 3);

              G.addEdge(2, 3);

              G.addEdge(2, 5);

              G.addEdge(2, 6);

              G.addEdge(4, 5);

              G.addEdge(5, 5);

              G.addEdge(5, 4);

              G.addEdge(5, 100);

              std::cout << G;

MatrixGraph mgA(5);

              mgA(0, 1) = 3;  mgA(1, 2) = 2; mgA(1, 3) = 2;

              mgA(2, 3) = mgA(3, 4) = 1;  mgA(4, 0) = 1;

              std::cout << mgA;

}

## 2  Choosing matrices or adjacency lists

Let us assume that we have a direct graph ![](2/images/00011.jpeg) with ![](2/images/00012.jpeg) nodes and ![](2/images/00013.jpeg)edges and that every pointer takes ![](2/images/00014.jpeg) bits, when is it more appropriate to use a matrix and when is it better to use adjacency lists to represent the graph?

### Solution

The matrix needs ![](2/images/00015.jpeg) bits, while the adjacency lists need ![](2/images/00016.jpeg) pointers for each starting list of ![](2/images/00017.jpeg) bits and ![](2/images/00018.jpeg) cells of ![](2/images/00019.jpeg) bits (![](2/images/00020.jpeg) for the pointer to the next cell and an additional ![](2/images/00021.jpeg) for the pointer to the node). Therefore combining all the information, we need to solve in ![](2/images/00022.jpeg) the formula ![](2/images/00023.jpeg)

## 3 Implementing a BFS visit

Breadth-first-Search (BFS) is a visiting strategy for a graph where a node is first visited and then all adjacent nodes are visited in turn.

### Solution

This is a classical interview question which can be implemented by using a simple queue. At the beginning the root node is enqueued and marked as visited. Then a node is dequeued and all the adjacent nodes not yet visited are enqueued for future visit in turn. The process is repeated until the queue is empty.

### Code

void bfs(const  Graph & g, Graph::NodeID  nid)

{

 // queue of visited nodes

              std::deque<Graph::NodeID> queue;       

 // bfs on unknown node

 if (nid >= g.numNodes())                                         

 return;

              std::vector<bool> visited(g.numNodes(), false);

              visited[nid] = true;

              queue.push_back(nid);

std::cout << "Start bfs" << std::endl;

 while (!queue.empty())

              {

 const  Graph::NodeID id = queue.front();

                            queue.pop_front();

std::cout << "Visited: " << id << std::endl;

 for (const  auto & e : g.edges(id))

                            {

 if (!visited[e.v])

                                          {

visited[e.v] = true;

                                                        queue.push_back(e.v);

                                          }

                            }

              }

std::cout << "End bfs" << std::endl << std::endl;

}

### Complexity

Space complexity is ![](2/images/00024.jpeg) for the queue and ![](2/images/00025.jpeg), if the graph is represented using an adjacency list, or ![](2/images/00026.jpeg) if an adjacency matrix is adopted. Time complexity is ![](2/images/00027.jpeg) , where ![](2/images/00028.jpeg) may vary between ![](2/images/00029.jpeg) and ![](2/images/00030.jpeg)) , depending on how sparse the graph is.

## 4   Erdős number

Paul Erdős is a famous mathematician who wrote more than 1500 scientific articles. His direct co-authors have distance 1 from him, while their respective co-authors have distance 2. Recursively, whoever has a collaboration with authors at distance ![](2/images/00031.jpeg)from Erdős will therefore be at distance ![](2/images/00032.jpeg) (also denoted as Erdős (author)=K). The author of this book has Erdős (“Antonio Gulli”)=3 because he wrote a paper with “Fabrizio Sebastiani” who, in turn, wrote a paper with “Micheal Anthony Steel”, who is a direct co-author of Erdős.  Erdős numbers can be computed with a slight variation of the BFS visit and this implementation is left as an exercise.

## 5  Implementing a DFS visit

Depth-first-Search (DFS) is a visiting strategy for a graph, where the visit starts from a selected root node and the exploration is run as far as possible along each branch before backtracking to the first not yet visited children.

### Solution

This is another classical interview question which can be solved by using either recursion or iteration.

The dfs method implements a recursive solution which starts from the root node sid and it keeps a boolean vector of visited nodes and their colours. For each node the colour is ‘w’ (white) at the very beginning, ‘g’ (gray) when the node is visitedand ‘b’ (black) when all the adjacent nodes are also visited.  In addition the time, when the node is visited, is stored in the vector timing.

The dfsStack method implements an iterative solution where the root node is inserted in the stack. Then the top of the stack is removed and all the adjacent not yet visited nodes are put on the stack itself. The process is repeated until the stack is empty.

### Code

void dfsUtilRich(const  Graph & g, Graph::NodeID  sid,

              std::vector<bool> & visited,

              std::vector<Graph::NodeID> & colour,

              std::vector<Graph::NodeID> & timing,

 unsigned  int & time)

{

std::cout << "Starting dfsUtilRich on " <<

 sid << std::endl;

 visited[sid] = true;

 colour[sid] = 'g'; // gray

              ++time;

 timing[sid] = time;

 for (const  auto & e : g.edges(sid))

 if (!visited[e.v])

                            dfsUtilRich(g, e.v, visited, colour, timing, time);

 colour[sid] = 'b'; //black

              ++time;

}

void dfs(const  Graph & g, Graph::NodeID  sid)

{

 if (sid >= g.numNodes()) // dfs on unknown node

 return;

 unsigned  int time = 0;

              std::vector<bool> visited(g.numNodes(), false);

 // white

              std::vector<Graph::NodeID> colour(g.numNodes(), 'w');

              std::vector<Graph::NodeID> timing(g.numNodes(), 0);

              visited[sid] = true;

std::cout << "Starting dfs on " <<

 sid << std::endl;

 for (const  auto & e : g.edges(sid))

              {

 if (!visited[e.v])

                            {

visited[e.v] = true;

                                          dfsUtilRich(g, e.v, visited,

                                                        colour, timing, time);

                            }

              }

std::cout << "End dfs" << std::endl << std::endl;

}

void dfsStack(const  Graph & g, Graph::NodeID  sid)

{

 if (sid >= g.numNodes()) // dfs on unknown node

 return;

              std::stack<Graph::NodeID> nodesToBeVisited;

              std::vector<bool> visited(g.numNodes(), false);

              visited[sid] = true;

              nodesToBeVisited.push(sid);

std::cout << "Starting dfs on " << sid << std::endl;

 while (!nodesToBeVisited.empty())

              {

 const  Graph::NodeID nid = nodesToBeVisited.top();

 bool myFullExploredNode = true;

 for (const  auto & e : g.edges(nid))

                            {

 if (!visited[e.v])

                                          {

visited[e.v] = true;

                                                        nodesToBeVisited.push(e.v);

std::cout << "Visited: " << e.v << std::endl;

myFullExploredNode = false;

 break;

                                          3}

                            }

 if (myFullExploredNode)

                                          nodesToBeVisited.pop();

              }

std::cout << "End dfs" << std::endl << std::endl;

}

### Complexity

Space complexity is ![](2/images/00033.jpeg) for the stack and ![](2/images/00034.jpeg), if the graph is represented using an adjacency list or ![](2/images/00035.jpeg) if an adjacency matrix is adopted. Time complexity is ![](2/images/00036.jpeg), where ![](2/images/00037.jpeg) may vary between ![](2/images/00038.jpeg) and ![](2/images/00039.jpeg) , depending on how sparse the graph is.

## 6  How to detect a cycle in a graph

### Solution

A DFS visit can detect a cycle, if there is a back edge during the visit of the graph. By using the notation defined in the above solution, this condition is represented by a transition from a grey node to a grey node.

### Code

This implementation is left as an exercise.

### Complexity

The complexity here is the same as DFS.

## 7  Given two nodes in an undirected graph, find the path connecting them 

### Solution

A simple solution is to visit the graph with DFS order starting from one of the two nodes and stopping the visit as soon as the other node is found. During this process the visited nodes are stored into a stack. At the end the stack will contain the desired path.

### Code

This implementation is left as an exercise.

### Complexity

The complexity is the same as DFS.

## 8  Solving mazes

Let’s suppose to have a maze as the one represented in this figure. What is the best way to find the exit?

![http://upload.wikimedia.org/wikipedia/commons/thumb/9/9d/MAZE_40x20_DFS_no_deadends.png/220px-MAZE_40x20_DFS_no_deadends.png](2/images/00040.gif)

### Solution

The interested reader can think about how to represent the maze with a graph ![](2/images/00041.jpeg) and what the most appropriate visiting strategies on ![](2/images/00042.jpeg) are.

## 9  Given a direct acyclic graph, implement a topological sort

A topological sort of a [directed graph](http://en.wikipedia.org/wiki/Directed_graph) is a linear ordering of its [vertices](http://en.wikipedia.org/wiki/Vertex_(graph_theory)) such that for every directed edge ![](2/images/00043.jpeg) from vertex ![](2/images/00044.jpeg) to vertex ![](2/images/00045.jpeg) comes before ![](2/images/00046.jpeg) in the ordering. A topological ordering is possible, if and only if the graph has no directed cycles. Such graphs are called “directed acyclic graphs” (DAG). 

### Solution

Given a DAG, the topological sort is obtained by visiting the nodes with a BFS and storing the nodes into a stack stk. At the end of the process the stack will contain the topologically sorted nodes. The interested reader should modify the code in order to verify the presence of cycles, if the graph is not a DAG (left as exercise).

### Code

void topologicalSortUtil(const  Graph & g,

 Graph::NodeID  sid,

              std::vector<bool> & visited,

              std::stack<Graph::NodeID> &stk)

{

 visited[sid] = true;

std::cout << "\t topologicalSortUtil"

<< sid << std::endl;

 for (const  auto & e : g.edges(sid))

 if (!visited[e.v])

                            topologicalSortUtil(g, e.v, visited, stk);

 stk.push(sid);

}

void topologicalSort(const  Graph & g)

{

              std::vector<bool> visited(g.numNodes(), false);

              std::stack<Graph::NodeID> stk;

 for (Graph::NodeID nid = 0; nid < g.numNodes(); ++nid)

 if (!visited[nid])

                            topologicalSortUtil(g, nid, visited, stk);

std::cout << "topologicalSort" << std::endl;

 while (!stk.empty())

              {

                            std::cout << stk.top() << std::endl;

                            stk.pop();

              }

}

### Complexity

Time complexity is ![](2/images/00047.jpeg), space complexity is ![](2/images/00048.jpeg).

## 10  Detecting a bipartite graph

A bipartite graph is a graph, in which its vertices can be divided into two disjoint sets U and ![](2/images/00049.jpeg).

![](2/images/00050.jpeg) ![](2/images/00051.jpeg) ![](2/images/00052.jpeg) ![](2/images/00053.jpeg) ![](2/images/00053.jpeg) ![](2/images/00053.jpeg) ![](2/images/00054.jpeg)

![](2/images/00055.jpeg) ![](2/images/00056.jpeg) ![](2/images/00053.jpeg) ![](2/images/00053.jpeg)

![](2/images/00057.jpeg) ![](2/images/00058.jpeg) ![](2/images/00053.jpeg)

### ![](2/images/00059.jpeg)

### Solution

A DFS or a BFS visit can be performed by assigning colors to the graph in such a way that the children have opposite colors from their parents.  If two directly connected nodes have same color, the graph is not bipartite.

### Code

bool isBipartite(const  Graph & g, Graph::NodeID  sid)

{

 if (sid >= g.numNodes())                                         

 return  false;

              std::vector<Graph::NodeID> colour(g.numNodes(), -1);

              colour[sid] = 1;

              std::list<Graph::NodeID> queue;

              queue.push_back(sid);

 while (!queue.empty())

              {

 const  Graph::NodeID n = queue.front();

                            queue.pop_front();

std::cout << "Visited=" << n << std::endl;

 for (const  auto & e : g.edges(n))

                            {

 if (colour[e.v] == -1)

                                          {

                                                        colour[e.v] = 1 - colour[n];

                                                        queue.push_back(e.v);

                                          }

 else  if (colour[e.v] == colour[n])

 return  false;

                            }

              }

 return  true;

}

### Complexity

Time complexity is ![](2/images/00060.jpeg), space complexity is ![](2/images/00061.jpeg).

## 11  Given a connected graph, compute the minimum spanning tree (MST)

Let’s start with some definitions. An undirected graph is said to be connected, if every pair of vertices in the graph is connected. In particular, two vertices ![](2/images/00062.jpeg) and ![](2/images/00063.jpeg) are defined as connected, if the graph contains a [path](http://en.wikipedia.org/wiki/Path_(graph_theory)) from![](2/images/00064.jpeg) to ![](2/images/00065.jpeg). Given a connected graph, a spanning tree is a tree which connects all vertices together. If the graph has weights associated to the edges, then the minimum spanning tree is a spanning tree with minimal sum of the edges’ weight.

### Solution

One way to compute the MST is to adopt a classical greedy algorithm due to Prim[[1]](#part0000_split_036.html__ftn1). At the beginning the tree contains a single vertex, chosen arbitrarily from the graph. Then the minimum weight edge is selected among those connecting a vertex in the tree with a vertex not being in the tree. This edge is added to the tree and the previous step is repeated until all vertices are in the tree. In our implementation the edges are maintained ordered by using a priority queue realized with boost::fibonacci

### Code

struct  nodeComparison

{

 const  MatrixGraph::NodeID node;

 MatrixGraph::weight priority;

  nodeComparison(MatrixGraph::NodeID  name,

MatrixGraph::NodeID  p) : node(name), priority(p) {};

 bool operator < (nodeComparison  const & rhs) const

  {

 return priority > rhs.priority;

  }

};

void PrimMST(const  MatrixGraph & g, MatrixGraph::NodeID  startNode)

{

 typedef boost::heap::fibonacci_heap< nodeComparison > Heap;

 Heap heap;

  std::map <MatrixGraph::NodeID, Heap::handle_type> mapHandles;

// for decrease() key

 MatrixGraph::weight edgeWeight;

 MatrixGraph::NodeID numNodes = g.getNumNodes();

  std::vector<bool> isInHeap(numNodes, false);

  std::vector<MatrixGraph::NodeID> parent(numNodes + 1, 0);

 for (MatrixGraph::NodeID i = 0; i < numNodes; ++i)

  {

    mapHandles[i] =

heap.push(nodeComparison(i,

std::numeric_limits<MatrixGraph::weight>::max()));

isInHeap[i] = true;

  }

  (*(mapHandles[startNode])).priority = 0;

// initial node has priority 0

  heap.increase(mapHandles[startNode]);

 // fibonacci has increase ammortized constat

 // decrease is logaritmic -> inverted operator <

 while (!heap.empty()){

 const  nodeComparison nc = heap.top(); // extract top

    heap.pop();

isInHeap[nc.node] = false; // no longer in heap

std::cout << "node=" << nc.node << " w="

<< nc.priority << std::endl;

 for (MatrixGraph::NodeID v = 0; v < numNodes; ++v)

    {

 if ((edgeWeight = g(nc.node, v)) // an edge (nc.node, v)

&& (isInHeap[v]) // v is in Heap

        && (edgeWeight < (*(mapHandles[v])).priority))

// improving weight

      {

        (*(mapHandles[v])).priority = edgeWeight;

        heap.increase(mapHandles[v]);

        parent[v] = nc.node;

std::cout << "node=" << nc.node << "->"

<< v << " with w=" <<

          (*(mapHandles[v])).priority << std::endl;

      }

    }

  }

std::cout << "MST" << std::endl;

 for (MatrixGraph::NodeID i = 1; i < numNodes; ++i)

  {

std::cout << parent[i] << '-' << i <<

 " weight=" << g(parent[i], i) << std::endl;

  }

}

### \

This particular implementation uses an adjacency matrix and therefore its complexity is ![](2/images/00066.jpeg). However it is possible to get ![](2/images/00067.jpeg) by using adjacent lists and a Fibonacci heap in which a Find-minimum is![](2/images/00068.jpeg) amortized time[[2]](#part0000_split_036.html__ftn2)

| adjacency matrix for dense or sparse graph | ![](2/images/00069.jpeg) |
| binary heap and adjacency lists for sparse graph | ![](2/images/00070.jpeg)![](2/images/00071.jpeg) |
| binary heap and adjacency lists for dense graph | ![](2/images/00072.jpeg) |
| Fibonacci heap and adjacency list | ![](2/images/00073.jpeg) |

## 12  

Space complexity evaluation is here left as an exercise. An example of minimum spanning tree is in the picture below

![](2/images/00074.jpeg)

## 13  Find the strongly connected components in a direct graph

A direct graph ![](2/images/00075.jpeg) is said to be strongly connected, if every node is reachable from every other node. The strongly connected components of ![](2/images/00076.jpeg) create a partition into subgraph that are themselves strongly connected as in this figure.

![http://upload.wikimedia.org/wikipedia/commons/thumb/5/5c/Scc.png/220px-Scc.png](2/images/00077.jpeg)

### Solution

The here implemented solution is the Kosaraju’s algorithm[[3]](#part0000_split_036.html__ftn3) which uses two passes of DFS. The first pass is carried out on the original graph and it is used to choose the order in which the outer loop of the second DFS tests are connected to the vertices. The second DFS is on the transpose graph of the original graph. Each recursive exploration finds a single new strongly connected component.

### Code

// 

// Transpose

void transpose(const  Graph & g, Graph & gt)

{

 gt.reserveNodes(g.numNodes());

 gt.reserveEdges(g.numEdges());

 // add all nodes

 for (const  auto & n : g.nodes())

 gt.addNode(n.w, n.label);

 // add all edges

 for (Graph::NodeID id = 0; id < g.numNodes(); ++id)

 for (const  auto & e : g.edges(id))

 gt.addEdge(e.v, id, e.w, e.label);

}

//

// SCC

void fillOrder(const  Graph & g, Graph::NodeID  v,

              std::vector<bool> & visited,

              std::stack<Graph::NodeID> &stk)

{

 visited[v] = true;

 for (const  auto & e : g.edges(v))

 if (!visited[e.v])

                            fillOrder(g, e.v, visited, stk);

 stk.push(v);

}

void StrongConnectedComponents(const  Graph & g)

{

              std::stack<Graph::NodeID> stk;

              std::vector<bool> visited(g.numNodes(), false);

 unsigned componentID = 0;

 for (Graph::NodeID id = 0; id < g.numNodes(); ++id)

 if (visited[id] == false)

                            fillOrder(g, id, visited, stk);

 Graph gt;

              transpose(g, gt);

std::fill(visited.begin(), visited.end(), false);

 while (!stk.empty())

              {

 Graph::NodeID id = stk.top();

                            stk.pop();

 if (!visited[id])

                            {

                                          dfsUtil(g, id, visited);

std::cout << "end component id="

                                                        << componentID++ << std::endl;

                            }

              }

}

### Complexity

Time complexity is here ![](2/images/00078.jpeg)

## 14 Covering DFS Trees

Given a graph ![](2/images/00079.jpeg) it is possible to define a path tree ![](2/images/00080.jpeg) generated by a DFS visit. If G is not (strongly) connected then we need to restart the DFS from each node and the visit will generate a forest of trees, If the graph is direc,t the visit will respect the direction of the edges, while if the graph is not direct, the visit will produce a random orientation of each edge as a consequence of the direction of the visit. During the visit the edges not yet included in ![](2/images/00081.jpeg) can be divided into three categories:

*   If the edge is examined by passing from a node ![](2/images/00082.jpeg) in ![](2/images/00083.jpeg) to another node ![](2/images/00084.jpeg) in T, which is an ancestor of ![](2/images/00085.jpeg) in G, then the edge (u, v) is called  loop back edge
*   If the edge is examined by passing from a node ![](2/images/00086.jpeg) in ![](2/images/00087.jpeg) to another node ![](2/images/00088.jpeg) in T, which is a descendant of ![](2/images/00089.jpeg) in G, then the edge (u, v) is called  forward edge
*   Otherwise it is called cross edge

## 15  Find an Hamiltonian cycle

A Hamiltonian path[[4]](#part0000_split_036.html__ftn4) is a path through a[graph](http://mathworld.wolfram.com/Graph.html) that visits each node exactly once. If the path is also a cycle, then we have a Hamiltonian cycle as in the figure. The problem is NP-Complete so the worst case solution needs exponential time in the number of nodes.

![http://upload.wikimedia.org/wikipedia/commons/thumb/6/60/Hamiltonian_path.svg/220px-Hamiltonian_path.svg.png](2/images/00090.jpeg)

### Solution

Here we present a backtracking algorithm in C++

### Code

// hamiltonianCycle

bool isSafe(const  MatrixGraph& g,

 const  MatrixGraph::NodeID  v,

              std::vector<MatrixGraph::NodeID> & path,

 const  unsigned  int  pos)

{

 if (!g(path[pos - 1], v))

 return  false;

 for (MatrixGraph::NodeID i = 0; i < pos; ++i)

 if (path[i] == v)

 return  false;

 return  true;

}

bool hamiltonianCycleUtil(const  MatrixGraph & g,

              std::vector<MatrixGraph::NodeID> & path,

 const  unsigned  int  pos)

{

 if (pos == g.getNumNodes())

              {

 if (g(path[pos - 1], path[0]))

 return  true;

 else

 return  false;

              }

 for (MatrixGraph::NodeID v = 1; v < g.getNumNodes();                             ++v)

              {

 if (isSafe(g, v, path, pos))

                            {

 path[pos] = v; // insert v

 if (hamiltonianCycleUtil(g, path,

 pos + 1) == true)

 return  true;

 path[pos] = -1; // remove v

                            }

              }

 return  false;

}

bool hamiltonianCycle(const  MatrixGraph & g)

{

 MatrixGraph::NodeID V = g.getNumNodes();

              std::vector<MatrixGraph::NodeID>path(V, -1);

 bool returnValue;

              path[0] = 0;

 if ((returnValue = hamiltonianCycleUtil(g, path, 1)))

              {

std::cout << "Hamiltionian cycle " << std::endl;

 for (MatrixGraph::NodeID i = 0; i < V; ++i)

std::cout << path[i] << ' ';

                            std::cout << std::endl;

              }

 else {

std::cout << "No Hamiltionian cycle";

              }

 return returnValue;

}

## 16  Find the articulation points in a graph

An articulation point is any vertex, where its removal increases the number of connected components.

### Solution

The algorithm proposed is due to Hopcroft and Tarjan[[5]](#part0000_split_036.html__ftn5). The idea is to run a DFS while maintaining:

1.  the depth of each vertex in the DFS tree
2.  For each node ![](2/images/00091.jpeg), the lowest depth of neighbours of all descendants of ![](2/images/00092.jpeg) in the DFS tree, called the lowpoint. The lowpoint of ![](2/images/00093.jpeg) can be computed after visiting all descendants of ![](2/images/00094.jpeg) as the minimum of the depth of ![](2/images/00095.jpeg), the depth of all neighbors of ![](2/images/00096.jpeg) (excluding the parent of ![](2/images/00097.jpeg) in the DFS tree) and the lowpoint of all children of ![](2/images/00098.jpeg) in the DFS tree.

A non-root vertex ![](2/images/00099.jpeg) is an articulation point, if and only if there is a child ![](2/images/00100.jpeg) of ![](2/images/00101.jpeg)such that ![](2/images/00102.jpeg) This property can be tested, once the depth-first search is returned from every child of v.  The root vertex must be handled separately: it is an articulation point, if and only if it has at least two children.

### Code

//

// Articulation Points

void articulationUtil(const  Graph & g,

 const  Graph::NodeID  u,

 unsigned  int & time,

              std::vector<bool> & visited,

              std::vector<Graph::NodeID> & discovery,

              std::vector<Graph::NodeID> & lower,

              std::vector<Graph::NodeID> & parent,

              std::vector<bool> & articulationPoints)

{

 Graph::NodeID children = 0;

 visited[u] = true;

 discovery[u] = lower[u] = ++time;

 for (const  auto & e : g.edges(u))

              {

 if (!visited[e.v])

                            {

 parent[e.v] = u;

                                          children++;

                                          articulationUtil(g, e.v, time, visited,

 discovery, lower, parent,

 articulationPoints);

 lower[u] = std::min(lower[u], lower[e.v]);

 if (parent[u] ==

                                                        std::numeric_limits<Graph::NodeID>::max()

                                                        && children > 1)

 articulationPoints[u] = true;

 if (parent[u] ==

                                                        std::numeric_limits<Graph::NodeID>::max()

&& lower[e.v] >= discovery[u])

 articulationPoints[u] = true;

                            }

 else  if (e.v != parent[u])

 lower[u] = std::min(lower[u],

discovery[e.v]);

              }

}

void articulationPoints(const  Graph & g)

{

 unsigned  int time = 0;

              std::vector<bool> visited(g.numNodes(), false);

              std::vector<Graph::NodeID> discovery(g.numNodes(), 0);

              std::vector<Graph::NodeID> lower(g.numNodes(), 0);

              std::vector<Graph::NodeID> parent(g.numNodes(),

                            std::numeric_limits<Graph::NodeID>::max());

              std::vector<bool> articulationPoints(g.numNodes(),

 false);

 for (Graph::NodeID id = 0; id < g.numNodes(); ++id)

 if (!visited[id])

                            articulationUtil(g, id, time, visited, discovery,

                                          lower, parent, articulationPoints);

 for (Graph::NodeID id = 0; id < g.numNodes(); ++id)

 if (articulationPoints[id])

std::cout << "articulation point id=" <<

                            id << std::endl;

}

### Complexity

Time complexity is ![](2/images/00103.jpeg). An example of articulation point is in the picture below

![](2/images/00104.jpeg)

## 17  Find the shortest path in a graph with non-negative edge weight

### Solution

Given a graph with non-negative edge weight, we can apply Dijkstra’s algorithm for finding the single-source shortest path tree[[6]](#part0000_split_036.html__ftn6). Edger Dijkstra was born in the Netherlands and he invented the algorithm in 1959.  For a given source node ![](2/images/00105.jpeg), the algorithm looks for the path with lowest cost between ![](2/images/00106.jpeg) and every other node. This class of problems has multiple applications including optimization, routing and traffic assignment. The pseudo-code for Dijkstra is given below. The vector ![](2/images/00107.jpeg) contains the sum of weights for the path used to arrive to the node ![](2/images/00108.jpeg) (at the beginning this is infinite). The vector ![](2/images/00109.jpeg) contains the predecessor of ![](2/images/00110.jpeg) in the shortest path (at the beginning ![](2/images/00111.jpeg)). In addition a priority queue![](2/images/00112.jpeg) is used to select nodes ![](2/images/00113.jpeg) with the smallest ![](2/images/00114.jpeg)  (in the pseudo-code this is the operationu ← EXTRACT-MIN(Q))).Moreover, ![](2/images/00115.jpeg)]contains all the nodes ![](2/images/00116.jpeg) adjacent to ![](2/images/00117.jpeg). So for each ![](2/images/00118.jpeg) , if ![](2/images/00119.jpeg) - the sum of weights for the path leading to ![](2/images/00120.jpeg) - plus to the weight of the edge ![](2/images/00121.jpeg)is less than ![](2/images/00122.jpeg) - the sum of the weights for the path leading to ![](2/images/00123.jpeg) - then we have identified a shorter path. In this case, ![](2/images/00124.jpeg) and ![](2/images/00125.jpeg) are updated accordingly. Also the node v is added to Q, if it has never been visited before.  Instead, if it has been already visited, its priority in Q should be reduced according to the new weight (this is the operationDECREASE-KEY(Q, v)in the pseudo-code). At the end the vectors ![](2/images/00126.jpeg) and ![](2/images/00127.jpeg) are returned.

### Code

| DIJKSTRA(G, s, w) for each vertex u in V d[u] ← infinity p[u] ← u color[u] ← WHITE color[s] ←  GRAY d[s] ← 0  INSERT(Q, s) while (Q != Ø) u ← EXTRACT-MIN(Q) for each vertex v in Adj[u] if (w(u,v) + d[u] < d[v]) d[v] ← w(u,v) + d[u] p[v] ← u if (color[v] ==  WHITE) color[v] ←  GRAY          INSERT(Q, v) else if (color[v] == GRAY)          DECREASE-KEY(Q, v) color[u] ← BLACK  return (d, p) |  |

For this exercise[[7]](#part0000_split_036.html__ftn7) we start using boost::BGL a powerful framework for graph creation and processing[[8]](#part0000_split_036.html__ftn8). A graph can have weights and names labels associated to the edges and those are stored in a boost::property. In addition a graph can be represented either with a boost::adjacency_list or with a boost:adjacenty_matrix. The boost:adjacenty_list uses many parameters including OutEdgeList (the selector for the container used to represent the edge-list for each of the vertices), VertexList (the selector for the container used to represent the vertex-list of the graph), Directed (a selector to choose whether the graph is directed, undirected, or directed with bidirectional edge access), VertexProperties (for specifying internal property storage), EdgeProperties (for specifying internal property storage), GraphProperties (for specifying property storage for the graph object) , EdgeList (the selector for the container used to represent the edge-list for the graph). For instance, listS selects std::list and this is a good choice, if you need to add and remove vertices quickly. The adjacency_listclass implements boost::property_maps for accessing objects (properties) that are attached to the vertices and edges of the graph, and boost::iterator_property_map is  used to navigate inside the maps. All these features are used to represent multiple flavours of graphs with an uniform representation. Having this contest in mind, we can create a Graph  g and add vertices and edges with the appropriate boost method. The predecessorMap records the edges in the shortest path tree, the tree is computed by the graph traversal, while the shortest path weight from the source vertex  to each vertex in the graph g is recorded in the distanceMap. In this particular example we compute the shortest path starting from a specific source node v3 and we extract the shortest path by following the computed precedessorMap

#include  <boost/graph/adjacency_list.hpp>

#include  <boost/graph/dijkstra_shortest_paths.hpp>

#include  <boost/graph/graph_traits.hpp>

#include  <boost/graph/iteration_macros.hpp>

#include  <boost/graph/properties.hpp>

#include  <boost/property_map/property_map.hpp>

void boostDijkstra()

{

 typedef  float  Weight;

 // http://www.boost.org/doc/libs/1_55_0/libs/graph/doc/property.html

 typedef boost::property<boost::edge_weight_t,

 Weight> WeightProperty;

 typedef boost::property<boost::vertex_name_t,

                            std::string> NameProperty;

 // http://www.boost.org/doc/libs/1_53_0/libs/graph/doc/adjacency_list.html

 typedef boost::adjacency_list < boost::listS,

                            boost::vecS, boost::directedS,

 NameProperty, WeightProperty > Graph;

 // http://www.boost.org/doc/libs/1_55_0/libs/graph/doc/graph_traits.html

 typedef boost::graph_traits < Graph >::vertex_descriptor  Node;

 typedef boost::property_map < Graph,

                            boost::vertex_index_t >::type  IndexMap;

 typedef boost::property_map < Graph,

                            boost::vertex_name_t >::type  NameMap;

 // http://www.boost.org/doc/libs/1_37_0/libs/property_map/iterator_property_map.html

 typedef boost::iterator_property_map < Node*, IndexMap,

 Node, Node& > PredecessorMap;

 typedef boost::iterator_property_map < Weight*, IndexMap,

 Weight, Weight& > DistanceMap;

 Graph g;

 Node v0 = boost::add_vertex(std::string("v0"), g);

 Node v1 = boost::add_vertex(std::string("v1"), g);

 Node v2 = boost::add_vertex(std::string("v2"), g);

 Node v3 = boost::add_vertex(std::string("v3"), g);

              boost::add_edge(v0, v1, 15, g);

              boost::add_edge(v1, v3, 7, g);

              boost::add_edge(v0, v2, 2, g);

              boost::add_edge(v2, v3, 4, g);

              std::vector<Node> predecessors(boost::num_vertices(g));

              std::vector<Weight> distances(boost::num_vertices(g));

 IndexMap indexMap = boost::get(boost::vertex_index, g);

 PredecessorMap predecessorMap(&predecessors[0],

                            indexMap);

 DistanceMap distanceMap(&distances[0], indexMap);

              boost::dijkstra_shortest_paths(g, v0,

                            boost::distance_map(distanceMap).predecessor_map(predecessorMap));

std::cout << "distances and parents:" << std::endl;

 NameMap nameMap = boost::get(boost::vertex_name, g);

 BGL_FORALL_VERTICES(v, g, Graph)

              {

std::cout << "distance(" << nameMap[v0] << ", "

<< nameMap[v] << ") = " << distanceMap[v]

<< ", ";

std::cout << "predecessor(" << nameMap[v]

<< ") = "

                                          << nameMap[predecessorMap[v]] << std::endl;

              }

              std::cout << std::endl;

 typedef std::vector<Graph::edge_descriptor> PathType;

 PathType path;

 Node v = v3;

 for (Node u = predecessorMap[v];

                            u != v;

                            v = u, u = predecessorMap[v])

              {

                            std::pair<Graph::edge_descriptor, bool> edgePair =

                                          boost::edge(u, v, g);

 Graph::edge_descriptor edge = edgePair.first;

                            path.push_back(edge);

              }

 float totalDistance = 0;

 for (PathType::reverse_iterator pathIterator =

                            path.rbegin();

                            pathIterator != path.rend(); ++pathIterator)

              {

                            std::cout <<

nameMap[boost::source(*pathIterator, g)]

<< " -> " << nameMap[boost::target(*pathIterator, g)]

<< " = " <<

                                          boost::get(boost::edge_weight, g,

*pathIterator)

<< std::endl;

              }

std::cout << "Distance: "

<< distanceMap[v2] << std::endl;

}

A useful exercise is to use Dijkstra for computing the shortest path on the graph represented in picture.

![](2/images/00128.jpeg)

### Complexity

Time complexity is ![](2/images/00129.jpeg), if the priority queue is implemented using Fibonacci heaps. Fibonacci heap is a priority queue which implements extracting minimum efficiently. Note that Dijkstra’s original algorithm does not use a [min-priority queue](http://en.wikipedia.org/wiki/Min-priority_queue) and runs in [time](http://en.wikipedia.org/wiki/Time_complexity)![](2/images/00130.jpeg).

## 18  Find MST(Minimum Spanning Tree) using Kruskal Algorithm

Kruskal’s algorithm finds a minimum spanning tree (MST) in an undirected graph with weighted edges. The algorithm orders the edges for increasing weight and then every single edge is included in the solution, if it does not form a cycle with the edges already selected.

### Solution

The pseudo code uses UNION-FIND operations[[9]](#part0000_split_036.html__ftn9)  :

*   Find: Determine which subset a particular element is in. It is used for determining, if two elements are in the same subset.
*   Union: Join two subsets into a single subset.

KRUSKAL-MST(G, w)

 T ← Ø

 for each vertex u in V

    MAKE-SET(DS, u)

 for each edge (u,v) in E in order of nondecreasing weight

 if FIND-SET(DS, u) != FIND-SET(DS, v)

      UNION-SET(DS, u, v)

 T ← T U {(u,v)}

return  T

In boost[[10]](#part0000_split_036.html__ftn10), this is defined inboost/graph/kruskal_min_spanning_tree.hpp

As an exercise try to compute Kruskal on the following graph

![](2/images/00131.jpeg)

![](2/images/00132.jpeg) ![](2/images/00133.jpeg) ![](2/images/00134.jpeg) ![](2/images/00134.jpeg)

![](2/images/00135.jpeg) ![](2/images/00136.jpeg) ![](2/images/00137.jpeg) ![](2/images/00138.jpeg) ![](2/images/00139.jpeg)

![](2/images/00140.jpeg) ![](2/images/00141.jpeg)

![](2/images/00142.jpeg) ![](2/images/00143.jpeg) ![](2/images/00144.jpeg) ![](2/images/00144.jpeg)

### Complexity

Time complexity is ![](2/images/00145.jpeg) because we use union-find data structure to keep the set information,whereFind operations on![](2/images/00146.jpeg) elements require  ![](2/images/00147.jpeg)  time.

## 19  Find the longest path in a DAG

The problem of finding the longest path is NP-hard for a general graph. However if we have a DAG, we can easily compute the topological sort. Then for every node we update the distance of its adjacent nodes by using the distance of current vertex.

### Solution

This code uses the topological sort defined before and then adds weights starting from the source

### Code

void longestPathDAG(const  Graph & g,

 const  Graph::NodeID  id,

              std::vector<Graph::NodeID>& distance)

{

              std::stack<Graph::NodeID> stk;

 distance = std::vector<Graph::NodeID>(g.numNodes(),

                            std::numeric_limits<Graph::NodeID>::max());

              std::vector<bool> visited(g.numNodes(), false);

 distance[id] = 0;

 for (Graph::NodeID id = 0; id < g.numNodes(); ++id)

 if (!visited[id])

                            topologicalSortUtil(g, id, visited, stk);

 while (!stk.empty())

              {

 const  Graph::NodeID id = stk.top();

                            stk.pop();

 if (distance[id] !=

                                          std::numeric_limits<Graph::NodeID>::max())

                            {

 for (const  auto & e : g.edges(id))

 if (distance[e.v] > distance[id] + e.w)

 distance[e.v] = distance[id] + e.w;

                            }

              }

 for (Graph::NodeID id = 0; id < g.numNodes(); ++id)

 if (distance[id] ==

std::numeric_limits<Graph::NodeID>::max())

std::cout << "id=" << id <<

 " has infinity distance" << std::endl;

 else

std::cout << "id=" << id <<

 " has distance=" << distance[id] << std::endl;

}

### Complexity

Time complexity is ![](2/images/00148.jpeg). What is the space complexity?

## 20  Find MST (Minimum Spanning Tree) using Prim Algorithm

Prim’s[[11]](#part0000_split_036.html__ftn11) algorithm finds a minimum spanning tree (MST) in an undirected graph with weighted edges. Prim’s is a typical greedy algorithm which maintains two data structures ![](2/images/00149.jpeg) containing the predecessor of the node ![](2/images/00150.jpeg) and ![](2/images/00151.jpeg), containing the minimum distance from node![](2/images/00152.jpeg). At the beginning every node is marked as not visited and the distance is infinite. Then the source node ![](2/images/00153.jpeg) is inserted in a priority queue ![](2/images/00154.jpeg) ordered by distance![](2/images/00155.jpeg). Until the queue is not empty a node ![](2/images/00156.jpeg)is de-queued from ![](2/images/00157.jpeg) . For each node ![](2/images/00158.jpeg) adjacent to ![](2/images/00159.jpeg)the condition ![](2/images/00160.jpeg) is checked where ![](2/images/00161.jpeg) is the weight associated to the edge ![](2/images/00162.jpeg). The node v is inserted in Q, if the condition is met and the node was never visited before. Instead if priority is decreased, the condition is met but the node is already in ![](2/images/00163.jpeg).             

### Solution

The pseudo code is the following:

PRIM-MST(G, s, w)

 for each vertex u  in  V[G] 

 color[u] ←  WHITE; d[u] ←  infinity 

 color[s] ←  GRAY; d[s] ← 0

  ENQUEUE(Q, s); p[s] ← s

 while (Q != Ø)

 u := DEQUEUE(Q)

 for each v in Adj[u] 

 if (w(u,v) < d[v])

 d[v] ← w(u,v); p[v] ← u

 if (color[v] = WHITE)

          ENQUEUE(Q, v) ;color[v] ←  GRAY

 else if (color[v] = GRAY)

          DECREASE-KEY (Q, v)

 color[u] ←  BLACK

return (p, d)

In boost, this is defined in [boost/graph/prim_minimum_spanning_tree.hpp](http://www.boost.org/doc/libs/1_55_0/boost/graph/prim_minimum_spanning_tree.hpp)

### Complexity

Time complexity is ![](2/images/00164.jpeg) where ![](2/images/00165.jpeg) is the time needed for extracting ![](2/images/00166.jpeg) nodes from ![](2/images/00167.jpeg) and ![](2/images/00168.jpeg) is the time needed for processing the adjacency list and update the queue. Note that if we use Fibonacci heap, then operations of insert and decreaseKey have cost ![](2/images/00169.jpeg) amortized by deleteKey with cost ![](2/images/00170.jpeg). So complexity is ![](2/images/00171.jpeg) by using Fibonacci

## 21  Find all pairs shortest paths using the Floyd-Warshall Algorithm

Floyd & Warshall’s algorithm finds the shortest distance between every pair of vertices in the graph. The algorithm detects, if there are loops with negative weights, which will produce a degenerate negative infinite shortest path otherwise.

### Solution

The pseudo-code is

let dist be a |V| × |V| array of min distances initialized to ∞

 for each vertex v

     dist[v][v] ← 0

 for each edge (u,v)

     dist[u][v] ← w(u,v)  // the weight for edge (u, v)

 for k from 1 to |V|

 for i from 1 to |V|

 for j from 1 to |V|

           if dist[i][j] > dist[i][k] + dist[k][j]

              dist[i][j] ← dist[i][k] + dist[k][j]

This pseudo-code computes the weight of each shortest path between all pair of nodes ![](2/images/00172.jpeg) in the graph. However, it does not memorize the minimum paths. These can be stored with some changes in the code which are here left for exercise.

Now let’s consider a negative cycle which is a cycle whose edges sum to a negative value. There is no shortest path between any pair of nodes ![](2/images/00173.jpeg) which form a part of a negative cycle, because path-lengths from ![](2/images/00174.jpeg) to![](2/images/00175.jpeg) can be arbitrarily small. As an exercise we ask to modify the pseudo-code for detecting negative cycles.

In boost this is defined in  [boost/graph/floyd_warshall_shortest.hpp](http://www.boost.org/doc/libs/1_41_0/boost/graph/floyd_warshall_shortest.hpp)

### Complexity

Time complexity is ![](2/images/00176.jpeg), while space complexity is ![](2/images/00177.jpeg)

## 22  Find all the single source shortest paths using Bellman Ford Algorithm

The Bellman-Ford algorithm finds the single-source shortest paths problem for a graph with both positive and negative edge weights. Dijkstra’s algorithm is more efficient for a graph with only positive edge weights. Bellman Ford is the code of the old RIP[[12]](#part0000_split_036.html__ftn12) (Routing Internet Protocol). Bellman-Ford is very similar to Dijkstra but it processes all the edges instead of selecting the node with minimum weight among those that still have to be processed (greedy choice). This computation is repeated for all the nodes.

### Solution

The pseudo-code is the following:

BELLMAN-FORD(G)

 for each vertex u in V

 d[u] ← infinity; p[u] ← u

 for  i ← 1  to  |V|-1

 for each edge (u,v) in E

 if (w(u,v) + d[u] < d[v])

 d[v] ← w(u,v) + d[u];

 p[v] ← u

 for each edge (u,v) in E

 if (w(u,v) + d[u] < d[v])

 return (false, , )

 return (true, p, d)

In boost this is defined in [boost/graph/bellman_ford_shortest_paths.hpp](http://www.boost.org/doc/libs/1_55_0/boost/graph/bellman_ford_shortest_paths.hpp)

### Complexity

Time complexity is ![](2/images/00178.jpeg)

## 23 Independent set of intervals

Given a set of n intervals in the real line, a maximum independent set is a subset X of intervals with maximum size such that any pair of intervals in X has empty intersection.

### Solution

Without losing in generality, let us assume that the intervals ![](2/images/00179.jpeg) have 2 distinct bounds. Let us add to additional intervals ![](2/images/00180.jpeg) and ![](2/images/00181.jpeg) such that ![](2/images/00182.jpeg) and ![](2/images/00183.jpeg) for ![](2/images/00184.jpeg). We can build an acyclic graph ![](2/images/00185.jpeg) with ![](2/images/00186.jpeg) nodes corresponding to the![](2/images/00187.jpeg) intervals such that there is an edge ![](2/images/00188.jpeg), if and only if ![](2/images/00189.jpeg). Then we assign the weight ![](2/images/00190.jpeg)  to each edge![](2/images/00191.jpeg). It can be verified that the shortest path on ![](2/images/00192.jpeg) defines the independent set of intervals.

### Complexity

G is a DAG and can be built in ![](2/images/00193.jpeg) and therefore the shortest path can be computed in ![](2/images/00194.jpeg).

## 24 Dominant set of intervals

Given a set of n intervals in the real line, a dominant set is a subset X of intervals with minimum size, such that any interval which is not in X has non-empty intersection with the intervals in X.

### Solution

Let us make the same assumptions of the previous exercise: we will construct a new graph ![](2/images/00195.jpeg). For each interval ![](2/images/00196.jpeg) with ![](2/images/00197.jpeg) define ![](2/images/00198.jpeg) and ![](2/images/00199.jpeg) h: ![](2/images/00200.jpeg)} and introduce and edge ![](2/images/00201.jpeg). if and only if ![](2/images/00202.jpeg). Then we assign the weight![](2/images/00203.jpeg). It can be verified that the shortest path on ![](2/images/00204.jpeg) defines a dominant set of intervals.

### Complexity

G is a DAG and can be built in ![](2/images/00205.jpeg) and therefore the shortest path can be computed in ![](2/images/00206.jpeg).

## 25  Weighted dominant set of intervals

Given a set of n intervals in the real line where each interval has an associated weight integer and a non-negative. Find a dominant set with minimum weight.

### Solution

Left as an exercise

## 26  Weighted shortest paths with cost associated to the nodes

Suppose that the cost is associated to the nodes instead that to  the edges and that therefore the cost of a path is the sum of all the nodes it contains. According to this assumption compute the all pair shortest path.

### Solution

A solution can be easily computed associating to each ![](2/images/00207.jpeg) the new weight ![](2/images/00208.jpeg). However, all the paths should increase the weight by a constant w(root), because the root is not crossed by any edge

## 27  Find the flow network using Ford–Fulkerson’Algorithm

A flow network (also known as a transportation network) is a directed graph, where each edge ![](2/images/00209.jpeg) has a capacity ![](2/images/00210.jpeg)and receives a flow ![](2/images/00211.jpeg) that cannot exceed![](2/images/00212.jpeg).  The amount of flow into a node must be equal to the amount of flow out of it. However, a source has a more outgoing flow and a sink has a more incoming flow. A network can be used to model traffic information, currents in an electrical circuit and similar problems.

### Solution

The pseudo-code is the following:

Givena Network ![](2/images/00213.jpeg) withflow capacity ![](2/images/00214.jpeg), a source node ![](2/images/00215.jpeg), and a sink node ![](2/images/00216.jpeg)compute a flow f from  ![](2/images/00217.jpeg) to ![](2/images/00218.jpeg) of maximum value

1.  ![](2/images/00219.jpeg) ← 0 for all edges![](2/images/00220.jpeg)
2.  While there is a path ![](2/images/00221.jpeg) from ![](2/images/00222.jpeg) to ![](2/images/00223.jpeg) in G![](2/images/00224.jpeg), such that ![](2/images/00225.jpeg) for all edges ![](2/images/00226.jpeg) :
    1.  Find ![](2/images/00227.jpeg)
    2.  For each edge ![](2/images/00228.jpeg)
        1.  ![](2/images/00229.jpeg) + ![](2/images/00230.jpeg)
        2.  ![](2/images/00231.jpeg) - ![](2/images/00232.jpeg)

where ![](2/images/00233.jpeg)  is the residual graph when ![](2/images/00234.jpeg)flow is sent over the network where the capacity ![](2/images/00235.jpeg) and there is no flow

The algorithm is defined in [boost/graph/edmonds_karp_max_flow.hpp](http://www.boost.org/doc/libs/1_55_0/boost/graph/edmonds_karp_max_flow.hpp)

### Complexity

It can be proven that Ford-Fulkerson[[13]](#part0000_split_036.html__ftn13) has time complexity is ![](2/images/00236.jpeg) where f is the maximum flow in the graph. A variant of Ford-Fulkerson known as Edmon-Karp[[14]](#part0000_split_036.html__ftn14) has proven complexity![](2/images/00237.jpeg) 

## 28  Assignment matching problem

The assignment matching problem consists in finding a maximum weight matching for a given weighted bipartite graph.

Assume that we have ![](2/images/00238.jpeg) workers and ![](2/images/00239.jpeg) tasks to be completed. For each pair (worker, task) we know the costs that should be paid per worker to conclude the task. The goal is to conclude all the tasks and to minimize the total cost, under the condition that each worker can execute only one task and vice versa.

### Solution

Let ![](2/images/00240.jpeg) the cost matrix for the worker ![](2/images/00241.jpeg) to conclude the task ![](2/images/00242.jpeg) and let ![](2/images/00243.jpeg) the assignment matrix when the worker ![](2/images/00244.jpeg) has assigned the task![](2/images/00245.jpeg). Clearly, ![](2/images/00246.jpeg) and ![](2/images/00247.jpeg) and we want to minimize the total cost function![](2/images/00248.jpeg).  Note that the costs-matrix can be represented as a complete bipartite graph as in the following example:

![](2/images/00249.jpeg)

Given this representation, the problem can be solved as a special instance of min cost flow and the solution is left as an exercise.

## 29  Find an Eulerian circuit

An Eulerian path[[15]](#part0000_split_036.html__ftn15) is a visit in a graph which touches every[edge](http://en.wikipedia.org/wiki/Edge_(graph_theory)) exactly once. If such a walk exists, the graph is said semi-eulerian or traversable. An Eulerian circuit is an Eulerian visit which starts and ends on the same [vertex](http://en.wikipedia.org/wiki/Vertex_(graph_theory)). These problems were first discussed by Leonhard Euler for solving the famous problem of Seven Bridges of Konigsberg[[16]](#part0000_split_036.html__ftn16) .

![Thumbnail for version as of 17:12, 27 July 2006](2/images/00250.jpeg)

The city of [Königsberg](http://en.wikipedia.org/wiki/K%C3%B6nigsberg) in [Prussia](http://en.wikipedia.org/wiki/Kingdom_of_Prussia) was built on both sides of the[Pregel river](http://en.wikipedia.org/wiki/Pregolya), and had two large islands which were connected to each other and the mainland by seven bridges The problem was to find a walk through the city that would cross each bridge once and only once. Euler proved that the problem has no solution and this problem is considering the first one introducing a new discipline called graph theory, the subject of this book.

### Solution

At first glance the problem seems similar to the Hamiltonian path. However it is not. Indeed a solution can be computed in linear time.

We notice that a graph has Eulerian cycle if: (a) All vertices with non-zero degree are connected b) All vertices have even degree. In addition, a graph follows the Eulerian Path, if following two conditions hold: (a) All vertices with non-zero degree are connected, (b) If zero or two vertices have odd degree and all other vertices have even degree. The proof of these properties is left as an exercise.

### Code

bool isConnected(const  Graph & g)

{

              std::vector<bool> visited(g.numNodes(), false);

              std::vector<Graph::NodeID> color(g.numNodes(), false);

              std::vector<Graph::NodeID> timing(g.numNodes(), 0);

 Graph::NodeID id;

 for (id = 0; id < g.numNodes(); ++id)

 if (g.outdegree(id))

 break;

 if (id == g.numNodes())

 return  true;

              dfsUtil(g, id, visited);

 for (id = 0; id < g.numNodes(); ++id)

 if (visited[id] == false && g.outdegree(id))

 return  false;

 return  true;

}

enum  euler { notEulerian, SemiEulerian, Eulerian };

//

// Eulerian

euler isEulerian(const  Graph & g)

{

 if (isConnected(g) == false)

 return  notEulerian;

 unsigned  int odd = 0;

 for (Graph::NodeID id = 0; id < g.numNodes(); ++id)

 if (g.outdegree(id) & 1)

                            odd++;

 if (odd > 2)

 return  notEulerian;

 return (odd) ? SemiEulerian : Eulerian;

}

### Complexity

Time complexity is ![](2/images/00251.jpeg)

## 30  Scheduling

Given ![](2/images/00252.jpeg) programs ![](2/images/00253.jpeg) which require ![](2/images/00254.jpeg) time for being executed and an acyclic relation of dependency such that ![](2/images/00255.jpeg), if program ![](2/images/00256.jpeg) must be executed before![](2/images/00257.jpeg) find an algorithm which minimizes the total execution time and respects the dependency relation

### Solution

We can define a DAG ![](2/images/00258.jpeg) with ![](2/images/00259.jpeg) nodes and ![](2/images/00260.jpeg) if and only if![](2/images/00261.jpeg). If we compute the topological sort of ![](2/images/00262.jpeg), the sorted sequence of nodes is the solution. Each node can start just after the moment given by the sum of all the preceding nodes in the sorted order

### Complexity

Complexity is ![](2/images/00263.jpeg) , where ![](2/images/00264.jpeg) and ![](2/images/00265.jpeg)

ABOUT THE AUTHOR

An experienced data mining engineer, passionate about technology and innovation in consumers’ space. Interested in search and machine learning on massive dataset with a particular focus on query analysis, suggestions, entities, personalization, freshness and universal ranking. Antonio Gullì has worked in small startups, medium (Ask.com, Tiscali) and large corporations (Microsoft, Elsevier). His carrier path is about mixing industry with academic experience.

“Nowadays, you must have a great combination of research skills and a just-get-it-done attitude.”

* * *

[[1]](#part0000_split_015.html__ftnref1)  [http://en.wikipedia.org/wiki/Prim%27s_algorithm](http://en.wikipedia.org/wiki/Prim%27s_algorithm)

[[2]](#part0000_split_015.html__ftnref2) http://en.wikipedia.org/wiki/Fibonacci_heap

[[3]](#part0000_split_017.html__ftnref3)  [http://en.wikipedia.org/wiki/Kosaraju%27s_algorithm](http://en.wikipedia.org/wiki/Kosaraju%27s_algorithm)

[[4]](#part0000_split_019.html__ftnref4)  [http://en.wikipedia.org/wiki/Hamiltonian_cycle](http://en.wikipedia.org/wiki/Hamiltonian_cycle)

[[5]](#part0000_split_020.html__ftnref5)  [http://en.wikipedia.org/wiki/Biconnected_component](http://en.wikipedia.org/wiki/Biconnected_component)

[[6]](#part0000_split_021.html__ftnref6)  [http://en.wikipedia.org/wiki/Dijkstra's_algorithm](http://en.wikipedia.org/wiki/Dijkstra's_algorithm)

[[7]](#part0000_split_022.html__ftnref7)  [http://programmingexamples.net/wiki/Boost/BGL/DijkstraComputePath](http://programmingexamples.net/wiki/Boost/BGL/DijkstraComputePath)

[[8]](#part0000_split_022.html__ftnref8)  [http://www.boost.org/doc/libs/1_55_0/libs/graph/doc/index.html](http://www.boost.org/doc/libs/1_55_0/libs/graph/doc/index.html)

[[9]](#part0000_split_023.html__ftnref9)  [http://en.wikipedia.org/wiki/Disjoint-set_data_structure](http://en.wikipedia.org/wiki/Disjoint-set_data_structure)

[[10]](#part0000_split_023.html__ftnref10)  [http://www.boost.org/doc/libs/1_55_0/libs/graph/doc/kruskal_min_spanning_tree.html](http://www.boost.org/doc/libs/1_55_0/libs/graph/doc/kruskal_min_spanning_tree.html)

[[11]](#part0000_split_025.html__ftnref11)  [http://en.wikipedia.org/wiki/Prim%27s_algorithm](http://en.wikipedia.org/wiki/Prim%27s_algorithm)

[[12]](#part0000_split_027.html__ftnref12)  [http://en.wikipedia.org/wiki/Routing_Information_Protocol](http://en.wikipedia.org/wiki/Routing_Information_Protocol)

[[13]](#part0000_split_032.html__ftnref13)  [http://en.wikipedia.org/wiki/Ford%E2%80%93Fulkerson_algorithm](http://en.wikipedia.org/wiki/Ford%E2%80%93Fulkerson_algorithm)

[[14]](#part0000_split_032.html__ftnref14)  [http://en.wikipedia.org/wiki/Edmonds%E2%80%93Karp_algorithm](http://en.wikipedia.org/wiki/Edmonds%E2%80%93Karp_algorithm)

[[15]](#part0000_split_034.html__ftnref15)  [http://en.wikipedia.org/wiki/Eulerian_path](http://en.wikipedia.org/wiki/Eulerian_path)

[[16]](#part0000_split_034.html__ftnref16)  [http://en.wikipedia.org/wiki/Seven_Bridges_of_K%C3%B6nigsberg](http://en.wikipedia.org/wiki/Seven_Bridges_of_K%C3%B6nigsberg)

A collection of Bit Programming Interview Questions Solved in C++

Antonio Gulli

Copyright © 2014 Antonio Gulli

All rights reserved.

ISBN:

ISBN-13:

Bits is the third of a series of 25 Chapters devoted to algorithms, problem solving, and C++ programming.

DEDICATION

To Leonardo, my second child.

Hoping that you keep your curiosity and energy

for the rest of your life.

ACKNOWLEDGMENTS

Thanks to Antonio Savona for his code review

Contents

[Contents](#part0000.html__Toc383672134)

[1. Given an unsigned int, swap the bits in odd and even positions](#part0000.html__Toc383672135)

[Solution](#part0000.html__Toc383672136)

[Code](#part0000.html__Toc383672137)

[2. Print the binary representation of an unsigned int](#part0000.html__Toc383672138)

[Solution](#part0000.html__Toc383672139)

[Code](#part0000.html__Toc383672140)

[3. Compute whether or not an unsigned number is a power of two](#part0000.html__Toc383672141)

[Solution](#part0000.html__Toc383672142)

[Code](#part0000.html__Toc383672143)

[4. Set the i-th bit](#part0000.html__Toc383672144)

[Solution](#part0000.html__Toc383672145)

[5. Unset the i-th bit](#part0000.html__Toc383672146)

[Solution](#part0000.html__Toc383672147)

[6. Toggle the i-th bit](#part0000.html__Toc383672148)

[Solution](#part0000.html__Toc383672149)

[7. Given an unsigned number with only one bit set, find the position of this bit](#part0000.html__Toc383672150)

[Solution](#part0000.html__Toc383672151)

[Code](#part0000.html__Toc383672152)

[Solution](#part0000.html__Toc383672153)

[Code](#part0000.html__Toc383672154)

[Solution](#part0000.html__Toc383672155)

[Code](#part0000.html__Toc383672156)

[8. Count the number of bits set in an unsigned number](#part0000.html__Toc383672157)

[Solution](#part0000.html__Toc383672158)

[Code](#part0000.html__Toc383672159)

[Solution for sparse bitmaps](#part0000.html__Toc383672160)

[Code](#part0000.html__Toc383672161)

[Solution for dense bitmaps](#part0000.html__Toc383672162)

[Code](#part0000.html__Toc383672163)

[Solution for 32bit integers](#part0000.html__Toc383672164)

[Code](#part0000.html__Toc383672165)

[9. Add two numbers without using arithmetic operators](#part0000.html__Toc383672166)

[Solution](#part0000.html__Toc383672167)

[Code](#part0000.html__Toc383672168)

[10. Given an array of integers where all the numbers are appearing twice find the only number which appears once](#part0000.html__Toc383672169)

[Solution](#part0000.html__Toc383672170)

[Code](#part0000.html__Toc383672171)

[11. Given an array of integers where all the numbers are appearing twice find the only two numbers which appears once](#part0000.html__Toc383672172)

[Solution](#part0000.html__Toc383672173)

[Code](#part0000.html__Toc383672174)

[12. Multiply two numbers without using arithmetic operators](#part0000.html__Toc383672175)

[Solution](#part0000.html__Toc383672176)

[Code](#part0000.html__Toc383672177)

[13. Compute the two’s complement for a given integer](#part0000.html__Toc383672178)

[Solution](#part0000.html__Toc383672179)

[Code](#part0000.html__Toc383672180)

[14. Isolate the rightmost bit set to 1](#part0000.html__Toc383672181)

[Solution](#part0000.html__Toc383672182)

[15. Create a mask for trailing zeros](#part0000.html__Toc383672183)

[Solution](#part0000.html__Toc383672184)

[16. Compute parity for a 32 bit number](#part0000.html__Toc383672185)

[Solution](#part0000.html__Toc383672186)

[Code](#part0000.html__Toc383672187)

[17. Swap two integers variables with no additional memory](#part0000.html__Toc383672188)

[Solution](#part0000.html__Toc383672189)

[Code](#part0000.html__Toc383672190)

[18. Swap bit i and j in a 64 bit number](#part0000.html__Toc383672191)

[Solution](#part0000.html__Toc383672192)

[Code](#part0000.html__Toc383672193)

[19. Reverse the order of bits in an unsigned integer](#part0000.html__Toc383672194)

[Solution](#part0000.html__Toc383672195)

[Code](#part0000.html__Toc383672196)

[20. Convert an integer to a string and a string to an integer](#part0000.html__Toc383672197)

[Solution](#part0000.html__Toc383672198)

[Code](#part0000.html__Toc383672199)

[21. Convert a number from base b1 to base b2](#part0000.html__Toc383672200)

[Solution](#part0000.html__Toc383672201)

[Code](#part0000.html__Toc383672202)

[22. Given a set S, compute the powerset of S](#part0000.html__Toc383672203)

[Solution](#part0000.html__Toc383672204)

[Code](#part0000.html__Toc383672205)

[23. Add two decimal strings representing two integers](#part0000.html__Toc383672206)

[Solution](#part0000.html__Toc383672207)

[Code](#part0000.html__Toc383672208)

[24. Generate all the bit patterns from 0 to ![](3/images/00001.jpeg) such that successive patterns differ by one bit.](#part0000.html__Toc383672209)

[Solution](#part0000.html__Toc383672210)

[Code](#part0000.html__Toc383672211)

[25. Represent  unsigned integers with variable length encoding using the continuation bit](#part0000.html__Toc383672212)

[Solution](#part0000.html__Toc383672213)

[Code](#part0000.html__Toc383672214)

[26. Represent an integer with variable length encoding using gamma encoding](#part0000.html__Toc383672215)

[Solution](#part0000.html__Toc383672216)

[Code](#part0000.html__Toc383672217)

[27. Represent an integer with variable length encoding using delta encoding](#part0000.html__Toc383672218)

[Solution](#part0000.html__Toc383672219)

[Code](#part0000.html__Toc383672220)

[28. Compute the average with no division](#part0000.html__Toc383672221)

[Solution](#part0000.html__Toc383672222)

# 1. Given an unsigned int, swap the bits in odd and even positions

## Solution

Assume that an unsigned int is 32bits and that we swap the bits in position ![](3/images/00002.jpeg) with those in position![](3/images/00003.jpeg),![](3/images/00004.jpeg). In order to select all the even bits we can AND with  bitmask 0xAAAAAAAAAA, which is a 32 bit number with even bits set (0xA is decimal 10, 1010 binary). For selecting all the odd bits we can AND with bitmask 0×55555555, which is a number with all even bits sets (0x5 is decimal5, 0101 in binary). Then we need to shift left (respectively right) of one position and OR the two intermediate results.

## Code

unsigned  int swapBits(unsigned  int  x)

{

 unsigned  int evenBits = x & 0xAAAAAAAA;

 unsigned  int oddBits  = x & 0x55555555;

              evenBits >>= 1; 

 oddBits <<= 1;  

 return (evenBits | oddBits);

}

# 2. Print the binary representation of an unsigned int

## Solution

An easy solution is to AND the ![](3/images/00005.jpeg) bit with the number ![](3/images/00006.jpeg)

## Code

void bin(unsigned  n)

{

 for (unsigned  int i = 1 << 31; i > 0; i = i >> 1)

 if (n & i) std::cout << 1;

 else std::cout << 0;

}

# 3. Compute whether or not an unsigned number is a power of two

## Solution

Suppose that the number is nonzero. If it is a power of two, than the only bit set is in position![](3/images/00007.jpeg). In this case we subtract 1, so all the bits at the left of ![](3/images/00008.jpeg)will be unset. Therefore a positive number ![](3/images/00009.jpeg) is a power of 2 if and only if ![](3/images/00010.jpeg) is 0\. Note that this check only works if ![](3/images/00011.jpeg)

## Code

bool isPowerOfTwo(unsigned n)

{ return n && (!(n & (n - 1))); }

# 4. Set the i-th bit

## Solution

For a given number n we can set the i-th bit with the expression

![](3/images/00012.jpeg)

# 5. Unset the i-th bit

## Solution

For a given number n we can unset the i-th bit with the expression

![](3/images/00013.jpeg)

# 6. Toggle the i-th bit

## Solution

For a given number n we can toggle the i-th bit with the expression

![](3/images/00014.jpeg)

# 7. Given an unsigned number with only one bit set, find the position of this bit

## Solution

If there is only one bit set, then the number must be a power of two. For identifying the position set we can AND the number with an appropriate bitmask.

## Code

unsigned  int findPosition(unsigned  int  n)

{

 unsigned  int i = 1, pos = 1;

 while (!(i & n))

 {

               i = i << 1;

               ++pos;

 }

 return pos;

}

## Solution

Another solution is using the logarithm for returning the position of the only bit set in the given unsigned ![](3/images/00009.jpeg). The code returns -1 if ![](3/images/00009.jpeg) is not a power of 2.

## Code

int findPosition2(unsigned  int  n)

{

 if (n & (n - 1))

  return -1;

 return (unsigned  int)(log((double)n) / log(2.0)) + 1;

}

## Solution

Yet another solution runs in ![](3/images/00015.jpeg). The key intuition is to perform a logarithmic binary search on the log ![](3/images/00016.jpeg)bits used for representing the unsigned int ![](3/images/00009.jpeg).

## Code

int findPosition3(unsigned  int  n)

{

 if (n & (n - 1))

  return -1;

 if (n == 1 << 31)

  return 32;

 unsigned  int position = 16;

 unsigned  int half = 1 << 15;

 unsigned  int stride = 16;

 while (1)

 {

  if (n == half)

  return position;

  else  if (n > half)

               {

  n = n >> stride;

                             position = position + (stride >> 1);

               }

  else

               {

  n = n & ((1 << stride) - 1);

                             position = position - (stride >> 1);

               }

               half = half >> (stride >> 1);

               stride >>= 1;

 }

 return position;

}

# 8. Count the number of bits set in an unsigned number

## Solution

We can simply loop and count the bits with complexity![](3/images/00017.jpeg), where ![](3/images/00016.jpeg)is the number of bits in the unsigned.

## Code

unsigned  int countBits(unsigned  int  n)

{

 unsigned  int count = 0;

 while (n)

 {

 count += n & 1;

  n >>= 1;

 }

 return count;

}

## Solution for sparse bitmaps

This solution works better for sparse unsigned s because it runs in a time proportional to the number of bits set to 1\. The line n &= (n – 1) sets the rightmost 1 in the bitmap to 0.

## Code

unsigned  int countBitsSparse(unsigned  int  n)

{

 unsigned  int count = 0;

 while (n)

 {

               count++;

  n &= (n - 1);

 }

 return count;

}

## Solution for dense bitmaps

This solution works better for dense bitmaps because it runs in a time proportional to the number of bits set to 0.  First you must toggle all the bits and then subtract the numbers of the set bits from ![](3/images/00018.jpeg). The line n &= (n – 1) sets the rightmost 1 in the bitmap to 0.

## Code

unsigned  int countBitsDense(unsigned  int  n)

{

 unsigned  int count = 8 * sizeof(unsigned  int);

 n = ~n;

 while (n)

 {

               count--;

  n &= (n - 1);

 }

 return count;

}

## Solution for 32bit integers

This solution works better for unsigned 32 bits integers. Here you use an additional lookup table containing the number of 1s enclosed in the binary representation of the 8 bit ![](3/images/00019.jpeg) number. Using pre-computed lookup tables is a commonly adopted trick for speeding up operations on lookup tables.

## Code

static  int bitInChar[256];

void fillBitsInChar()

{

 for (unsigned  int i = 0; i < 256; ++i)

               bitInChar[i] = countBits(i);

}

unsigned  int countBitsConstantFor32BitsInt(unsigned  int  n)

{

 return bitInChar[n & 0xffu] +

               bitInChar[(n >> 8) & 0xffu] +

               bitInChar[(n >> 16) & 0xffu] +

               bitInChar[(n >> 24) & 0xffu];

}

# 9. Add two numbers without using arithmetic operators

## Solution

We can use XOR for adding two bits and the AND operator for computing the carry. In the code we also implemented a subtract operation.

## Code

int add(int  x, int  y)

{

 while (y != 0)

 {

  int carry = x & y;

  x = x ^ y;

  y = carry << 1;

 }

 return  x;

}

int negate(int  x) {

 return add(~x, 1);

}

int subtract(int  x, int  y) {

 return add(x, negate(y));

}

# 10.  Given an array of integers where all the numbers are appearing twice find the only number which appears once

## Solution

We can identify the only number that appears one time by XOR’ing the array of integers. If a number is duplicate then XOR operation will be 0\. In other words, if we XOR all the numbers the result is exactly the number which appears once.

## Code

Left as exercise.

# 11.  Given an array of integers where all the numbers are appearing twice find the only two numbers which appears once

## Solution

XOR-ing all the numbers produces as result the number ![](3/images/00020.jpeg) where ![](3/images/00021.jpeg) and ![](3/images/00022.jpeg) are the only two numbers which appear once.  Let ![](3/images/00023.jpeg) be the first bit set to 1 in ![](3/images/00024.jpeg)We can partition all the numbers into sets: the numbers having the ![](3/images/00023.jpeg) bit set to 1 and the numbers having it set to 0\. Clearly n1 and n2 cannot be in the same set. So the solution of this problem has been reduced to the solution of the previous problem.

## Code

Left as exercise.

# 12.  Multiply two numbers without using arithmetic operators

## Solution

Without loss of generality let’s assume that we multiply ![](3/images/00025.jpeg), and ![](3/images/00026.jpeg). The code is dealing with the case ![](3/images/00027.jpeg). While ![](3/images/00028.jpeg)If y is even, we can multiply ![](3/images/00025.jpeg) by 2 and divide ![](3/images/00029.jpeg) by 2, otherwise we add ![](3/images/00025.jpeg) to the result and we subtract 1 to ![](3/images/00029.jpeg). The code implements the following logic.

## Code

int isEven(int  n) {

 return !(n & 1);

}

int multiply(int  x, int  y) {

 int res = 0;

 if (x < 0 && y < 0) {

  return multiply(negate(x), negate(y));

 }

 if (x >= 0 && y < 0) {

  return multiply(y, x);

 }

 while (y > 0) {

  if (isEven(y)) {

  x <<= 1 ;

  y >>= 1;

               }

  else {

 res = add(res, x);

  y = add(y, -1);

               }

 }

 return res;

}

# 13.  Compute the two’s complement for a given integer

## Solution

The two's complement of an n-bit number is the result of subtracting the number from ![](3/images/00030.jpeg). The two's complement system has the advantage that the arithmetic operations of addition, subtraction, and multiplication are identical to the ones defined for unsigned binary numbers. This requires  inputs  to be represented with the same number of bits and any overflow beyond those bits is discarded from the result.  Indeed zero has only a single representation.

## Code

int complement2(int  n)

{

 n = ~n;

 n = n + 1;

 return  n;

}

# 14.  Isolate the rightmost bit set to 1

## Solution

Let’s build some example. Suppose that ![](3/images/00031.jpeg), if we compute ![](3/images/00032.jpeg) in two’s complement we get ![](3/images/00033.jpeg). Therefore ![](3/images/00034.jpeg) selects the rightmost bit set to 1.

# 15.  Create a mask for trailing zeros

## Solution

If we are able to identify the rightmost bit set to 1, then we can create the mask for trailing zeros just subtracting 1\. The solution is therefore ![](3/images/00035.jpeg)

# 16.  Compute parity for a 32 bit number

## Solution

Given a number![](3/images/00036.jpeg), we can drop the last bit with the expression![](3/images/00037.jpeg). Then if the number of bits set to 1 is even, we return 1, otherwise we return 0.  In other words, we need to maintain a bit which changes its status from 0 to 1 as many times as the number of bits set to 1 in![](3/images/00036.jpeg). This is achieved in our code with the variable![](3/images/00038.jpeg). In many practical implementations we can avoid to process every single bit in isolation by storing a number of pre-computed parity tables for a number of bits.

## Code

unsigned  short parity(unsigned  long n)

{

 unsigned  short result = 0;

 while (n)

 {

               result ^= 1;

               n &= (n - 1);

 }

 return result;

}

static  int preComputedParity[1 << 16];

unsigned  short partityFast(_int64 n)

{

 int mask = 0xffff;

 return preComputedParity[n >> 48] ^

               preComputedParity[(n >> 32) & mask] ^

               preComputedParity[(n >> 16) & mask] ^

               preComputedParity[n  & mask];

}

# 17.  Swap two integers variables with no additional memory

## Solution

The solution uses XOR operation and it needs no additional storage. The interested reader can think about how to swap two variables which are not integers.

## Code

void swap(unsigned  int & i, unsigned  int & j)

{

 i ^= j;

 j ^= i;

 i ^= j;

}

# 18.  Swap bit i and j in a 64 bit number

## Solution

If ![](3/images/00023.jpeg) is equal to![](3/images/00039.jpeg),no swap is required. We need to swap ![](3/images/00023.jpeg) and ![](3/images/00040.jpeg) if those two bits are different, which means that they are XOR’d to 1\. If they are different, then there are only two cases possible: (0, 1) and (1, 0) and for those a XOR with 1 will swap the result. If the two bits are different, then their XOR is 0 and for any number ![](3/images/00041.jpeg). Those observations are implemented in the code below.

## Code

int swapBits(int n, unsigned  int i, unsigned  int j)

{

 if (i == j)

  return n;

 int xor = ((n >> i) ^ (n >> j)) & 1;

 return n ^ (xor << i) ^ (xor << j);

}

# 19.  Reverse the order of bits in an unsigned integer

## Solution

We simply apply the function used for swapping bits. First solution re-use the code defined for a previous exercise, while the second one manipulates bits directly.

## Code

unsigned  int reverse(unsigned  int  n)

{

 unsigned numBits = sizeof(unsigned  int) * 8;

 unsigned halfBits = numBits >> 1;

 for (unsigned  int i = 0; i < halfBits; ++i)

  n = swapBits(n, i, numBits - i - 1);

 return  n;

}

unsigned  int mirror(unsigned  int n)

{

 for (unsigned  int i = 0; i <= 15; i++)

 {

               n = (n & (0xffffffff - (1 << i) - (1 << (31 - i)))) |

                             ((n & (1 << i)) << (31 - i * 2)) |

                             ((n & (1 << (31 - i))) >> (31 - i * 2));

 }

 return n;

}

# 20.  Convert an integer to a string and a string to an integer

## Solution

For a base 10 integer![](3/images/00036.jpeg) we know that we can get the last digit with the operation ![](3/images/00042.jpeg) and that we can right shift the number with ![](3/images/00043.jpeg). Also the ASCII character for the digit ![](3/images/00044.jpeg) is ![](3/images/00045.jpeg) . If the number is negative, we need to prepend  character ‘-‘.

## Code

std::string toString(int  n)

{

 if (n == 0) return  "0";

              std::string result;

 result.reserve(10);

 if (n<0)

 {

  n = -n;

               result.push_back('-');

 }

 for (int i = log10(n); i >= 0(n); i--)

               result.push_back('0' + (n / (int)pow(10, i)) % 10);

 return result;

}

int toInt(const std::string & s)

{

 if (s.empty()) return 0;

 const  bool negative = (s[0] == '-') ? true : false;

 int result = 0;

 for (unsigned  int i = (negative ? 1 : 0);

i < s.size(); ++i)

 {

  if (isdigit(s[i]))

               {

 result = result * 10 + s[i] - '0';

               }

 }

 return (negative) ? -result : result;

}

# 21.  Convert a number from base b1 to base b2

## Solution

We can generalize the solution presented in the previous exercise. The idea is to convert from base ![](3/images/00046.jpeg) into decimal and from the decimal into base ![](3/images/00047.jpeg)

## Code

std::string convertFromBaseToBase(const std::string & s,

  unsigned  int  b1, unsigned  int  b2)

{

 if (s.empty()) return  s;

 bool negative = (s[0] == '-');

 int n = 0, reminder;

 for (unsigned  int i = (negative ? 1 : 0);

 i < s.size(); ++i)

 n = n * b1 + (isdigit(s[i]) ?

  s[i] - '0' : s[i] - 'A' + 10);

              std::string result;

 while (n)

 {

 reminder = n % b2;

               result.push_back(reminder >= 10 ?

  'A' + reminder - 10 : '0' + reminder);

 n /= b2;

 }

 if (negative)

               result.push_back('-');

              reverse(result.begin(), result.end());

 return result;

}

# 22.  Given a set S, compute the powerset of S

## Solution

The powerset of ![](3/images/00048.jpeg) is the set of all the subsets of S. For instance given the set ![](3/images/00049.jpeg) ,the powerset is![](3/images/00050.jpeg)

![](3/images/00051.jpeg).

If we represent the presence (absence) of ![](3/images/00019.jpeg) element in ![](3/images/00048.jpeg) with a bit set to 1 (respectively, 0), then we can build the powerset by generating all the bitmasks from 0 to ![](3/images/00052.jpeg) where ![](3/images/00009.jpeg) is the size of![](3/images/00053.jpeg). Note that the position of the ![](3/images/00019.jpeg) bit is given by ![](3/images/00054.jpeg).

## Code

void powerSet(const std::vector<char> & set)

{

 for (unsigned  int i = 0; i < (1 << set.size()); ++i)

 {

  unsigned  int n = i;

  while (n)

               {

  unsigned  int bit = n & ~(n - 1);

 std::cout << set[log2(bit)];

                             n &= n - 1;

               }

 std::cout << ",";

 }

}

# 23.  Add two decimal strings representing two integers

## Solution

The two strings can represent very large integers. The algorithm used for summing the value is the one taught at primary school.

## Code

int padDecimalStrings(std::string &str1, std::string &str2)

{

 int len1 = str1.size();

 int len2 = str2.size();

 if (len1 < len2)

 {

  str1.insert(0, len2 - len1, '0');

  return len2;

 }

 else  if (len1 > len2)

  str2.insert(0, len1 - len2, '0');

 return len1;

}

std::string addDecimalStrings(std::string  s1, std::string  s2)

{

 int len = padDecimalStrings(s1, s2);

 int b1, b2, sum, carry = 0;

 std::string res;

 res.resize(len);

 for (int i = len - 1; i >= 0; i--)

 {

 b1 = s1[i] - '0';

 b2 = s2[i] - '0';

               sum = (b1 + b2 + carry);

               carry = sum / 10;

               res[i] = (char)sum % 10 + '0';

 }

 if (carry)

 res = '1' + res;

 return res;

}

# 24.  Generate all the bit patterns from 0 to ![](3/images/00055.jpeg) such that successive patterns differ by one bit.

## Solution

Those patterns are named Gray code after the inventor Frank Gray[[1]](#part0000.html__ftn1).  It is convenient to generate them incrementally as![](3/images/00056.jpeg)If we analyze the pattern, we understand that any list ![](3/images/00057.jpeg) is generated from the previous list ![](3/images/00058.jpeg)  in three steps. At the beginning each element in ![](3/images/00058.jpeg) is prepended by a 0. Then the list ![](3/images/00058.jpeg) is reversed and each element is prepended by a 1\. As final step the two intermediate lists are juxtaposed to create the new list![](3/images/00059.jpeg). This process is repeated until we generate![](3/images/00060.jpeg).

## Code

void gray(unsigned  int  n)

{

 if (n == 0)

  return;

              std::vector<std::string> gray;

 gray.push_back("0");

 gray.push_back("1");

 for (int i = 2; i < (1 << n); i = i << 1)

 {

  for (int j = i - 1; j >= 0; j--)

                             gray.push_back(gray[j]);

  for (int j = 0; j < i; j++)

 gray[j] = "0" + gray[j];

  for (int j = i; j < 2 * i; j++)

 gray[j] = "1" + gray[j];

 }

 for (unsigned i = 0; i < gray.size(); i++)

               std::cout << gray[i] << std::endl;

}

# 25.  Represent  unsigned integers with variable length encoding using the continuation bit

## Solution

The key idea is to take a 64bit unsigned integer ![](3/images/00016.jpeg)and represent it with a list of bytes. For each byte seven bits are used for storing the integers with variable length encoding. In addition the most significant bit is the continuation bit and it is used to signal whether or not we need an additional byte for encoding n.  For example: if the number is less than ![](3/images/00061.jpeg) , we need only one byte where the most significant bit it set to 0. Otherwise if the number is less than ![](3/images/00062.jpeg) , we need two bytes where the first byte has the continuation bit set to 1 and the second byte has the continuation bit set to 0\. This representation is used for saving space when implementing an inverted index[[2]](#part0000.html__ftn2), a data structure frequently used by search engines. The inverted index is similar to the analytical index used to memorize the page where a word occurs in a book. The crucial intuition is to store the difference between two consecutive pages for each word and adopt a variable length encoding in order to save space.

## Code

void encodeContinuationBit(__int64  n,

std::vector<unsigned  short> & encode)

{

 __int64 x = n;

 unsigned  short e;

 if (!x) encode.push_back(0);

 while (x)

 {

               e = x & 127;

                            x >>= 7;

  if (x)

                             e |= (1 << 7);

  encode.push_back(e);

 }

}

# 26.  Represent an integer with variable length encoding using gamma encoding

## Solution

Gamma encoding is another variable length encoding for integers[[3]](#part0000.html__ftn3). The number ![](3/images/00025.jpeg) is represented with ![](3/images/00063.jpeg) bits. The integer is separated into two parts. The former is the highest power of 2 not greater than x  (say ![](3/images/00064.jpeg) and it is represented in unary with log(x) bits set to 0 followed by a 1\. The latter is the remaining binary digit representing ![](3/images/00065.jpeg).

## Code

void gammaEncoding(unsigned  int  x)

{

 int i;

 unsigned lenOfX = 0;

 for (i = x; i > 1; i >>= 1) // floor(log2(x))

               lenOfX++;

 for (i = lenOfX; i > 0; --i)

 std::cout << '0';

 std::cout << '1';

 x -= (1 << lenOfX); // reminder

 for (i = 1 << (lenOfX -1); i > 0; i >>= 1)

 if (x & i)

               std::cout << 1;

 else

               std::cout << 0;

}

# 27.  Represent an integer with variable length encoding using delta encoding

## Solution

Delta encoding is another variable length encoding for integers[[4]](#part0000.html__ftn4). The number ![](3/images/00025.jpeg) is represented with ![](3/images/00066.jpeg) bits. The integer is separated into two parts. The former one is the highest power of 2 not greater than x  (say ![](3/images/00064.jpeg) and it is represented by encoding the number ![](3/images/00067.jpeg) with gamma encoding. The latter one is the remaining binary digit representing ![](3/images/00065.jpeg).

## Code

void deltaEncoding(unsigned  int  x)

{

 int len = 0, lengthOfLen = 0, i;

 for (int i = x; i > 0; i >>= 1) // 1+floor(log2(num))

               len++;

 for (int i = len; i > 1; i >>= 1) // floor(log2(len))

               lengthOfLen++;

 for (int i = lengthOfLen; i > 0; --i)

               std::cout << 0;

 for (int i = lengthOfLen; i >= 0; --i)

               std::cout << ((len >> i) & 1);

 for (int i = len - 2; i >= 0; i--)

               std::cout << ((x >> i) & 1);

}

# 28.  Compute the average with no division

## Solution

This problem solves a bug in binary search and merge sort reported in 2006 more than 60 years after the first binary search algorithm has been published.[[5]](#part0000.html__ftn5) Binary search is typically implemented as it follows:

int binSearch(int  a[], unsigned  int  size, int  key) {

 int low = 0;

 int high = size;

 while (low <= high) {

  int mid = (low + high) / 2;

  int midVal = a[mid];

  if (midVal < key)

                             low = mid + 1;

  else  if (midVal > key)

                             high = mid - 1;

  else

  return mid; // key found

 }

 return -(low + 1); // key not found.

}

and the bug is in the line  int ![](3/images/00068.jpeg); since the sum overflow to a negative value if the sum of ![](3/images/00069.jpeg) and ![](3/images/00070.jpeg)is greater than the maximum positive int value ![](3/images/00071.jpeg). In C and C++ this causes an array index out of bounds with unpredictable results. In other languages this situation will throw and exception. The solution is to compute:

![](3/images/00072.jpeg)

It is quite amazing to think that it took more than 60 years to detect a bug in a piece of code so commonly used in the industry and studied by generations of students and academics!!

ABOUT THE AUTHOR

An experienced data mining engineer, passionate about technology and innovation in consumers’ space. Interested in search and machine learning on massive dataset with a particular focus on query analysis, suggestions, entities, personalization, freshness and universal ranking. Antonio Gullì has worked in small startups, medium (Ask.com, Tiscali) and large corporations (Microsoft). His carrier path is about mixing industry with academic experience.

“Nowadays, you must have a great combination of research skills and a just-get-it-done attitude.”

* * *

[[1]](#part0000.html__ftnref1)  [http://en.wikipedia.org/wiki/Gray_code](http://en.wikipedia.org/wiki/Gray_code)

[[2]](#part0000.html__ftnref2)  [http://en.wikipedia.org/wiki/Inverted_index](http://en.wikipedia.org/wiki/Inverted_index)

[[3]](#part0000.html__ftnref3)  [http://nlp.stanford.edu/IR-book/html/htmledition/gamma-codes-1.html](http://nlp.stanford.edu/IR-book/html/htmledition/gamma-codes-1.html)

[[4]](#part0000.html__ftnref4)  [http://nlp.stanford.edu/IR-book/html/htmledition/gamma-codes-1.html](http://nlp.stanford.edu/IR-book/html/htmledition/gamma-codes-1.html)

[[5]](#part0000.html__ftnref5)  [http://googleresearch.blogspot.co.uk/2006/06/extra-extra-read-all-about-it-nearly.html](http://googleresearch.blogspot.co.uk/2006/06/extra-extra-read-all-about-it-nearly.html)

A collection of Design Pattern Interview Questions Solved in C++

Antonio Gulli

Copyright © 2014 Antonio Gulli

All rights reserved.

ISBN:

ISBN-13:

Design Patterns is the fourth of a series of 25 Chapters devoted to algorithms, problem solving, and C++ programming.

DEDICATION

To Aurora for her joy of life

ACKNOWLEDGMENTS

Thanks to  Francesco Nidito for his code review

Contents

[Contents](#part0000.html__Toc388104055)

[Design Patterns](#part0000.html__Toc388104056)

[Creational Patterns](#part0000.html__Toc388104057)

[1. Implementing the Abstract factory pattern](#part0000.html__Toc388104058)

[Solution](#part0000.html__Toc388104059)

[2. Implementing the Builder pattern](#part0000.html__Toc388104060)

[Solution](#part0000.html__Toc388104061)

[3. Implementing the Factory pattern](#part0000.html__Toc388104062)

[Solution](#part0000.html__Toc388104063)

[4. Implementing the Prototype pattern](#part0000.html__Toc388104064)

[Solution](#part0000.html__Toc388104065)

[5. Implementing the Singleton pattern](#part0000.html__Toc388104066)

[Solution](#part0000.html__Toc388104067)

[Solution – The double checked locked pattern (DCLP)](#part0000.html__Toc388104068)

[6. Implementing the Object pool pattern](#part0000.html__Toc388104069)

[Solution](#part0000.html__Toc388104070)

[Structural Patterns](#part0000.html__Toc388104071)

[7. Implementing the Adapter pattern](#part0000.html__Toc388104072)

[Solution](#part0000.html__Toc388104073)

[8. Implementing the Bridge pattern](#part0000.html__Toc388104074)

[Solution](#part0000.html__Toc388104075)

[9. Implementing the Composite pattern](#part0000.html__Toc388104076)

[Solution](#part0000.html__Toc388104077)

[10. Implementing the Decorator pattern](#part0000.html__Toc388104078)

[Solution](#part0000.html__Toc388104079)

[11. Implementing the Façade pattern](#part0000.html__Toc388104080)

[Solution](#part0000.html__Toc388104081)

[12. Implementing the Flyweight pattern](#part0000.html__Toc388104082)

[Solution](#part0000.html__Toc388104083)

[13. Implementing the Proxy pattern](#part0000.html__Toc388104084)

[Solution](#part0000.html__Toc388104085)

[}](#part0000.html__Toc388104086)

[Behavioural Patterns](#part0000.html__Toc388104087)

[14. Implementing the Chain of responsibility pattern](#part0000.html__Toc388104088)

[Solution](#part0000.html__Toc388104089)

[15. Implementing the Command pattern](#part0000.html__Toc388104090)

[Solution](#part0000.html__Toc388104091)

[16. Implementing the Interpreter pattern](#part0000.html__Toc388104092)

[Solution](#part0000.html__Toc388104093)

[17. Implementing the Iterator pattern](#part0000.html__Toc388104094)

[Solution](#part0000.html__Toc388104095)

[18. Implementing the Mediator pattern](#part0000.html__Toc388104096)

[Solution](#part0000.html__Toc388104097)

[19. Implementing the Memento pattern](#part0000.html__Toc388104098)

[Solution](#part0000.html__Toc388104099)

[20. Implementing the Observer pattern](#part0000.html__Toc388104100)

[Solution](#part0000.html__Toc388104101)

[21. Implementing the State pattern](#part0000.html__Toc388104102)

[Solution](#part0000.html__Toc388104103)

[22. Implementing the Strategy pattern](#part0000.html__Toc388104104)

[Solution](#part0000.html__Toc388104105)

[23. Implementing the Template pattern](#part0000.html__Toc388104106)

[Solution](#part0000.html__Toc388104107)

[24. Implementing the Visitor pattern](#part0000.html__Toc388104108)

[Solution](#part0000.html__Toc388104109)

# Design Patterns

Design Patterns are a collection of logical models adopted for solving recurrent problems which are observed during the process of software development. Patterns are not dealing with core algorithms adopted by the programs but are instead providing reusable  best practise solutions for a modern software design.  For this reason algorithms are essential for computational efficiency, and patterns are critical for building scalable architectural solutions.

In Object Oriented Programming Patterns typically show relationships and interactions between classes and objects. In this book we will discuss three classes of Design patterns:

1) Creational patterns, which create objects on your behalf rather than  instantiating them directly.

2) Structural patterns, which compose interfaces by leveraging inheritance. The composition of objects allows to create new functionalities, simplify interfaces, adapt heterogeneous objects, improve performances and reduce complexity.

3) Behavioural patterns, which are used to describe  interaction and communication among objects. Behavioural patterns are also used to handle the internal state and the internal activities of each object.

Design Patterns started to be adopted in Computer Science after the publication of the book “[Design Patterns: Elements of Reusable Object-Oriented Software](http://en.wikipedia.org/wiki/Design_Patterns_(book))” by the so-called "Gang of Four" (Gamma et al.)[[1]](#part0000.html__ftn1)

# Creational Patterns

Creational patterns create objects on your behalf rather than instantiating them directly.

# 1. Implementing the Abstract factory pattern

## Solution

The intuition behind an abstract factory pattern is to encapsulate a group of factories that have a common behaviour with no need of specifying their classes. This pattern allows to exchange concrete implementations with no need of changing the code that uses those implementations. This is because the factory typically returns an abstract pointer and the client does not care about internal details.

In this example the class Widget has a pure virtual method. The two classes derived by the Widget are implementing a specific draw() behaviour. In this illustrative situation we just print a different text.

Code

namespace Abstract_Factory{

 // The Factory pattern suggests defining a

 // creation services interface in a Factory

 // base class, and implementing each "platform"

 // in a separate Factory derived class.

 class  Widget{

 public:

  virtual  void draw() = 0; // make it pure virtual

};

 class  OSX_Button : public  Widget{

 public:

  void draw() {

 std::cout << "\tOSX buttom" << std::endl;

               }

 };

 class  Windows_Button : public  Widget{

 public:

  void draw() {

 std::cout << "\tWindows buttom" << std::endl;

               }

 };

}; // end Abstract Factory

void testAbstractFactory(){

 using  namespace Creational_Patterns::Abstract_Factory;

 Widget * w = new  OSX_Button();

 w->draw();

 delete w;

}

# 2. Implementing the Builder pattern

## Solution

The builder aims at separating the construction of complex objects from their representation. Instead of using different constructors, the pattern defines a single object: the builder. This object builds the desired object step-by-step according to the configuration parameters defined by the user. The Builder is different from the Abstract factory because the former delegates the construction of the actual object to a specific auxiliary class/object, while the latter uses inheritance for exchanging concrete implementations.

In this example the class Builder is implemented according to a pure virtual method configure which is defined in each subclass for setting up the parameters used to drive  each subclass building process.  A set of specific tests based on different conditions can be added to the skeleton code for driving the specific action items taken by the ‘Simple Builder’ and by the ‘Advanced Builder’ respectively.

Code

namespace Builder{

 // Separate the construction of a complex object from its

 // representation so that the same construction process

 // can create different representations.

 class  Build{ // base class

 public:

  virtual  void configure() = 0;

 // here can add methods to see the internal state

 protected:

  int configuration_1_; // all the confs variable

  int configuration_2_; // all the confs variable

  //...

  int configuration_n_; // all the confs variable

              };

 class  SimpleBuilder : public  Build { // a derived class

 public:

               SimpleBuilder()

               {

  // here you can add explicit tests on configuration

               // parameters for driving the ‘simple builder’

// creation steps

std::cout << "\tSimple Builder" << std::endl;

               };

  void configure()

               {

  // here you can add additional configuration steps

               };

 };

 class  AdvancedBuilder : public  Build { // a derived class

 public:

               AdvancedBuilder()

               {

  // here you can add explicit tests on configuration

               // parameters for driving the ‘advanced builder’

// creation steps

std::cout << "\tAdvanced Builder" << std::endl;

               };

  void configure()

               {

  // here you can add additional configuration steps

                            };

 };

 // the class that use multiple builders

 class  ClientClass{

 public:

               ClientClass(Build * builder) : builder_(builder){};

 private:

  Build * builder_; // stores the specific builder

 };

}; // end Builder

void testBuilder(){

 using  namespace Creational_Patterns::Builder;

 Build * builder = new  AdvancedBuilder();

 Client c(builder);

 delete builder;

}

# 3. Implementing the Factory pattern

## Solution

The factory method uses factories for creating objects with no explicit need of identifying the exact class of object that will be created. Typically the factory pattern leverages the inheritance mechanism with the actual creation process delegated to subclasses. Factory is frequently used for avoiding duplication of code and for abstracting common functionalities. In this sense a superclass specifies generic behaviours by using pure virtual placeholders for creation steps. Then the superclass delegates the creation details to subclasses that are supplied by the client.

Factory patterns can be seen as a simplified version of an Abstract Factory pattern. The Factory Method pattern is responsible of creating products that belong to one family, while the Abstract Factory pattern deals with multiple families of products.  For example, with the Factory method you can produce implementations (say SUV, Station Wagons, Convertibles, ..) of one specific interface (say IAutomobile), while with the Abstract Factory method you can produce implementations of a particular Factory interface (say all the  type of automobiles given a family of vehicles including cars, trucks, caravan, and so on and so forth).

In this example we have one base class and two derived classes A and B which can be selected for exchanging the implementation according to specific needs.  The only difference with the example provided at page 10 is that OSX_Button and Windows_Button represent a particular Factory interface for the specific operative system within the families of generic buttons.

Code

namespace Factory_Method{

 // Define an interface for creating an object,

 // but let subclasses decide which class to instantiate.

 // Factory Method lets a class defer instantiation to

 // subclasses.

 //

 // Factory Method can return the same instance multiple

 // times, or can return a subclass rather than an object

 // of that exact type.

 class  Base{

 public:

  virtual  void what_to_do() = 0;

              };

 class  A : public  Base{

 public:

 A() { std::cout << "\tClass A" << std::endl; }

  void what_to_do() { };

              };

 class  B : public  Base{

 public:

 B() { std::cout << "\tClass B" << std::endl; }

  void what_to_do() { };

              };

}; // end Factory Method

void testFactoryMethod(){

 using  namespace Creational_Patterns::Factory_Method;

 Base * b = new  A();

 b->what_to_do();

 delete b;

 b = new  B();

 b->what_to_do();

 delete b;

}

# 4. Implementing the Prototype pattern

## Solution

The prototype pattern creates a prototypical instance which is then cloned for producing new objects. This pattern is very effective when the cost of cloning is less than the cost of creating a new object.

In this example we define a class Proto with a protected virtual method clone() which must be implemented by the subclasses. Different prototypes are stored in a static array and the subclasses have to register themselves.

Code

namespace Prototype{

 // Specify the kinds of objects to create using a

 // prototypical instance, and create new objects

 // by copying this prototype.

 // Declare an abstract base class that specifies a

 // pure virtual "clone" method, and, maintains a

 // dictionary of all "cloneable" concrete derived

 // classes.

 class  Base {

 public:

  virtual  Base* clone() = 0;

  virtual  void doSomething() = 0;

 };

 class  Factory {

 public:

  static  Base* makeBase(int choice);

 private:

  static  Base* s_prototypes[3];

 };

 class  A : public  Base{

 public:

  Base*   clone() { return  new  A; }

  void doSomething() {

 std::cout << "A is now doing\n";

               }

 };

 class  B : public  Base {

 public:

  Base*   clone() { return  new  B; }

  void doSomething() {

 std::cout << "B is now doing\n";

               }

 };

 Base* Factory::s_prototypes[] = {

 0, new  A, new  B

 };

 Base* Factory::makeBase(int  choice) {

  return s_prototypes[choice]->clone();

 }

 // end Protype

};

void testPrototype(){

 using  namespace Creational_Patterns::Prototype;

 Base * b = Factory::makeBase(1);

 b->doSomething();

 delete b;

}

# 5. Implementing the Singleton pattern

## Solution

This pattern restricts the instantiation of a class to one single object. In a single thread environment the constructor is typically private and a static instance is initialized only once by checking its nullness.

Code

namespace Singleton{

 // Ensure a class has only one instance,

 // and provide a global point of access to it.

 // The singleton pattern must be carefully constructed

 // in multi-threaded applications.

 // The classic solution to this problem is to use mutual

 // exclusion on the class that indicates that the object

 // is being instantiated.

 class  Single{

 public:

  static  Single * getInstance(void) {

  if (!instance_){

 instance_ = new  Single();

                             }

  return instance_;

               };

 private:

  // cannot be invoked

 Single(){ std::cout << "\tSingle" << std::endl; };

 static  Single * instance_; // a single instance

 };

 Single *Single::instance_; // force instantiation

}; // end Singleton

void testSingleton(){

 using  namespace Creational_Patterns::Singleton;

 Single * s = Single::getInstance();

 delete s;

}

## Solution – The double checked locked pattern (DCLP)

In a multi-threaded environment it is mandatory to acquire a lock() before accessing the singleton instance for not incurring in risks of conflicts across threads. This is achieved by the first code snippet reported below: the solution is always correct but it needs to always perform an expensive lock. An optimization sometimes used is the so called double checked locked pattern (DCLP), which tests for the value being null before trying to acquire a lock.[[2]](#part0000.html__ftn2)

Code

Singleton* Singleton::instance() {

Lock lock; // acquire lock 

 if (pInstance == 0) {

 pInstance = new Singleton;

 }

 return pInstance;

} // release lock (via Lock destructor)

Singleton* Singleton::instance() {

 if (pInstance == 0) { // 1st test

               Lock lock;

  if (pInstance == 0) { // 2nd test

 pInstance = new Singleton;

               }

 }

 return pInstance;

}

# 6. Implementing the Object pool pattern

## Solution

The Object pool is a pattern used for caching objects and avoiding expensive re-creations. This pattern is frequently used for objects representing the connection to a database shared among multiple clients. For instance this pattern has been used for implementing java JDBC drivers[[3]](#part0000.html__ftn3).

In this simplified example we allocated a cache of three objects but decided to adopt a very naïve cache policy which always returns the first object in the cache. More sophisticate allocation strategies can be adopted according to different needs. Also,  locking strategies should be adopted in a multi-thread environment.

Code

namespace Object_Pool{

 // Object pools are used to manage the object caching.

 // A client with access to an Object pool can avoid

 // creating a new Objects by simply asking the pool

 // for one that has already been instantiated instead.

 static  const  int num_objects = 3;

 class  Object_to_share{

 public:

               Object_to_share(){

 std::cout << "\tAn object to share" << std::endl;

               };

 };

 class  Pool{

 public:

  Object_to_share * getObject(void){

 std::cout << "\tGetting object" << std::endl;

  return &(objpool_[0]);

               }

 private:

  // could allocate dynamically

  Object_to_share objpool_[num_objects];

 };

}; // end ObjectPool

void testObjectPool(){

 using  namespace Creational_Patterns::Object_Pool;

 Object_to_share o;

 Pool p;

 p.setObject(&o);

 Object_to_share * ptr = p.getObject();

}

# Structural Patterns

Structural patterns compose interfaces by leveraging inheritance. The composition of objects allows to create new functionalities, simplify interfaces, adapt heterogeneous objects, improve performances, and reduce complexity.

# 7. Implementing the Adapter pattern

## Solution

The adapter patter is used to allow operations between classes with incompatible interfaces by means of an appropriate wrapper.

In this example the adapter class inherits publically a DesideredInterface and privately a LegacyInterface.  DesideredInterface is implemented according to a pure virtual method which is implemented by the adapter to make the existing class work with others without modifying their source code. An alternative and more modern implementation driven by templates instead of private inheritance is also provided.

Code

namespace Adapter{

 // The Adapter pattern allows otherwise incompatible

 // classes to work together by converting the interface

 // of one class into an interface expected by the

 // clients.

 class  DesiredInterface{

 public:

  virtual  void make() = 0;

 };

 class  LegacyInterface{

 public:

               LegacyInterface() {

 std::cout << "\tCalled legacy" << std::endl;

               };

 };

 // privately inherits the legacy component

 class  adapter : public  DesiredInterface,

  private  LegacyInterface{

 public:

 adapter() : LegacyInterface(){};

  void make() {

 std::cout << "\tAdapter do something "

<< std::endl;

                            }

 };

}; //end adapter

void testAdapter()

{

 using  namespace Structural_Patterns::Adapter;

 adapter * a = new  adapter();

 a->make();

 delete a;

}

template<typename  T>

struct  GenericVehicleAdapter : VehicleInterface {

 GenericVehicleAdapter(T* x) : m(x) { }

 virtual  void Run() { return m->Run(); }

 T* m;

};

void testTemplateAdapter() {

 Shuttle shuttle;

 GenericAdapter<Shuttle> vehiclelike(&shuttle);

}

# 8. Implementing the Bridge pattern

## Solution

The bridge pattern decouples the abstraction from its concrete implementation. In this way they can evolve independently. Following this patter the class itself can be considered as on specific implementation, while it is more generically seen as an abstraction. In C++ this pattern is sometime confused with the PIMPL (private implementation)[[4]](#part0000.html__ftn4). However there are differences. PIMPL is a way of hiding the implementation. This is in order to break compilation dependencies. The Bridge pattern on the other hand is a way of supporting multiple implementations.

In this example the class bridge has a pointer bridge_imp and the two illustrative subclasses a and b provide specific implementation by means of the a_imp and b_impi classes.

Code

namespace Bridge{

//

// Decouple an abstraction from its implementation so that the

// two can vary independently. This is different from

// Adapter which makes unrelated classes work together.

 class  BridgeImp{ // de-couple

 public:

               BridgeImp() {};

 protected:

  int my_data_;

 };

 class  Bridge{

 public:

               Bridge() {};

 protected:

  BridgeImp * imp_;

 };

 class  AImp : public  BridgeImp{ // implementat. hierarchy

 public:

               AImp() { my_data_ = 1; }// what you need here

};

class  A : public  Bridge{ // hierarchy

public:

               A(){

 imp_ = new  AImp();

 std::cout << "\tcreated a" << std::endl;

               };

               ~A(){

  delete imp_;

 std::cout << "\tdeleted a" << std::endl;

               }

};

class  BImp : public  BridgeImp{ // implement. hierarchy

public:

BImp() { my_data_ = 2; }; // what you need here

};

class  B : public  Bridge{ // hierarchy

public:

               B() {

 imp_ = new  BImp();

 std::cout << "\tcreated b" << std::endl;

               };

               ~B(){

  delete imp_;

 std::cout << "\tdeleted b" << std::endl;

               }

};

}; // end Bridge

void testBridge()

{

 using  namespace Structural_Patterns::Bridge;

 A bridgeA;

 B bridgeB;

}

# 9. Implementing the Composite pattern

## Solution

The composite pattern is used to compose multiple objects with common behaviour in such a way that they can be operated as one single object. A typical use is with a tree-like object composition.

In this example the Component class is implemented according to a pure virtual method traverse, which is implemented at its turn by the subclass Leaf and by the subclass Composite. In addition Composite maintains a vector of pointers where Components are inserted. This vector is used to iterate the whole structure.

Code

namespace Composite{

 // Compose objects into tree structures to represent

 // whole-part hierarchies. Recursive composition

 class  Component{

 public:

  virtual  void traverse() = 0; // pure virtual

 };

 class  Leaf : public  Component{

 private:

  int value_; // whatever you need here

 public:

               Leaf(int  val) : value_(val) {};

  void traverse() { std::cout << value_ << " "; }

 };

 class  Composite : public  Component{

 private:

               std::vector< Component * > children_;

  typedef std::vector< Component * >::const_iterator  comp_const_it;

 public:

  void add(Component * e) { children_.push_back(e); };

 void traverse()

               {

  comp_const_it it = children_.begin();

  comp_const_it it_end = children_.end();

  for (; it != it_end; ++it)

                                           (*it)->traverse();

               }

 };

}; // end composite

void testComposite(){

 using  namespace Structural_Patterns::Composite;

 Leaf l1(1);

 Leaf l2(2);

 Composite c;

 c.add(&l1); c.add(&l2);

 c.traverse();

}

# 10.  Implementing the Decorator pattern

## Solution

The decorator pattern is used to add additional behaviours to a method that is already existing for an object. In certain situations the existing behaviour is completely overridden. Those additional behaviours can be either  permanent, or transient, or dynamically added at run-time.

In this example class A_and X inherit from A and implements the virtual method make() accordingly.

Code

namespace Decorator{

 // Attach additional responsibilities to an object

 // dynamically. Decorators provide a flexible alternative

 // to subclassing for extending functionality.

 class  A{

 public:

 A() { std::cout << "\tA" << std::endl; }

 virtual  void make(void) {

 std::cout << "\t making A" << std::endl;

               }

 };

 // the decoration is private;

 class  A_and_X : public  A{

 public:

  void make(void) {

  A::make(); make_x();

               };

 private:

  void make_x() {

 std::cout << "\t making X" << std::endl;

               };

 };

}; // end Decorator

# 11.  Implementing the Façade pattern

## Solution

The façade pattern is used to provide a simplified interface to a large code segment so that the customers can only focus on the needed functionalities. This pattern is frequently used to reduce external code dependencies on the inner details of a library.

In this example three classes A, B, C are wrapped by one only class façade which simplifies the access to all former classes.

Code

namespace Facade{

 // "facade" object that provides a single, simplified

 // interface to the many individual interfaces within

 // the subsystem.

 class  A{

 public:

 A() { std::cout << "\tInit A" << std::endl; }

  void make() { std::cout << "\tmake A" << std::endl; }

 };

 class  B{

 public:

 B() { std::cout << "\tInit B" << std::endl; }

  void make() { std::cout << "\tmake B" << std::endl; }

 };

 class  C{

 public:

 C() { std::cout << "\tInit C" << std::endl; }

  void make() { std::cout << "\tmake C" << std::endl; }

 };

 Class Facade{

 public:

               Facade() { a_.make(); b_.make(); c_.make(); }

 private:

  A a_;

  B b_;

  C c_;

 };

}; //end facade

void testFacade(){

 using  namespace Structural_Patterns::Facade;

 Facade f;

}

# 12.  Implementing the Flyweight pattern

## Solution

The flyweight pattern is used for reducing the costs of creating a large number of similar objects. This is particularly important in those situations where performance is critical.

In this example Icon is a lightweight class which is stored in a vector contained within the FlyweightFactory. In this way a specific icon is nothing but a pointer to a specific object shared by every single instance of the same icon used by the windows system.

Code

namespace Flyweight{

 //The Flyweight pattern shares objects and reduce costs

 // in terms of memory and increase performance

 //

 // Clients should not instantiate Flyweights directly,

 // they should obtain them exclusively from a

 // FlyweightFactory object to shar properly.

 class  Icon { // don't have a "huge" object for each Icon

 public:

               Icon(unsigned  int  i) : shared_name_(i) {};

  unsigned  int getName(){ return shared_name_; }

 private:

  unsigned  int shared_name_;

 };

 class  FlyweightFactory{

 public:

  static  Icon * getIcon(unsigned  int  name)

               {

                             std::vector<Icon *>::const_iterator it, it_end;

                             it = icons_.begin();

                             it_end = icons_.end();

  for (; it != it_end; ++it){

  if ((*it)->getName() == name){

                                                         std::cout <<

  "\tFlyweight -> reusing an icon with name="

 << name << std::endl;

  return *it;

                                           }

                             }

                             icons_.push_back(new  Icon(name));

                             std::cout <<

  "\tCreated a new icon with name="

 << name << std::endl;

  return icons_.back();

 }; // an example: get an Icon allocated

                            ~FlyweightFactory()

               {

                             std::vector<Icon *>::const_iterator it, it_end;

                             it = icons_.begin();

                             it_end = icons_.end();

  for (; it != it_end; ++it){

  delete *it;

                             }

               }

 private:

  static std::vector<Icon *>icons_;

               };

                            std::vector<Icon *> FlyweightFactory::icons_;

// force allocation

}; // end Flyweight

void testFlyweight(){

 using  namespace Structural_Patterns::Flyweight;

 FlyweightFactory * fw = new  FlyweightFactory();

              fw->getIcon(0);

 fw->getIcon(0);

 delete fw;

}

# 13.  Implementing the Proxy pattern

## Solution

The proxy pattern is used for mediating the access to an object in those situations where a need of additional functionalities is present. Those include, but are not limited to, control of access, reduction of complexity for operation, network access, access to a file system or to a large chunk on memory and more in general access to resources.

In this example an ImageProxy class is used to access an image which could be for instance located in a remote file system.

Code

namespace Proxy{

 // The Proxy provides a surrogate to provide access to

 // an object. Example: A check or bank draft is a proxy

 // for funds in an account.

 // Decorator and Proxy have different purposes

 // but similar structures. Both describe how to provide

 // a level of indirection to another object,

 // and the implementations keep a reference to the object

 // to which they forward requests (delegation)

 class  ImageProxy{

 private:

  unsigned  int name_;

 public:

               ImageProxy(unsigned  int  name) : name_(name)

               {

 std::cout << "\tCreating image name="

                                           << name_ << std::endl;

               };

                            ~ImageProxy()

               {

 std::cout << "\tDelete image name="

                                           << name_ << std::endl;

               };

  void draw()

               {

 std::cout << "\tDraw image name="

                                           << name_ << std::endl;

               };

 };

 class  Image{

 private:

  ImageProxy * img_proxy_;

  static  unsigned  int name_;

 public:

               Image() : img_proxy_(0) {};

 ~Image() { delete img_proxy_; };

 void draw()

               {

  if (!img_proxy_)

                                           img_proxy_ =

  new  ImageProxy(name_++);

                                          img_proxy_->draw();

               }

 };

 // this is used only for example

 unsigned  int  Image::name_ = 0;

}; // end Proxy

void testProxy()

{

 using  namespace Structural_Patterns::Proxy;

 Image img;

 img.draw();

# }

# Behavioural Patterns

Behavioural patterns are used to describe  interaction and communication among objects. Behavioural patterns are also used to handle the internal state and the internal activities of each object.

# 14.  Implementing the Chain of responsibility pattern

## Solution

A chain of responsibility pattern delegates a sequence of commands to a chain of processing objects. Objects can be dynamically added to a list.

In this example a Base class maintains a list of objects Base. Derived classes can register themselves and they can also provide specific handle() for detailed information.

Code

namespace Chain_Of_Responsability{

 // Decoupling the sender of a request and its receiver

 // It gives more than one object a chance to handle

 // the request

 class  Base

 {

 public:

               Base(unsigned  int  name) : name_(name), next_(0) {};

  void add(Base* n) // add to the chain

               {

  if (next_)

  n->setPointer(next_);

 next_ = n;

               }

  void setPointer(Base * p) { next_ = p; }

 virtual  void handle(unsigned  int  who){

 if (who == name_)

 std::cout << "\t" << name_ << " is the one"

                                           << std::endl;

  if (next_)

                                           next_->handle(who);

               }

 protected:

  unsigned  int name_;

 private:

  Base * next_;

 };

 class  H1 : public  Base{

 public:

               H1(unsigned  int  name) : Base(name) {  };

 void handle(unsigned  int  who){

 std::cout << "\tHandler H1" << std::endl;

  Base::handle(who);

               }

 };

 class  H2 : public  Base{

 public:

               H2(unsigned  int  name) : Base(name) {  };

 void handle(unsigned  int  who){

 std::cout << "\tHandler H2" << std::endl;

  Base::handle(who);

               }

 };

}; // end Chain_Of_Responsability

void testChainOfResponsability(){

 using  namespace Behavioural_Patterns::Chain_Of_Responsability;

 H2 h2(2);

 H1 h1(1);

 Base b(0);

              b.add(&h1);

 b.add(&h2);

 h2.handle(2);

}

# 15.  Implementing the Command pattern

## Solution

The command pattern is used to create objects which encapsulate behaviours and states. This pattern is frequently needed when we want to delegate a sequence of calls with no need of explicitly knowing the parameter details or the specific methods here involved.

In this example the class command has a constructor which is initialized with the name of the Person and the particular commands used, which are talk() and listen().

Code

namespace Command{

 // Command decouples the object that invokes the

 // operation from the one that knows how to

 // perform it.

 class  Person;

 class  Command

 {

 private:

  Person *object_;

  void(Person:: *method_)();

 public:

               Command(Person *o = 0, void(Person:: *m)() = 0) :

                             object_(o), method_(m)

               { }

  void execute()

               {

                             (object_->*method_)();

               }

 };

 class  Person

 {

 private:

               std::string name_;

  Command cmd_;

 public:

               Person(std::string  n, Command  c) : name_(n), cmd_(c)

               {}

  void talk()

               {

 std::cout << name_ << " is talking" << std::endl;

                             cmd_.execute();

               }

  void listen()

               {

 std::cout << name_ << " is listening" <<

std::endl;

                            }

 };

}; // end command

void testCommand()

{

 using  namespace Behavioural_Patterns::Command;

 Person Angela("angela", Command());

 Person Willy("willy", Command(&Angela, &Person::listen));

 Willy.talk();

}

# 16.  Implementing the Interpreter pattern

## Solution

The Interpreter is a pattern used for implementing a specialized interpreted language. The idea is to have a class for each symbol of the grammar, used for defining the Interpreter.

In this example language is very simple and the input is taken from a stream of characters.

Code

namespace Interpreter{

 class  Interpreter

 {

 public:

  template<typename  itr>

  static void runInterpreter(itr  from, itr  to)

               {

  for (itr i = from; i != to; ++i)

                             {

  switch (*i)

                                           {

  case  'h':

 std::cout << "Hello";

  break;

  case  'w':

 std::cout << "world";

  break;

  case  ' ':

 std::cout << ' ';

  break;

  case  'n':

                                                         std::cout << endl;

  break;

  default:

 std::cout << "Unknown command";

                                           }

                             }

               }

 };

};

# 17.  Implementing the Iterator pattern

## Solution

The Iterator pattern is used to access all the elements of an object without exposing its internal representation. This pattern is commonly used by libraries of containers such as the STL for decoupling accesses to a specific container from its implementation.

In this example a stack class is accessed by means of an iterator.

Code

namespace Iterator{

 // An aggregate object such as a list should give you

 // a way to access its elements without exposing its

 // internal structure.

 class  Stack

 {

 private:

  int items_[100]; // should be dynamic

  int sp_; // current item          

 public:

  friend  class  Iterator; // friend it to access iterator

               Stack() { sp_ = -1; }

 void push(int  in) { items_[++sp_] = in; }

  int pop() { return items_[sp_--]; }

  bool isEmpty() { return (sp_ == -1); }

 };

 class  Iterator{

 private:

  const  Stack &stk_; // access the structure

  int index_;

 public:

               Iterator(const  Stack &s) : stk_(s), index_(0)

 {} // initialize the iterator

 void operator++()

               {

                             ++index_;

               }

 bool operator()() // get the end of structure

               {

  return index_ != stk_.sp_ + 1;

               }

 int operator *()

               {

  return stk_.items_[index_];

               }

 };

 bool operator == (const  Stack &s1,

  const  Stack &s2)

 {

  Iterator it1(s1), it2(s2);

 for (; it1(); ++it1, ++it2)

  if (*it1 != *it2)

  return  false;

 return  true;

 }

}; // end Iterator

void testIterator()

{

 using  namespace Behavioural_Patterns::Iterator;

 Stack s;

 Iterator it(s);

 s.push(10);

 s.push(20);

 while (it())

 {

 std::cout << *it << ' ';

               it++;

 }

}

It is worth noting that in C++ iterators are frequently implemented by using the semantic of pointers with classical operations of deference, increment, decrement and pointer comparison for indicating when the end of the container has been reached. We have already used iterators for instance in this code snippet

std::vector<Icon *>::const_iterator it, it_end;

it = icons_.begin();

it_end = icons_.end();

for (; it != it_end; ++it){

 if ((*it)->getName() == name){

               std::cout <<

  "\tFlyweight -> reusing an icon="

 << name << std::endl;

  return *it;

 }

}

# 18.  Implementing the Mediator pattern

## Solution

The Mediator allows interactions among classes with loose coupling. Each class is not required to recognize too much details of the other classes logic, which is exposed only to the mediator. Objects are not required to communicate directly anymore but they leverage the mediator, thereby reducing the coupling effects.

In this example the class list acts as a mediator among nodes.

Code

namespace Mediator{

 // Define an object that encapsulates how a set

 // of objects interact. promotes loose coupling

 //

 // for example a list mediates between node objects

 class  Node {

 private:

  int v_;

 public:

               Node(int  v) : v_(v){};

  int getValue() { return v_; }

 };

 class  List { // mediating nodes

 private:

               std::vector<Node *> values_;

  typedef std::vector<Node *>::const_iterator  const_it;

 public:

  void add(Node *n){ values_.push_back(n); }

  void traverse()

               {

  const_it it1 = values_.begin();

  const_it it2 = values_.end();

  for (; it1 != it2; it1++)

 std::cout << " " << (*it1)->getValue();

                             std::cout << std::endl;

               }

 };

}; // end mediator

void testMediator()

{

 using  namespace Behavioural_Patterns::Mediator;

 Node n1(1), n2(2), n3(3);

 List l; l.add(&n1); l.add(&n2); l.add(&n3);

 l.traverse();

}

# 19.  Implementing the Memento pattern

## Solution

Memento is a patter used to store and restore the state of an object. This is generally used for supporting undo operations, for supporting serialization, or for storing the seed of a pseudorandom number generator.

In this example a class memento is used to store a value which is saved and successively restored by the class client. More sophisticate implementations can use a vector to store multiple values and support ‘undo’ operations.

Code

namespace Memento{

 // The client requests a Memento from the source object

 // when it needs to checkpoint the source object's state

 // If the client subsequently needs to "rollback" the

 // source object's state, it hands the Memento back to

 // the source object for reinstatement.

 class  Memento{

 public:

               Memento(int  val) : value_(val) {};

  int getValue() { return value_; };

 private:

  friend  class  Client;

  int value_;

 };

 class  Client{ // client

 public:

               Client(int  value) : value_(value) {};

  void increment() { ++value_; } // change of state;

  int get_value() { return value_; }

 Memento * create_memento() {

  return  new  Memento(value_);

               }

  void restore_from_memento(Memento * m) {

 value_ = m->value_;

               }

 private:

  int value_;

              };

}; // end memento

void testMemento()

{

 using  namespace Behavioural_Patterns::Memento;

 Client c(20);

 Memento * m = c.create_memento();

 std::cout << m->getValue();

 delete m;

}

# 20.  Implementing the Observer pattern

## Solution

The Observer pattern implements the publisher/subscriber interactions, where a number of registered observer objects are informed about events produced by the publishers. This pattern is frequently used for implementing a distributed event handling system and for windows systems.

In this example the class Observer is implemented according to a pure virtual method update which is itself implemented by subclasses a_observer and b_observer. The class subject keeps a vector of observers which are notified by calling the method notify(). Note that new observers can be dynamically attached to existing lists.

Code

namespace Observer{

 // when one object changes state,

 // all its dependents are notified and

 // updated automatically.

 class  Observ{

 public:

  virtual  void update(int value) = 0;

 };

 class  AObserv : public  Observ{

 public:

  void update(int  value)

               {

 std::cout << "\ta seeing " <<

  value << std::endl;

               }

 };

 class  BObserv : public  Observ{

 public:

  void update(int  value)

               {

 std::cout << "\tb seeing " <<

  value << std::endl;

               }

 };

 class  Subject{

 private:

  int value_;

               std::vector<Observ *>  observers_;

  typedef std::vector<Observ *>::const_iterator  const_it;

 public:

  void set_value(int  value) {

 value_ = value; notify();

               }

 // attach the observers

  void attach(Observ * o) {

                             observers_.push_back(o);

               }

  void notify()

               {

  const_it it = observers_.begin(),

                                           it_end = observers_.end();

  for (; it != it_end; ++it)

                                           (*it)->update(value_);

               }

 };

}; // end observer

void testObserver()

{

 using  namespace Behavioural_Patterns::Observer;

 AObserv a;

 BObserv b;

 Subject s;

              s.attach(&a);               s.attach(&b);

 s.set_value(3);

}

# 21.  Implementing the State pattern

## Solution

The State pattern is used to allow an object to change his behaviour, when the internal state of the object itself is changing. For instance this pattern can be used to change the state of an object at run-time.

In this simple example the class state is implemented according to two virtual methods on(..) and off(..) which are at their turn implemented in the class OFF() and ON() respectively. The current state is maintained within the class tool as a pointer.

Code

namespace State {

 // Allow an object to alter its behavior when its

 // internal state changes. The object will appear

 // to change its class.

 class  tool{

 private:

  class  state * current_;

 public:

  void set_current(state * s) { current_ = s; };

  void on();

  void off();

 };

 class  state{

 public:

  virtual  void on(tool * t){

 std::cout << " state on\n";

               }

  virtual  void off(tool *t){

 std::cout << " state off\n";

               }

 };

 void  tool::on()

 {

 std::cout << "on is the state";

               current_->on(this);

 }

 void  tool::off()

 {

 std::cout << "off is the state";

               current_->off(this);

 }

 class  OFF : public  state{ // changing state OFF->on

 public:

  void on(tool * t);

 };

 class  ON : public  state{ // changing state off->ON

 public:

  void off(tool * t){

std::cout << "\tgoing from ON to OFF" <<   std::endl;

  t->set_current(new  OFF());

  delete  this;    

               }

 };

 void  OFF::on(tool * t){

std::cout << "\tgoing from OFF to ON" << std::endl;

  t->set_current(new  ON());

  delete  this;     

 }

}; // end State

void testState()

{

 using  namespace Behavioural_Patterns::State;

 Tool * t = new  Tool();

 ON * on = new  ON();

 t->set_current(on);

 on->off(t);

 delete t;

}

# 22.  Implementing the Strategy pattern

## Solution

The Strategy pattern allows selection at run-time on specific algorithms for implementing a particular behaviour given a class of similar algorithms for that function.

In this example we have two classes algo1 and algo2 derived by the superclass strategy.

Code

namespace Strategy{

 // Strategy lets the algorithm vary independently

 // from the clients that use it.

 enum  ALGO { ALGO1, ALGO2 };

 class  Strategic{

 public:

  virtual  void do_it() = 0;

 };

 class  Algo1 : public  Strategic{

 void do_it() {

 std::cout << "\tcalling algo1" << std::endl;

               }

 };

 class  Algo2 : public  Strategic{

 void do_it() {

 std::cout << "\tcalling algo2" << std::endl;

               }

 };

 class  Testbed{

 public:

                            Testbed() : strategy_(NULL) {};

  void choose_strategy(unsigned  int  what)

               {

  Strategic * tmp;

 switch (what){

  default:

  case  ALGO1:

 tmp = new  Algo1();

  delete strategy_;

                                           strategy_ = tmp;

  break;

  case  ALGO2:

 tmp = new  Algo2();

  delete strategy_;

                                           strategy_ = tmp;

  break;

                             }

                             strategy_->do_it();

               }

                            ~Testbed(){

  if (strategy_)

  delete strategy_;

               }

 private:

  Strategic * strategy_;

 };

} // end Strategy

void testStrategy()

{

 using  namespace Behavioural_Patterns::Strategy;

 Testbed tb;

 tb.choose_strategy(1);

}

# 23.  Implementing the Template pattern

## Solution

The template pattern allows the definition of  algorithms skeleton as an abstract class, where subclasses have the responsibility of providing its concrete behaviour. The word template is not related to C++ templates.

In this example the class algorithm_base has 3 basic steps a(),  b(), and c() and it is implemented according to two pure virtual methods X(), and Y() , which are then appropriately implemented by the two derived classes.

Code

namespace Template{

 // Define the skeleton of an algorithm

 // deferring some steps to client subclasses

 class  AlgorithmBase{

 void a() { std::cout << "\tA" << std::endl; }

  void b() { std::cout << "\tB" << std::endl; }

  void c() { std::cout << "\tC" << std::endl; }

  virtual  void X() = 0;

  virtual  void Y() = 0;

 public:

 void execute() { a(); X(); b();  Y(); c(); }

 };

 class  AlgorithmRefinementFirstModel : public  AlgorithmBase{

 void X() { std::cout << "\tX1" << std::endl; }

  void Y() { std::cout << "\tY1" << std::endl; }

 };

 class  AlgorithmRefinementSecondModel :public  AlgorithmBase{

 void X() { std::cout << "\tX2" << std::endl; }

  void Y() { std::cout << "\tY2" << std::endl; }

 };

} // end Template

void testTemplate()

{

 using  namespace Behavioural_Patterns::Template;

 AlgorithmBase * a = new  AlgorithmRefinementFirstModel();

 a->execute();

 delete a;

 a = new  AlgorithmRefinementSecondModel();

 a->execute();

 delete a;

}

# 24.  Implementing the Visitor pattern

## Solution

The Visitor pattern allows to visit an object in a hierarchical way with no need of considering internal details. In this way algorithms can be separated from the object structure on which they operate.

In this example the class Parent contains a vector of parent_elements pointers and a pure virtual method accept() which is then implemented by the subclasses. Two different implementations of parent visitors have been provided.

Code

namespace Visitor{

 // Represent an operation to be performed on the elements

 // of an object structure.  Operations are performed

 // without polluting internal object

 // A practical result of this separation is the ability

 // to add new operations to existing object structures

 // without modifying those structures.

 // In essence, the visitor allows one to add new

 // virtual functions to a family of classes without

 // modifying the classes themselves;

 class  A;

 class  B;

 class  C;

 class  Parent;

 // an interface for visitor

 struct  parent_element_visitor{

 virtual  void visit(A &a) const = 0;

  virtual  void visit(B &b) const = 0;

  virtual  void visit(C &c) const = 0;

  virtual  void visit(Parent &p) const = 0;

  virtual ~parent_element_visitor() {};

 };

 // interface for a single element in hierarchy

 struct  parent_element{

 virtual  void accept(const  parent_element_visitor& visitor) = 0;

  virtual ~parent_element() {};

 };

 // class in hierarchy

 class  A : public  parent_element{

 public:

 A() { std::cout << "\tcalled A" << std::endl; }

 void accept(const  parent_element_visitor & v)

               {

  v.visit(*this);

               }

 };

 // class in hierarchy

 class  B : public  parent_element{

 public:

 B() { std::cout << "\tcalled B" << std::endl; }

 void accept(const  parent_element_visitor & v)

               {

  v.visit(*this);

               }

 };

 // class in hierarchy

 class  C : public  parent_element{

 public:

 C() { std::cout << "\tcalled C" << std::endl; }

 void accept(const  parent_element_visitor & v)

               {

  v.visit(*this);

               }

 };

 // container of all the objects in hierarchy

 class  Parent{

 public:

  typedef std::vector<parent_element*>::const_iterator  const_parent_collection_it;

  typedef std::vector<parent_element*> parent_collection;

 parent_collection& getElements()

               {

  return elements_;

               }

                            Parent()

               {

                             elements_.push_back(new  A());

                             elements_.push_back(new  B());

                             elements_.push_back(new  C());

               }

               ~Parent()

               {

  for (const_parent_collection_it it = elements_.begin();

                                           it != elements_.end(); ++it)

                             {

  delete *it;

 } // call the destructors

               }

 private:

  parent_collection elements_;

 };

 // a first concrete implementation of visitor

 class  parent_model_one_visitor : public  parent_element_visitor{

 public:

  void visit(A &a) const {

 std::cout << "\tvisit A, model one"

                                           << std::endl;

               }

  void visit(B &b) const {

 std::cout << "\tvisit B, model one"

                                           << std::endl;

               }

  void visit(C &c) const {

 std::cout << "\tvisit B, model one"

                                           << std::endl;

               }

 void visit(Parent &p) const {

 Parent::parent_collection& elements =

p.getElements();

  for (Parent::const_parent_collection_it it =

                                           elements.begin();

                                           it != elements.end(); ++it){

 // calling the visitor callback

                                           (*it)->accept(*this);

                             };

               }

 };

 // a second concrete implementation of visitor

 class  parent_model_two_visitor :

  public  parent_element_visitor{

 public:

  void visit(A &a) const {

 std::cout << "\tvisit A, model two"

                                           << std::endl;

               }

  void visit(B &b) const {

 std::cout << "\tvisit B, model two"

                                           << std::endl;

               }

  void visit(C &c) const {

 std::cout << "\tvisit B, model two"

                                           << std::endl;

               }

  void visit(Parent &p) const {

 Parent::parent_collection& elements =

  p.getElements();

  for (Parent::const_parent_collection_it it =

                                           elements.begin();

                                           it != elements.end(); ++it){

 // calling the visitor callback

                                           (*it)->accept(*this);

                             };

               }

 };

}; // end visitor

void testVisitor()

{

 using  namespace Behavioural_Patterns::Visitor;

 Parent p;

 parent_element_visitor * pv = new  parent_model_one_visitor();

 pv->visit(p);

 delete pv;

 pv = new  parent_model_two_visitor();

 pv->visit(p);

 delete pv;

}

ABOUT THE AUTHOR

An experienced data mining engineer, passionate about technology and innovation in consumers’ space. Interested in search and machine learning on massive dataset with a particular focus on query analysis, suggestions, entities, personalization, freshness and universal ranking. Antonio Gullì has worked in small startups, medium (Ask.com, Tiscali) and large corporations (Microsoft). His carrier path is about mixing industry with academic experience.

“Nowadays you must have a great combination of research skills and a just-get-it-done attitude.”

* * *

*   [[1]](#part0000.html__ftnref1)  Gamma, Erich; Richard Helm, Ralph Johnson, and John Vlissides (1995). Design Patterns: Elements of Reusable Object-Oriented Software. Addison-Wesley. ISBN 0-201-63361-2.

[[2]](#part0000.html__ftnref2) Some architectures can implement code optimizations and break the correctness of the solution. The interested reader can find more information in this paper [http://www.aristeia.com/Papers/DDJ_Jul_Aug_2004_revised.pdf](http://www.aristeia.com/Papers/DDJ_Jul_Aug_2004_revised.pdf)

[[3]](#part0000.html__ftnref3)[http://docs.oracle.com/cd/E13222_01/wls/docs81/ConsoleHelp/jdbc_connection_pools.html](http://docs.oracle.com/cd/E13222_01/wls/docs81/ConsoleHelp/jdbc_connection_pools.html)

[[4]](#part0000.html__ftnref4)  [http://en.wikipedia.org/wiki/Private_class_data_pattern](http://en.wikipedia.org/wiki/Private_class_data_pattern)

A collection of Tree Programming Interview Questions Solved in C++

Antonio Gulli

Copyright © 2015 Antonio Gulli

All rights reserved.

ISBN:

ISBN-13:

“Tree” is the fifth of a series of 25 Chapters devoted to algorithms, problem solving and C++ programming.

DEDICATION

To my wife Francesca

Love always finds a path between forgiveness and karma

ACKNOWLEDGMENTS

Table of Contents

[1 Implementing a preorder visit for a Binary Tree](#part0000_split_005.html__Toc418655653)

[Solution](#part0000_split_005.html__Toc418655654)

[Code](#part0000_split_005.html__Toc418655655)

[Complexity](#part0000_split_005.html__Toc418655656)

[2 Computing the diameter of a binary tree](#part0000_split_006.html__Toc418655657)

[Solution](#part0000_split_006.html__Toc418655658)

[Code](#part0000_split_006.html__Toc418655659)

[Complexity](#part0000_split_006.html__Toc418655660)

[3 Implementing an in-order visit for a Binary Tree](#part0000_split_007.html__Toc418655661)

[Solution](#part0000_split_007.html__Toc418655662)

[Code](#part0000_split_007.html__Toc418655663)

[Complexity](#part0000_split_007.html__Toc418655664)

[4 Implementing a post-order visit for a Binary Tree](#part0000_split_008.html__Toc418655665)

[Solution](#part0000_split_008.html__Toc418655666)

[Code](#part0000_split_008.html__Toc418655667)

[Complexity](#part0000_split_008.html__Toc418655668)

[5 Implementing a level order visit for a Binary Tree](#part0000_split_009.html__Toc418655669)

[Solution](#part0000_split_009.html__Toc418655670)

[Code](#part0000_split_009.html__Toc418655671)

[Complexity](#part0000_split_009.html__Toc418655672)

[6 Counting the number of leaves in a tree](#part0000_split_010.html__Toc418655673)

[Solution](#part0000_split_010.html__Toc418655674)

[Code](#part0000_split_010.html__Toc418655675)

[Complexity](#part0000_split_010.html__Toc418655676)

[7 Checking if two binary trees are structurally identical](#part0000_split_011.html__Toc418655677)

[Solution](#part0000_split_011.html__Toc418655678)

[Code](#part0000_split_011.html__Toc418655679)

[}](#part0000_split_011.html__Toc418655680)

[Complexity](#part0000_split_011.html__Toc418655681)

[8 Printing all the paths in a binary tree](#part0000_split_012.html__Toc418655682)

[Solution](#part0000_split_012.html__Toc418655683)

[Code](#part0000_split_012.html__Toc418655684)

[Complexity](#part0000_split_012.html__Toc418655685)

[9 Verifying if a path sum is equal to an integer](#part0000_split_013.html__Toc418655686)

[Solution](#part0000_split_013.html__Toc418655687)

[Code](#part0000_split_013.html__Toc418655688)

[Complexity](#part0000_split_013.html__Toc418655689)

[10 Find the maximum path sum between two leaves of a binary tree](#part0000_split_014.html__Toc418655690)

[Solution](#part0000_split_014.html__Toc418655691)

[Code](#part0000_split_014.html__Toc418655692)

[Complexity](#part0000_split_014.html__Toc418655693)

[11 Reconstructing a tree given its pre-order and in-order traversals](#part0000_split_015.html__Toc418655694)

[Solution](#part0000_split_015.html__Toc418655695)

[Code](#part0000_split_015.html__Toc418655696)

[Complexity](#part0000_split_015.html__Toc418655697)

[12 Printing a zig-zag traversal](#part0000_split_016.html__Toc418655698)

[Solution](#part0000_split_016.html__Toc418655699)

[Code](#part0000_split_016.html__Toc418655700)

[Complexity](#part0000_split_016.html__Toc418655701)

[13 Printing the lowest common ancestor (LCA)](#part0000_split_017.html__Toc418655702)

[Solution](#part0000_split_017.html__Toc418655703)

[Code](#part0000_split_017.html__Toc418655704)

[Complexity](#part0000_split_017.html__Toc418655705)

[14 Implementing “find” and “insert” in a Binary Search Tree](#part0000_split_018.html__Toc418655706)

[Solution](#part0000_split_018.html__Toc418655707)

[Code](#part0000_split_018.html__Toc418655708)

[Complexity](#part0000_split_018.html__Toc418655709)

[15 Print a BST in order](#part0000_split_019.html__Toc418655710)

[Solution](#part0000_split_019.html__Toc418655711)

[Code](#part0000_split_019.html__Toc418655712)

[Complexity](#part0000_split_019.html__Toc418655713)

[16 Implementing findMin and findMax in a BST](#part0000_split_020.html__Toc418655714)

[Solution](#part0000_split_020.html__Toc418655715)

[Code](#part0000_split_020.html__Toc418655716)

[Complexity](#part0000_split_020.html__Toc418655717)

[17 Implementing deleteNode in a BST](#part0000_split_021.html__Toc418655718)

[Solution](#part0000_split_021.html__Toc418655719)

[Code](#part0000_split_021.html__Toc418655720)

[Complexity](#part0000_split_021.html__Toc418655721)

[18 Implementing the lowest common ancestor in a BST](#part0000_split_022.html__Toc418655722)

[Solution](#part0000_split_022.html__Toc418655723)

[Code](#part0000_split_022.html__Toc418655724)

[Complexity](#part0000_split_022.html__Toc418655725)

[19 Checking if a tree is a BST](#part0000_split_023.html__Toc418655726)

[Solution](#part0000_split_023.html__Toc418655727)

[Code](#part0000_split_023.html__Toc418655728)

[Complexity](#part0000_split_023.html__Toc418655729)

[20 Converting a Double linked list into a BST](#part0000_split_024.html__Toc418655730)

[Solution](#part0000_split_024.html__Toc418655731)

[Code](#part0000_split_024.html__Toc418655732)

[Complexity](#part0000_split_024.html__Toc418655733)

[21 Converting a BST into a Double Linked List](#part0000_split_025.html__Toc418655734)

[Solution](#part0000_split_025.html__Toc418655735)

[Code](#part0000_split_025.html__Toc418655736)

[Complexity](#part0000_split_025.html__Toc418655737)

[22 Finding the k-th element in a BST](#part0000_split_026.html__Toc418655738)

[Solution](#part0000_split_026.html__Toc418655739)

[Code](#part0000_split_026.html__Toc418655740)

[Complexity](#part0000_split_026.html__Toc418655741)

[23 Printing all the keys in a BST within a given interval](#part0000_split_027.html__Toc418655742)

[Solution](#part0000_split_027.html__Toc418655743)

[Code](#part0000_split_027.html__Toc418655744)

[Complexity](#part0000_split_027.html__Toc418655745)

[24 Merging Two Balanced Binary Search Trees](#part0000_split_028.html__Toc418655746)

[Solution](#part0000_split_028.html__Toc418655747)

[Code](#part0000_split_028.html__Toc418655748)

[Complexity](#part0000_split_028.html__Toc418655749)

[25 Finding out if there is a triplet in a Balanced BST that adds to zero](#part0000_split_029.html__Toc418655750)

[Solution](#part0000_split_029.html__Toc418655751)

[Code](#part0000_split_029.html__Toc418655752)

[Complexity](#part0000_split_029.html__Toc418655753)

[26 Implementing a B-Tree](#part0000_split_030.html__Toc418655754)

[Solution](#part0000_split_030.html__Toc418655755)

[Code](#part0000_split_030.html__Toc418655756)

[Complexity](#part0000_split_031.html__Toc418655757)

[27 Implementing a Skiplist](#part0000_split_032.html__Toc418655758)

[Solution](#part0000_split_032.html__Toc418655759)

[Code](#part0000_split_032.html__Toc418655760)

[Complexity](#part0000_split_032.html__Toc418655761)

[28 Implementing Tries](#part0000_split_033.html__Toc418655762)

[Solution](#part0000_split_033.html__Toc418655763)

[Code](#part0000_split_033.html__Toc418655764)

[29 Implementing a segment tree](#part0000_split_034.html__Toc418655765)

[Solution](#part0000_split_034.html__Toc418655766)

[Code](#part0000_split_034.html__Toc418655767)

[Complexity](#part0000_split_034.html__Toc418655768)

[30 Implementing Range minimum queries](#part0000_split_035.html__Toc418655769)

[Solution](#part0000_split_035.html__Toc418655770)

[Code](#part0000_split_035.html__Toc418655771)

[Complexity](#part0000_split_035.html__Toc418655772)

[31 Implementing a suffix tree](#part0000_split_036.html__Toc418655773)

[Solution](#part0000_split_036.html__Toc418655774)

[Code](#part0000_split_036.html__Toc418655775)

[Complexity](#part0000_split_036.html__Toc418655776)

## 1 Implementing a preorder visit for a Binary Tree

### Solution

A binary tree is a tree where every node has at most two children.  The non-recursive pre-order visit can be implemented by using a stack.

In a loop:

*   First the current node is visited.
*   Then the left children are pushed until a leaf is reached
*   Then if the stack is empty, we leave the loop. Otherwise the top of the stack is popped out and the visit continues towards the right children.

### Code

template<typename  tVal>

 struct  binaryTree

   {

 tVal v__;

 struct  binaryTree<tVal> * left;

 struct  binaryTree<tVal> * right;

      binaryTree(tVal  v) : v__(v),

         left(NULL), right(NULL) {}

   };

 template<typename  tVal>

 void nonRecursivePreOrder(binaryTree<tVal> * root)

   {

      std::stack<binaryTree<tVal> *> s;

 while (true)

      {

 //left

 while (root)

         {

std::cout << " v=" << root->v__;

            s.push(root);

 root = root->left;

         }

 if (s.empty())

 break;

 // this one

 root = s.top();

         s.pop();

 //right

 root = root->right;

      }

   }

### Complexity

Time complexity is ![](5/images/00001.jpeg) and space complexity is ![](5/images/00001.jpeg)

## 2 Computing the diameter of a binary tree

### Solution

The solution can be computed easily with the use of recursion

### Code

template<typename  tVal>

 unsigned diameter(binaryTree<tVal> * root, unsigned & dim)

   {

 unsigned left, right;

 if (!root)

 return 0;

      left = diameter(root->left, dim);

      right = diameter(root->right, dim);

 if (left + right > dim)

 dim = left + right;

 return ((left > right) ? left : right) + 1;

   }

### Complexity

Time complexity is ![](5/images/00001.jpeg) and space complexity is ![](5/images/00001.jpeg).

## 3 Implementing an in-order visit for a Binary Tree

### Solution

A non-recursive in-order visit can be implemented by using a stack.

In a loop:

*   First the left children are pushed until a leaf is reached
*   Then if the stack is empty, we leave the loop. Otherwise the top of the stack pops out and the current node is visited.
*   Finally the visit continues towards the right children

### Code

 template<typename  tVal>

 void nonRecursiveInOrder(binaryTree<tVal> * root)

   {

      std::stack<binaryTree<tVal> *> s;

 while (true)

      {

 //left

 while (root)

         {

            s.push(root);

 root = root->left;

         }

 if (s.empty())

 break;

 // this one

 root = s.top();

         s.pop();

std::cout << " v=" << root->v__;

 //right

 root = root->right;

      }

   }

### Complexity

Time complexity is ![](5/images/00001.jpeg) and space complexity is ![](5/images/00001.jpeg)

## 4 Implementing a post-order visit for a Binary Tree

### Solution

During post-ordering every single node is visited twice: the first time when moving towards the left children and then again, when moving towards the right children. In order to differentiate the two cases, we can compare if the current element and the right child of the element at the top of the stack are the same.

### Code

 template<typename  tVal>

 void nonRecursivePostOrder(binaryTree<tVal> * root)

   {

      std::stack<binaryTree<tVal> *> s;

 while (true)

      {

 if (root)

         {

            s.push(root);

 root = root->left;

         }

 else {

 if (s.empty())

 break;

 else

 if (!s.top()->right)

               {

 root = s.top();

                  s.pop();

std::cout << " v=" << root->v__;

 if (root == s.top()->right)

                  {

std::cout << " v=" << s.top()->v__;

                     s.pop();

                  }

               }

 if (!s.empty())

 root = s.top()->right;

 else

 root = NULL;

} // else

} // while

   }

### Complexity

Time complexity is ![](5/images/00001.jpeg) and space complexity is ![](5/images/00001.jpeg)

## 5 Implementing a level order visit for a Binary Tree

### Solution

Level order visits can be implemented for all nodes at one level before going to the next level. The idea is very simple.

In a loop:

*   First the root is visited
*   Then while traversing nodes at level ![](5/images/00002.jpeg)all the nodes at level ![](5/images/00003.jpeg) are stored in a queue
*   The loop is continued until all the levels are completed

### Code

template<typename  tVal>

 void nonRecursiveLevelOrder(binaryTree<tVal> * root)

   {

      std::queue<binaryTree<tVal> *> q;

 binaryTree<tVal> * tmp;

 if (!root)

 return;

      q.push(root);

 while (!q.empty())

      {

         tmp = q.front();

         q.pop();

std::cout << " v=" << tmp->v__;

 if (tmp->left)

            q.push(tmp->left);

 if (tmp->right)

            q.push(tmp->right);

      }

   }

### Complexity

Time complexity is ![](5/images/00001.jpeg) and space complexity is ![](5/images/00001.jpeg).

## 6 Counting the number of leaves in a tree

### Solution

A solution can be provided by modifying the level order visit where we increment a counter every time we reach a leaf node.

### Code

template<typename  tVal>

 unsigned NumLeavesNonRecursiveLevelOrder(binaryTree<tVal> * root)

   {

      std::queue<binaryTree<tVal> *> q;

 binaryTree<tVal> * tmp;

 unsigned count = 0;

 if (!root)

 return count;

      q.push(root);

 while (!q.empty())

      {

         tmp = q.front();

         q.pop();

 if (!tmp->left && !tmp->right)

count++; // another leaf

 else

         {

 if (tmp->left)

               q.push(tmp->left);

 if (tmp->right)

               q.push(tmp->right);

         }

      }

 return count;

   }

### Complexity

Time complexity is ![](5/images/00001.jpeg) and space complexity is ![](5/images/00001.jpeg).

## 7 Checking if two binary trees are structurally identical

### Solution

A solution can be provided by recursion. We consider as base cases when both nodes are null, or if only one of them is null. Otherwise the algorithm checks if both nodes contain the same value and if both left children and right children are recursively structurally identical.

### Code

template<typename  tVal>

 unsigned structIdentical(binaryTree<tVal> * r1, binaryTree<tVal> * r2)

   {

 if (!r1 && !r2)

 return  true;

 if (!r1 || !r2)

 return  false;

 return (r1->v__ == r2->v__ &&

         structIdentical(r1->left, r2->left) &&

         structIdentical(r1->right, r2->right));

###  }

### Complexity

Time complexity is ![](5/images/00001.jpeg) and space complexity is ![](5/images/00001.jpeg).

## 8 Printing all the paths in a binary tree

### Solution

A solution can be provided by recursion. The idea is to keep a vector ![](5/images/00004.jpeg)passing during recursion, while every node is pushed_back() to ![](5/images/00005.jpeg). Every time we reach a leaf, the vector is printed.

### Code

template<typename  tVal>

 void printAllPaths(binaryTree<tVal> * root,

      std::vector<tVal> path)

   {

 if (!root)

 return;

 path.push_back(root->v__);

 if (!root->left && !root->right)

      {

         std::vector<tVal>::iterator it = path.begin();

 for (; it != path.end(); it++)

std::cout << " v=" << *it;

         std::cout << std::endl;

      }

 else

      {

         printAllPaths(root->left, path);

         printAllPaths(root->right, path);

      }

   }

### Complexity

Time complexity is ![](5/images/00001.jpeg) and space complexity is ![](5/images/00001.jpeg).

## 9 Verifying if a path sum is equal to an integer

### Solution

The idea is to subtract the current value from the given sum, while visiting recursively the tree.

### Code

template<typename  tVal>

 bool hasSum(binaryTree<tVal> * root,

 int  sum)

   {

 if (!root)

 return (sum == 0);

 else

      {

 int remainingSum = sum - root->v__;

 if ((root->left && root->right) ||

            (!root->left && !root->right))

 return (hasSum(root->left, remainingSum) ||

            hasSum(root->right, remainingSum));

 else

 if (root->left)

 return hasSum(root->left, remainingSum);

 else

 return hasSum(root->right, remainingSum);

      }

   }

### Complexity

Time complexity is ![](5/images/00001.jpeg) and space complexity is ![](5/images/00001.jpeg).

## 10 Find the maximum path sum between two leaves of a binary tree

### Solution

The maximum path sum between two leaves can either touch the root of the three or can be located on a subtree only if it belongs to the tree itself. Hence we have the following cases of recursion:

*   The base case is when the root is NULL and we return 0
*   Then we compute recursively the maximum path sum for the left and right subtree respectively
*   Then we compute the maximum for the left subtree, for the right subtree, and for the subtree rooted at the current node. If this maximum improves the total maximum observed so far, then the total maximum is updated
*   Returning from recursion we compute the maximum between the right and left subtrees and add the weight for the current node.

### Code

template<typename  tVal>

 tVal max(tVal  a, tVal  b)

   {

 return (a >= b) ? a : b;

   }

 template<typename  tVal>

 int maxPathSum(binaryTree<tVal> * root, tVal &res)

   {

 if (!root)

 return 0;

 int lLPSum = maxPathSum(root->left, res);

 int rLPSum = maxPathSum(root->right, res);

 int curr_sum = max((lLPSum + rLPSum + root->v__),

         max(lLPSum, rLPSum));

 if (res < curr_sum)

 res = curr_sum;

 return max(lLPSum, rLPSum) + root->v__;

   }

### Complexity

Time complexity is ![](5/images/00001.jpeg) and space complexity is ![](5/images/00001.jpeg).

## 11 Reconstructing a tree given its pre-order and in-order traversals

### Solution

In a preorder visit the root is always the leftmost element of each subtree. So we start to put the leftmost element of the preorder array of visits as the root of the whole tree. Now: if we search that very element in the inorder array, we can immediately infer all elements that are before that very value, belonging to the left subtree and all elements after that same value, belonging to the right subtree. The solution can be therefore computed recursively.

### Code

 template<typename  tVal>

 unsigned search(std::vector<tVal> inorder,

 unsigned  start, unsigned  end, tVal  v)

   {

 for (unsigned i = start, i <= end; i__++)

 if (inorder[i] == v)

 return i;

   }

 template<typename  tVal>

 binaryTree<tVal> * buildBTfromInorderAndPreorder(

 const std::vector<tVal> & inOrder,

 const std::vector<tVal> & preOrder,

 unsigned & preIndex,

 unsigned  inStart, unsigned  inEnd)

   {

 binaryTree<tVal> * n;

n->v__ = preOrder[preIndex++];

 if (inStart == inEnd)

 return n;

 int inIndex =

         search(inOrder, inStart, inEnd, n->v__);

      n->left =

         buildBTfromInorderAndPreorder(inOrder, preOrder,

 inStart, inIndex - 1);

      n->right =

         buildBTfromInorderAndPreorder(inOrder, preOrder,

inIndex+1, inEnd);

   }

### Complexity

Time complexity is ![](5/images/00006.jpeg). A question for the interested reader could be, whether or not this one is the optimal complexity.

## 12 Printing a zig-zag traversal

### Solution

A Zig-Zag traversal is implemented by using two stacks which are swapped at every level. During the visit of currentLevel all children are inserted in the nextLevel stack. To be considered: a Boolean value is maintained for determining the direction of a visit (either left to right, or right to left) and this direction in reversed at every cycle. When a currentLevel stack is empty, then it is swapped with nextLevel. By using two stacks, a zig-zag visit is a variant of a level order visit.

### Code

 template<typename  tVal>

 void printZigZag(binaryTree<tVal> * root)

   {

 binaryTree<tVal> * tmp;

 bool left2right = true;

 if (!root)

 return;

      std::stack<binaryTree<tVal> *> currLevel;

      std::stack<binaryTree<tVal> *> nextLevel;

      currLevel.push(root);

 while (!currLevel.empty())

      {

         tmp = currLevel.top();

         currLevel.pop();

 if (tmp)

         {

std::cout << " v=" << tmp->v__;

 if (left2right)

            {

               nextLevel.push(tmp->left);

               nextLevel.push(tmp->right);

            }

 else

            {

               nextLevel.push(tmp->right);

               nextLevel.push(tmp->left);

            }

         }

 if (currLevel.empty())

         {

            left2right = !left2right;

            currLevel.swap(nextLevel);

         }

      }

   }

### Complexity

Time complexity is ![](5/images/00001.jpeg) and space complexity is ![](5/images/00001.jpeg).

## 13 Printing the lowest common ancestor (LCA)

### Solution

A solution can be computed recursively. The lowest common ancestor for two nodes ![](5/images/00007.jpeg) and ![](5/images/00008.jpeg) is ![](5/images/00009.jpeg)if the root is ![](5/images/00010.jpeg)Otherwise the LCA is ![](5/images/00007.jpeg) (respectively![](5/images/00011.jpeg)) if the root is ![](5/images/00007.jpeg) (respectively![](5/images/00011.jpeg)). Those are the base cases. Then the solution is recursively computed for the left and for the right subtree. After returning from recursion, if both left and right are available, then the LCA is the current root, otherwise it is left, if this is available (respectively right, if this is available).

### Code

template<typename  tVal>

 binaryTree<tVal> * LCA(binaryTree<tVal> * root,

 binaryTree<tVal> * n1, binaryTree<tVal> * n2)

   {

 if (!root)

 return  NULL;

 if (root == n1 || root == n2)

 return  root;

 binaryTree<tVal> * left =

         LCA(root->left, n1, n2);

 binaryTree<tVal> * right =

         LCA(root->right, n1, n2);

 if (left && right)

 return  root;

 else

 return (left ? left : right);

   }

### Complexity

Time complexity is ![](5/images/00001.jpeg) and space complexity is ![](5/images/00001.jpeg).

## 14 Implementing “find” and “insert” in a Binary Search Tree

### Solution

A Binary Search Tree (BST) is a tree where each node has no more than two children. The left subtree of a node contains only nodes with keys being strictly less than the node's key. The right subtree of a node contains only nodes with keys being greater than the node's key.

Find() begins by examining the [root node](http://en.wikipedia.org/wiki/Tree_(data_structure)#root_nodes). If the tree is null, the key does not exist in the tree. If the key equals the one of the root, find() returns the root. If the key is less than the one of the root, the left subtree is searched. If the key is greater than the one of the root, the right subtree is searched. This method is repeated recursively or iteratively. Here below we propose a recursive version and we leave to the interested reader the task of implementing an iterative version on his own.

Insert() follows a similar approach. The candidate key for insertion is searched inside the tree. If it is found, the process returns. Otherwise if the search reaches a null node, the key is inserted in that position. The process can be either recursive or iterative.

### Code

 template<typename  tVal>

 template<typename  tVal>

 struct  binaryTree

   {

 tVal v__;

 struct  binaryTree<tVal> * left;

 struct  binaryTree<tVal> * right;

      binaryTree(tVal  v) : v__(v),

         left(NULL), right(NULL) {}

   };

 template<typename  tVal>

 binaryTree<tVal> * find(binaryTree<tVal> * const  root,

 const  tVal  k)

   {

 if (!root)

 return  NULL;

 return ((root->v__ < k) ? find(root->right, k) :

         (root->v__ > k ? find(root->left, k) : root));

   }

 template<typename  tVal>

 void insert(binaryTree<tVal> * & root, const  tVal  k)

   {

 if (!root)

      {

 root = new  binaryTree<tVal>(k);

 return;

      }

 if (root->v__ < k)

         insert(root->right, k);

 else  if (root->v__ > k)

         insert(root->left, k);

   }

### Complexity

Average time complexity of “insert” and “find” is![](5/images/00012.jpeg)) , where ![](5/images/00013.jpeg) expresses the number of nodes in the tree. However if the tree is not balanced, complexity is![](5/images/00014.jpeg)).

## 15 Print a BST in order

### Solution

A BST is a binary tree, so the in-order visit starts with the left subtree, and then it continues with the current node and finally the right subtree.

### Code

 template<typename  tVal>

 void printInorder(binaryTree<tVal> * const  node)

   {

 if (!node)

 return;

      printInorder(node->left);

std::cout << " n=" << node->v__;

      printInorder(node->right);

   }

### Complexity

Time complexity is![](5/images/00014.jpeg)), where ![](5/images/00013.jpeg) is the number of nodes in the tree.

## 16 Implementing findMin and findMax in a BST

### Solution

The minimum key is located in the leftmost children, while the maximum key is located in the rightmost children.

### Code

 template<typename  tVal>

 binaryTree<tVal> * findMin(binaryTree<tVal> * root)

   {

 if (!root)

 return  NULL;

 while (root->left) { root = root->left; }

 return  root;

   }

 template<typename  tVal>

 binaryTree<tVal> * findMax(binaryTree<tVal> * root)

   {

 if (!root)

 return  NULL;

 while (root->right) { root = root->right; }

 return  root;

   }

### Complexity

Average time complexity is![](5/images/00012.jpeg)) , where ![](5/images/00013.jpeg) is the number of nodes in the tree. However if the tree is not balanced, complexity is![](5/images/00014.jpeg)).

## 17 Implementing deleteNode in a BST

### Solution

The code deleteNode() starts by finding the key to delete in the tree. If there is no key, the algorithm returns. Otherwise there are two different cases:

*   If the node is internal, deleteNode() finds the maximum key in the left subtree rooted to the node, where the key has been found. This maximum key replaces the searched key, which is therefore removed. Then the maximum is deleted by the left subtree.
*   If the node is external and there is one chil (either on the left or on right side) then the child replaces the father. In any case the external node is freed.

The following code implements the algorithm:

### Code

template<typename  tVal>

 binaryTree<tVal> * deleteNode(binaryTree<tVal> * root,

 const  tVal  key)

   {

 binaryTree<tVal> * tmp;

 if (!root)

 return  NULL;

 else  if (key < root->v__)

 root->left = deleteNode(root->left, key);

 else  if (key > root->v__)

 root->right = deleteNode(root->right, key);

 else {

 // internal node

 if (root->left && root->right)

         {

            tmp = findMax(root->left);

 root->v__ = tmp->v__;

 root->left = deleteNode(root->left, root->v__);

         }

 else

         {

tmp = root;

 if (root->left == NULL)

 root = root->right;

 if (root->right == NULL)

 root = root->left;

 delete tmp;

         }

      }

 return  root;

   }

### Complexity

Average time complexity is![](5/images/00012.jpeg)) , where ![](5/images/00013.jpeg) is the number of nodes in the tree. However if the tree is not balanced, complexity is![](5/images/00014.jpeg)).

## 18 Implementing the lowest common ancestor in a BST

### Solution

The lowest common ancestor (LCA) of two nodes ![](5/images/00007.jpeg) (with key ![](5/images/00015.jpeg)) and ![](5/images/00016.jpeg)(with key ![](5/images/00017.jpeg))  for a tree rooted at the root node is a node with key ![](5/images/00018.jpeg)such that either ![](5/images/00019.jpeg) or ![](5/images/00020.jpeg). If these conditions are not met, LCA navigates the three by either moving left (if ![](5/images/00021.jpeg) ) or right, otherwise until either the one of the conditions is met or an external node is reached.

### Code

 template<typename  tVal>

 binaryTree<tVal> * lca(binaryTree<tVal> * const  root,

 binaryTree<tVal> * const  n1, binaryTree<tVal> * const  n2)

   {

 if (!root || !n1 || !n2)

 return;

 while (true)

      {

 if ((n1->v__ < root->v__) && (root->v__ < n2->v__ ) ||

            (n1->v__ > root->v__) && (root->v__ > n2->v__ ))

 return  root;

 else  if (n1->v__ < root->v__)

 root = root->left;

 else

 root = root->right;

      }

   }

### Complexity

The worst case time complexity is![](5/images/00014.jpeg)).

## 19 Checking if a tree is a BST

### Solution

A solution can be computed recursively by checking if the left subtree, the current node and the right subtree follow the BST ordering. It is therefore convenient to pass the previous analyzed key by reference and compare the current node with that key.

### Code

template<typename  tVal>

 bool isBST(binaryTree<tVal> * const  root,

 tVal & prev)

   {

 if (!root)

 return  true;

 if (!isBST(root->left, prev))

 return  false;

 if (root->v__ < prev)

 return  false;

 prev = root->v__;

 return isBST(root->right, prev);

   }

### Complexity

The worst case time complexity is![](5/images/00014.jpeg)).

## 20 Converting a Double linked list into a BST

### Solution

Converting a double linked list into a BST can be easily achieved recursively. The forward pointer of the double linked list can be used as a right child of a node and the backward pointer as left child. The algorithm starts by finding the element located in the middle position of the list (this is left as an exercise). This node is the root of the BST. Then the left side and the right side are computed recursively.

### Code

 template<typename  tVal>

 struct  dLL

   {

 tVal v__;

 struct  dLL<tVal> * prev;

 struct  dLL<tVal> * next;

      dLL(tVal  v) : v__(v),

         prev(NULL), next(NULL) {}

   };

 template <typename  tVal>

 dLL<tVal> * findMiddleNode(dLL<tVal> *head);

 // left is prev

 // right is next

 template <typename  tVal>

 binaryTree<tVal> * doubleListToBST(dLL<tVal> * head)

   {

 dLL<tVal> * tmp, * p, *q;

 // head and head->next exist

 if (!head || !head->next)

 return null;

 // find middle point

      tmp = findMiddleNode(head);

 // find the precedessor

p = head;

 while (p->next != tmp)

         p = p->next;

 // break first half

p->next = NULL;

 // start next half

      q = tmp->next;  

tmp->next = NULL;

 // recurisve

      tmp->prex = doubleListToBST(head);

      tmp->next = doubleListToBST(q);

 return tmp;

   }

### Complexity

Time complexity is![](5/images/00014.jpeg)) , where ![](5/images/00013.jpeg) is the number of nodes in the list.

## 21 Converting a BST into a Double Linked List

### Solution

Converting a BST into a double linked list can be easily achieved recursively. The right child of a node can be used as forward pointer of the double linked list and the left child as backward pointer. A special case happens at the beginning, when the tail pointer of the double linked list is not defined as detailed in the code.

### Code

 template <typename  tVal>

 void bstToDoubleList(binaryTree<tVal> *root,

 binaryTree<tVal> ** head, binaryTree<tVal> ** tail)

   {

 if (!root)

 return;

 if (root->left)

         bstToDoubleList(root->left, head, tail);

 root->left = *tail;

 if (*tail)

         (*tail)->right = root;

 else

         *head = root;

      *tail = root;

 if (root->right)

         bstToDoubleList(root->right, head, tail);

   };

### Complexity

Time complexity is![](5/images/00014.jpeg)) , where ![](5/images/00013.jpeg) is the number of nodes in the list.

## 22 Finding the k-th element in a BST

### Solution

It is easy to solve the problem recursively by keeping a reference to a counter as explained in the code below.

### Code

 template<typename  tVal>

 binaryTree<tVal> * findkth(binaryTree<tVal> * const  root,

 const  tVal  k, unsigned & count)

   {

 if (!root)

 return  NULL;

 binaryTree<tVal> * left = findkth(root->left, k, count);

 if (left)

 return left;

 if (++count == k)

 return  root;

 return findkth(root->right, k, count);

   }

### Complexity

Time complexity is![](5/images/00022.jpeg)), where ![](5/images/00023.jpeg) is the position of the key to be found.

## 23 Printing all the keys in a BST within a given interval

### Solution

Given two keys ![](5/images/00024.jpeg) such that ![](5/images/00025.jpeg), the BST tree is navigated so that if the current node has a key larger or equal than ![](5/images/00023.jpeg) , the navigation continues recursively with the left children. Then the range condition is checked and if it is met, the current node is printed. Finally the navigation continues recursively with the right children.

### Code

 template<typename  tVal>

 binaryTree<tVal> * rangePrint(binaryTree<tVal> * const  root,

 const  tVal  k, const  tVal  h)

   {

 if (!root)

 return  NULL;

 if (root->v__ >= k)

         rangePrint(root->left, k, h);

 if (root->v__ >= k && root->v__ <= h)

std::cout << " v=" << root->v__;

 if (root->v__ <= h)

         rangePrint(root->right, k, h);

   }

### Complexity

The worst time complexity is![](5/images/00014.jpeg)) , where ![](5/images/00013.jpeg) is the number of nodes in the tree.

## 24 Merging Two Balanced Binary Search Trees

### Solution

The most efficient method for merging two BST is to store each one of them in an array. Then the two sorted arrays are merged and the resulting array is converted back to a new BST.

### Code

 template<typename  tVal>

 void storeInorder(binaryTree<tVal> * const  root,

      std::vector<tVal> & inorder)

   {

 if (!root)

 return;

      storeInorder(root->left, inorder);

 inorder.push_back(root->v__);

      storeInorder(root->right, inorder);

   }

 template<typename  tVal>

 void dumpVector(const std::vector<tVal> &v1)

   {

      std::cout << std::endl;

      std::vector<tVal>::const_iterator it = v1.begin();

 for (; it != v1.end(); it++)

std::cout << *it << " ";

      std::cout << std::endl;

   }

 template<typename  tVal>

 void merge(const std::vector<tVal> & v1,

 const std::vector<tVal> & v2,

      std::vector<tVal> & merged)

   {

 unsigned m = v1.size(), n = v2.size();

 if (merged.size() != n + m)

 return;

 unsigned i = 0, j = 0, k = 0;

 while (i < m && j < n)

      {

 if (v1[i] < v2[j])

 merged[k] = v1[i++];

 else

 merged[k] = v2[j++];

         k++;

      }

 while (i < m)

 merged[k++] = v1[i++];

 while (j < n)

 merged[k++] = v2[j++];

   }

 template<typename  tVal>

 binaryTree<tVal> * sortedArrayToBST(const std::vector<tVal> &v,

 int  start, int  end)

   {

 if (start > end)

 return  NULL;

 int mid = (start + end) / 2;

 binaryTree<tVal> *root =

 new  binaryTree<tVal>(v[mid]);

      root->left = sortedArrayToBST(v, start, mid - 1);

      root->right = sortedArrayToBST(v, mid + 1, end);

 return root;

   }

 template<typename  tVal>

 binaryTree<tVal> * mergeTrees(binaryTree<tVal> * const  root1,

 binaryTree<tVal>  * const  root2)

   {

      std::vector<int> v1;

      storeInorder(root1, v1);

      std::vector<int> v2;

      storeInorder(root2, v2);

      std::vector<int> merged(v1.size() + v2.size());

      merge(v1, v2, merged);

      dumpVector(merged);

 return sortedArrayToBST(merged, 0, merged.size() - 1);

   }

 template<typename  tVal>

 void dump(binaryTree<tVal> * const  root)

   {

 if (!root)

 return;

 else

std::cerr << " v==" << root->v__ << " ";

 if (root->left)

      {

std::cerr << " ->left ";

         dump(root->left);

      }

 if (root->right)

      {

std::cerr << " ->right ";

         dump(root->right);

      }

   }

}

### Complexity

This method has complexity ![](5/images/00026.jpeg) , where ![](5/images/00013.jpeg) and ![](5/images/00027.jpeg) are the numbers of nodes in the two BSTs.

## 25 Finding out if there is a triplet in a Balanced BST that adds to zero

### Solution

The optimal solution is to convert the BST into a double linked list. Then it is possible to iterate through the list and for each negative element we try to find a pair in the list,which sum is equal to the key of the current node multiplied by -1.

### Code

 template <typename  tVal>

 void bstToDoubleList(binaryTree<tVal> *root,

 binaryTree<tVal> ** head, binaryTree<tVal> ** tail)

   {

 if (!root)

 return;

 if (root->left)

         bstToDoubleList(root->left, head, tail);

 root->left = *tail;

 if (*tail)

         (*tail)->right = root;

 else

         *head = root;

      *tail = root;

 if (root->right)

         bstToDoubleList(root->right, head, tail);

   };

 template <typename  tVal>

 bool isPresentInDLL(binaryTree<tVal> * head,

 binaryTree<tVal> * tail, int  sum)

   {

 while (head != tail)

      {

 int curr = head->v__ + tail->v__;

 if (curr == sum)

 return  true;

 else  if (curr > sum)

 tail = tail->left;

 else

 head = head->right;

      }

 return  false;

   }

 template <typename  tVal>

 bool isTripletPresent(binaryTree<tVal> *root)

   {

 if (!root)

 return  false;

 binaryTree<tVal>* head = NULL;

 binaryTree<tVal>* tail = NULL;

      bstToDoubleList(root, &head, &tail);

 while ((head->right != tail) && (head->v__ < 0))

      {

 if (isPresentInDLL(head->right, tail, -1 * head->v__))

 return  true;

 else

            head = head->right;

      }

 return  false;

   }

### Complexity

This part is left to the reader as an exercise

## 26 Implementing a B-Tree

### Solution

A b-tree allows insertion and deletion in logarithmic time and it is typically used for systems that write and read large blocks of data such as databases or file systems.

In B-trees internal nodes have a variable number of children nodes within a predefined range![](5/images/00028.jpeg). When data is inserted or removed from a node, its number of children nodes changes and therefore internal nodes may be joined or split for guaranteeing that they don’t exceed the range. Each internal node of a B-tree will contain a number of sorted keys. Keys act as separation values which divide a tree into subtrees as explained in the image below. Therefore ![](5/images/00029.jpeg) is the minimum branching factor for the tree.

![http://bluerwhite.org/btree/tree1.png](5/images/00030.jpeg)

The factor of 2 will guarantee that nodes can be split or combined. If an internal node has ![](5/images/00031.jpeg) keys, then adding a key to that node can be accomplished by splitting the ![](5/images/00032.jpeg)key node into two ![](5/images/00033.jpeg) key nodes and by adding the key to the parent. Each split node maintains the required minimum number of keys. Likewise if each internal node and its neighbor have ![](5/images/00033.jpeg)keys, then a key can be deleted from the internal node by joining with its neighbor. Deleting the key would leave ![](5/images/00034.jpeg) keys to the internal node but joining the neighbor would add![](5/images/00035.jpeg)keys plus one more key coming from the neighbor's parent. The total is still ![](5/images/00031.jpeg) keys. The number of branches from a node is one more than the number of keys stored in that node. A B-tree is kept balanced by requiring that all leaf-nodes are at the same depth.

More formally a B-tree of order![](5/images/00036.jpeg) is defined as a tree which satisfies the following properties:

1.  Every node has at most ![](5/images/00037.jpeg) children.
2.  Every non-leaf node (except for the root) has at least ![](5/images/00038.jpeg) children.
3.  The root has at least two children if it is not a leaf node.
4.  A non-leaf node with ![](5/images/00023.jpeg) children contains  ![](5/images/00039.jpeg) keys.
5.  All leaves appear in the same level
6.  Each internal node’s keys act as a separation value which divides its subtrees.

It can be shown that a b-tree of height h with all its nodes completely filled has![](5/images/00040.jpeg) keys. The height of the B-tree is therefore ![](5/images/00041.jpeg) and this value makes the insert, logarithmically finds and deletes operations in the worst case

Search

This operation is similar to the one of searching a binary search tree. Starting from the root, the tree is recursively traversed from top to bottom and at each level the search chooses the subtree, which has separation keys on both sides of the search value. The search within a node can be linear or binary.

Insertion

To insert a new key, search the tree to find the leaf node, where the new key should be added:

*   If the node contains fewer than![](5/images/00042.jpeg), then there is room for the new element, which can be inserted by following the order.
*   Otherwise if the node is full and it must be split into two nodes:
    *   The median element is selected among the leaf's elements and the new element.
    *   Values less than the median one are put in the new left node and values greater than the median one are put in the new right node
    *   The median acts as a separation value.

The separation key is inserted in the node's parent, which should be split, if full. If the node is the root, we need to create a new root above the old one.

If the splitting goes all the way up to the root, it creates a new root with a single separator key and two children. When a node is split, one key goes to the parent, but one additional key is added.

Deletion

The idea is to find and delete the item, then restructure the tree to regain its invariants. This operation is left as an exercise.

### Code

#ifndef BTREE_HEAD_

#define  BTREE_HEAD_ 1

#include  <iostream>

namespace Tree{

 typedef  int  tKey;

 class  BtreeNode;

 typedef  BtreeNode * BtreeLink;

 class  BtreeNode

   {

 private:

 unsigned t__; // 2t-1 keys, 2t children

 bool leaf__; // is a leaf

 unsigned n__; // current number

 tKey * keys__; // array of key

 BtreeLink * children__; // ptr to array of children

 public:

 // constructor

      BtreeNode(unsigned  t, bool  leaf) :

         t__(t), leaf__(leaf), n__(0),

         keys__(new  tKey[2 * t__ - 1]),

         children__(new  BtreeLink[2 * t__])

      {};

 // traverse

 void traverse(unsigned  lev=0)

      {

std::cout << "lev=" << lev << " ";

 // n keys, n+1 childrens

 unsigned i = 0;

 for (; i < n__; i++)

         {

std::cout << " " << keys__[i];

 if (!leaf__)

               children__[i]->traverse(lev+1);

         }

 // last children

 if (!leaf__)

            children__[i]->traverse(lev + 1);

      };

 // delete all

 void deleteAll()

      {

 //n+1 children

 for (unsigned i = 0; i <= n__; i++)

         {

 if (!leaf__)

               children__[i]->deleteAll();

         }

 delete[] children__;

 delete[] keys__;

      };

 // dstrc

      ~BtreeNode()

      {

         deleteAll();

      }

 // search in btree

 //

 BtreeLink search(tKey  k)

      {

 unsigned i = 0;

 // search right location

 for (; i < n__ && k > keys__[i]; i++);

 // found the key

 if (keys__[i] == k)

 return  this;

 // not found

 if (leaf__)

 return  NULL;

 // recursively

 return children__[i]->search(k);

      }

 // insert in a node that is not full

 void insertNonFull(tKey  k)

      {

 // rightmost key

 int i = n__ - 1;

 if (leaf__)

         {

 // one position is available

 // so copy the keys and

 // find the right spot

 while (i >= 0 && keys__[i] > k)

            {

               keys__[i + 1] = keys__[i];

               i--;

            }

 // found the right position

keys__[i + 1] = k;

            n__++;

         }

 else  // non leaf

         {

 // find the right spot

 while (i >= 0 && keys__[i] > k)

               i--;

 // full

 // split and recursively insert

 if (children__[i + 1]->n__ == 2 * t__ - 1)

            {

               splitChild(i + 1, children__[i + 1]);

 if (keys__[i + 1] < k)

i++; // next children

            }

            children__[i + 1]->insertNonFull(k);

         }

std::cout << "traversing n==" << n__;

         traverse();

         std::cout << std::endl;

      }

 void splitChild(int  i, BtreeLink  l)

      {

 BtreeLink m = new  BtreeNode(l->t__, l->leaf__);

         m->n__ = t__ - 1;

 // copy the right keys from t to 2t-1

 for (unsigned j = 0; j < t__ - 1; j++)

m->keys__[j] = l->keys__[j + t__];

 // copy the children from t to 2t

 if (!l->leaf__)

         {

 for (unsigned j = 0; j < t__ ; j++)

m->children__[j] = l->children__[j + t__];

         }

 // one key less

 l->n__ = t__ - 1;

 // make room

 for (int j = n__ ; j >= i+1; j--)

            children__[j + 1] = children__[j];

 // connect the new node

         children__[i + 1] = m;

 // make room

 for (int j = n__ - 1; j >= i; j--)

            keys__[j + 1] = keys__[j];

 //copy the middle key

         keys__[i] = l->keys__[t__ - 1];

         n__++;

      }

 friend  class  Btree;

   };

 class  Btree

   {

 BtreeNode * root;

 unsigned t__;

 public:

      Btree(unsigned  t) :

         root(NULL), t__(t) {};

 void traverse()

      {

 if(root) root->traverse();

      }

 BtreeLink search(tKey  k)

      {

 return(root ? root->search(k) : NULL);

      }

 void insert(tKey  k)

      {

 if (!root)

         {

root = new  BtreeNode(t__, true);

root->keys__[0] = k;

            root->n__ = 1;

         }

 else

         {

 // full root

 if (root->n__ == 2 * t__ - 1)

            {

 BtreeLink btn = new  BtreeNode(t__, false);

               btn->children__[0] = root;

 // split the root

 // move 1 key to one children

               btn->splitChild(0, root);

 if (btn->keys__[0] < k)

                  btn->children__[1]->insertNonFull(k);

 else

                  btn->children__[0]->insertNonFull(k);

 // change root

               root = btn;

            }

 else

               root->insertNonFull(k);

         }

      }

   };

};

#endif

### Complexity

The table here below provides space complexity for the average and the worst case, by reporting also space and time complexity for search, insert and delete.

|  | Average case | Worst case |
| Space | ![](5/images/00043.jpeg) | ![](5/images/00043.jpeg) |
| Search | ![](5/images/00044.jpeg) | ![](5/images/00044.jpeg) |
| Insert | ![](5/images/00044.jpeg) | ![](5/images/00044.jpeg) |
| Delete | ![](5/images/00044.jpeg) | ![](5/images/00044.jpeg) |

## 27 Implementing a Skiplist

### Solution

Skiplists allow to find elements in a list with an average logarithmic time. The idea is to maintain additional pointers, which allow to skip elements as in the image.

![http://igoro.com/wordpress/wp-content/uploads/2008/07/skiplist.png](5/images/00045.jpeg)

A skip list has many layers. The bottom one is an ordinary ordered list. Each higher layer acts as "fast lane" for the lists below. In particular: an element in the ![](5/images/00046.jpeg) layer appears in the ![](5/images/00047.jpeg) layer with some probabilityp (typically ![](5/images/00048.jpeg)=0.5). Each element appears averagely in ![](5/images/00049.jpeg) lists, and the most frequent ones in![](5/images/00050.jpeg) lists.

### Code

#ifndef SKIP_HEAD_

#define  SKIP_HEAD_

#include  <iostream>

#define  DEBUG2 1

namespace Tree{

 typedef  int  num;

 template <typename  Tkey, typename  Tval>

 class  Skiplist{

 private:

 struct  node

      {

 Tkey key_; // the key

 Tval val_; // the val

 num size_; // size of array 

 node **next_; // array of pointers

         node(const  Tkey  key, const  Tval  val, num  size) :

            key_(key), val_(val), size_(size), next_(new  node*[size_])

         {

 for (num i = 0; i < size_; ++i) next_[i] = 0;

         }

      };

 typedef  node* const  link;

 Tkey default_key_; // default item in skiplist

 Tval default_val_; // default val in skiplist

 link head_; // head of skiplist

 num lgN_; // current number of link in skiplist

 num lgNmax_; // max number of link in skiplist

 // random skiplist expansion

 num rand_sl_gen__()

      {

 num i, j, t = rand(); // t is in [0, RAND_MAX]

 // generate j=2, 4, ... i < lgNmax_

 // t > RAND_MAX / 2^i

 for (i = 1, j = 2; i < lgNmax_; i++, j += j)

 if (t > RAND_MAX / j) break;             

 // t is a number < 1/2^i

 if (i > lgN_) // expand current level

lgN_ = i; // this grows logaritimcally

 return i;

      }

 // remove a key and a val

 void remove__(link  t, Tkey  key, num  k)

      {

#ifdef  DEBUG2

std::cerr << "remove__ " << t << " key="

<< key << " level=" << k << std::endl;

#endif

 if (t == 0) return; // null?

 link x = t->next_[k];// next cell

 if ((x != 0) && // not null

(x->key_ >= key)) // >=

         {

 if (key == x->key_){ // found it

 t->next_[k] = x->next_[k]; //   remove

#ifdef  DEBUG2

std::cerr << " done" << std::endl;

#endif

            }

 if (k == 0) // can delete

{ //   no more links in level

 delete x;

 return;

            }

 // try to remove one level below

            remove__(t, key, k - 1);

 return;

         }

 // x->key_ < key

 // try to remove in the same level

         remove__(t->next_[k], key, k);

      }

 // remove all keys

 void remove_all__(link  t, num  k)

      {

#ifdef DEBUG

std::cerr << "remove__ " << t << " level="

            << k << std::endl;

#endif

 if (t == 0) return;

 link x = t->next_[k];

 if (x != 0)

         {

 t->next_[k] = x->next_[k]; //   remove

 // can delete

 if (k == 0)

{ //   no more links in level

 delete x;

 return;

            }

 // try to remove one level below

            remove_all__(t, k - 1);

         }

 // x->key_ >= key

 // try to remove in the same level

         remove_all__(t->next_[k], k);

      }

 // search a key, given a link and the current level

 Tval search__(link  t, const  Tkey  key, num  k) const

      {

#ifdef DEBUG

std::cerr << "search__ " << t << " key="

<< key << " level=" << k << std::endl;

#endif

 if (t == 0) // search failed

 return default_val_;

#ifdef DEBUG

std::cerr << "key =" << key << " val = "

         << t->val_ << std::endl;

#endif

 if (key == t->key_) // search success

 return  t->val_;

 link x = t->next_[k]; // link to the next level

 if ((x == 0) || //   null?

            (key < x->key_)) //   search key < next level link's key

         {

 if (k == 0) // no more levels available

 return default_val_;

 // try previous level

 return search__(t, key, k - 1);

         }

 // key > x->key_

 //   keep searching on the same level

 return search__(x, key, k);

      }

 // insert the new node pointed by link x with level k

 void insert__(link  t, link  x, num  k)

      {

#ifdef DEBUG

std::cerr << "insert__ " << t << " " << x << " level=" << k

<< " key=" << x->key_ << " value=" << x->val_ << std::endl;

#endif

 Tkey key = x->key_; // current key

 link tk = t->next_[k]; // link to next level current link

 if ((tk == 0) || //   null?

(key < tk->key_)) //   search key < next level link's key

         {

 if (k < x->size_) // is curr lev allowed for this node?

{ //   insert:

 x->next_[k] = tk;// new node's successor is tk

 t->next_[k] = x; // t'successor is x

#ifdef DEBUG

std::cerr << "\tdone inserted key=" << key

<< " value=" << x->val_ << std::endl;

#endif

            }

 if (k == 0) // level 0

 return; //   return

 // k >= x->size__

 //  insert down a level

            insert__(t, x, k - 1);

 return; 

         }

 // k > tk->key_

insert__(tk, x, k); //   stay in the same level

      }

 public:

      Skiplist(num  lgNmax = 5) :

         head_(new  node(default_key_, default_val_, lgNmax + 1)),

         lgN_(0), lgNmax_(lgNmax) {};

      ~Skiplist(){ remove_all__(head_, lgN_); };

 // search a key and get a val

 //   start from head_ and current level reached lgN_

 inline  Tval search(const  Tkey  key) const

      {

 return search__(head_, key, lgN_);

      };

 // insert a key and a val

 // start from head_ and

 // the new randomized node with

 //   j=rand_sl_gen() links built with

 //  probability 1/t^j current level is lgN_

 //

 inline  void insert(const  Tkey  key, const  Tval  val)

      {

insert__(head_, new  node(key, val, rand_sl_gen__()), lgN_);

      };

 inline  void remove(Tkey  key)

      {

remove__(head_, key, lgN_ -1);

      }

}; // end class Skiplist

}; // end namespace Tree

#endif

### Complexity

The table here below provides space complexity for the average and the worst cases, by reporting also space and time complexity for search, insert and delete.

|  | Average case | Worst case |
| Space | ![](5/images/00043.jpeg) | ![](5/images/00051.jpeg) |
| Search | ![](5/images/00044.jpeg) | ![](5/images/00043.jpeg) |
| Insert | ![](5/images/00044.jpeg) | ![](5/images/00043.jpeg) |
| Delete | ![](5/images/00044.jpeg) | ![](5/images/00043.jpeg) |

## 28 Implementing Tries

### Solution

A trie is an ordered tree data structure used to store dynamic set or associative array, where the keys are usually strings. Typically the strings are not explicitly memorized, instead each key has a position in the tree, which defines the key with which the position is associated. All the descendants of a node have a common prefix of the string associated with that node, and the root is associated with the empty string. In the example below the trie works for an alphabet of 26 different symbols and the position of each child identifies the current symbol for the inserted string.  An example is provided in the image.

![http://www.geeksforgeeks.org/wp-content/uploads/standardtrie.png](5/images/00052.jpeg)

### Code

ifndef TRIE_HEAD_

#define  TRIE_HEAD_ 1

#include  <iostream>

// suppose the trie is for 26 chars only

#define  BRANCHLEVEL 26

namespace Tree{

 // this trie is used to memorize keys implicitely

 template <typename  Tkey>

 class  Trie{

 private:

 // a node contains a ptr to array of nodes

 struct  node

      {

 // branch for this node

 node **next;

         node() : next(new  node*[BRANCHLEVEL])

         {

 for (unsigned  int i = 0; i < BRANCHLEVEL; i++)

next[i] = NULL;

         }

      };

 typedef  node *link;

 link head; // the head

 //recursive deletion of nodes

 //

 void deleteTrie__(link  l)

      {

 if (!l)

 return;

 else

         {

 for (unsigned  int i = 0; i < BRANCHLEVEL; i++)

               deleteTrie__(l->next[i]);

 delete[] l;

         }

      }

 // specialized version for Tkey == std::string

 // this is equivalent to hash each letter

 //

 unsigned digit(std::string & k, unsigned  d)

      {

 if (d < k.length())

 return  k[d] % BRANCHLEVEL;

 else

 return  BRANCHLEVEL;

      }

 // search the key k from link l ed digit d

 bool search__(link  l, Tkey  k, unsigned  d)

      {

 // get the d-th branch value from k

 unsigned  int i = digit(k, d);

 if (i == BRANCHLEVEL) // found

 return  true;

 if (!l)

 return  false;

 // i-th branch in the tree

 return search__(l->next[i], k, d + 1);

      }

 // recursively insert considering the key

 void insert__(link& l, Tkey  k, unsigned  d)

      {

 // get the d-th branch value from k

 unsigned  int i = digit(k, d);

 if (i == BRANCHLEVEL)

 return;

 if (!l)

 l = new  node();

         insert__(l->next[i], k, d + 1);

      }

 public:

      Trie() : head(NULL) {};

      ~Trie()

      {

         deleteTrie__(head);

      }

 bool search(Tkey  k)

      {

 return search__(head, k, 0);

      }

 void insert(Tkey  k)

      {

insert__(head, k, 0);

      }

}; // end class Trie

}; // end namespace Tree

#endif

## 29 Implementing a segment tree

### Solution

Given an ![](5/images/00053.jpeg), a segment tree allows:

a) to find the sum of elements in the range ![](5/images/00054.jpeg) where ![](5/images/00055.jpeg) in time ![](5/images/00056.jpeg)

b) To update a specific element ![](5/images/00057.jpeg) such that ![](5/images/00058.jpeg)

Segment trees have the following properties

*   Leaf nodes are the elements of an![](5/images/00059.jpeg)
*   Each internal node represents a merge operation of the leaf nodes. Different types of problems have different representations of merge operations. In the code below we simply use a merge operation which sum all the leaves under the node

Frequently segment trees are represented in an array where for each node ![](5/images/00046.jpeg) the left child is in position ![](5/images/00060.jpeg) and right child is in position ![](5/images/00061.jpeg)

![the sum interval tree for [1..7]](5/images/00062.jpeg)

### Code

 inline  int getMid(int  s, int  e)

{ return  s + (e - s) / 2; }

 int getSumUtil(const  int  segmentTree[], int  segmentStart, int  segmentEnd,

 int  queryStart, int  queryEnd, int  index)

   {

 // contained in the interval

 if (queryStart <= segmentStart && segmentEnd <= queryEnd)

 return  segmentTree[index];

 // If outside interval

 if (segmentEnd < queryStart || segmentStart > queryEnd)

 return 0;

 // If a part of this segment overlaps with the given range

 unsigned mid = getMid(segmentStart, segmentEnd);

 // get the mid point and go left and right in the segmentTree

 return getSumUtil(segmentTree, segmentStart, mid,

 queryStart, queryEnd, 2 * index + 1) +

         getSumUtil(segmentTree, mid + 1, segmentEnd,

 queryStart, queryEnd, 2 * index + 2);

   }

 void updateValueUtil(int  segmentTree[], int  segmentStart, int  segmentEnd,

 int  whereToUpdate, int  valueToAdd, int  index)

   {

 // not the right interval

 if (whereToUpdate < segmentStart ||

 whereToUpdate > segmentEnd)

 return;

 // update

 segmentTree[index] += valueToAdd;

 if (segmentEnd != segmentStart)

      {

 // recursively get mid point and go left or right

 int mid = getMid(segmentStart, segmentEnd);

         updateValueUtil(segmentTree, segmentStart, mid,

 whereToUpdate, valueToAdd, 2 * index + 1);

         updateValueUtil(segmentTree, mid + 1, segmentEnd,

 whereToUpdate, valueToAdd, 2 * index + 2);

      }

   }

 void updateValue(int  array[], int  segmentTree[], int  n,

 int  whereToAdd, int  newValue)

   {

 if (whereToAdd < 0 || whereToAdd > n - 1)

 return;

 int diff = newValue - array[whereToAdd];

 array[whereToAdd] = newValue;

      updateValueUtil(segmentTree, 0, n - 1,

 whereToAdd, diff, 0);

   }

 int getSum(int  segmentTree[], int  n,

 int  queryStart, int  queryEnd)

   {

 // Check for erroneous input values

 if (queryStart < 0 || queryEnd > n - 1 ||

 queryStart > queryEnd)

 return -1;

 return getSumUtil(segmentTree, 0, n - 1,

 queryStart, queryEnd, 0);

   }

 int constructSTUtil(const  int  array[], int  segmentTree[],

 int  segmentStart, int  segmentEnd, int  segmentIndex)

   {

 if (segmentStart == segmentEnd)

      {

 segmentTree[segmentIndex] = array[segmentStart];

 return  array[segmentStart];

      }

 int mid = getMid(segmentStart, segmentEnd);

 segmentTree[segmentIndex] =

         constructSTUtil(array, segmentTree,

 segmentStart, mid, segmentIndex * 2 + 1) +

         constructSTUtil(array, segmentTree,

mid + 1, segmentEnd, segmentIndex * 2 + 2);

 return  segmentTree[segmentIndex];

   }

 int *constructSegmentTree(int  array[], int  n)

   {

 int x = (int)(ceil(log2(n))); //Height of segment tree

 int max_size = 2 * (int)pow(2, x) - 1; //Maximum size of segment tree

 int *segmentTree = new  int[max_size];

      constructSTUtil(array, segmentTree, 0, n - 1, 0);

 return segmentTree;

   }

### Complexity

Time complexity is ![](5/images/00063.jpeg)for both update and range sum operations.

## 30 Implementing Range minimum queries

### Solution

Given an ![](5/images/00053.jpeg), a segment tree allows to find the minimum in the range ![](5/images/00054.jpeg) where ![](5/images/00055.jpeg) in time ![](5/images/00056.jpeg). In this case the segment tree has the following properties

*   Leaf nodes are the elements of an![](5/images/00059.jpeg)
*   Each internal node represents the minimum of all the leaves under the node

Frequently segment trees are represented in an array where for each node ![](5/images/00046.jpeg) the left child is in position ![](5/images/00060.jpeg) and right child is in position ![](5/images/00061.jpeg)

### Code

Left as an exercise

### Complexity

Minimum is computed with ![](5/images/00056.jpeg) time complexity. However, there is a![](5/images/00001.jpeg) preprocessing time and ![](5/images/00064.jpeg)extra space required.

## 31 Implementing a suffix tree

### Solution

A Suffix Tree (also known as Pat Tree) is a tree containing all the suffixes of a given string ![](5/images/00065.jpeg). The construction of a suffix tree takes linear time and also linear space (although with very large constants). Once the suffix three is built, it is possible to solve a myriad of problems on textual strings[[1]](#part0000_split_037.html__ftn1)  such as:

*   Check a string ![](5/images/00066.jpeg) , if length m is a substring of![](5/images/00067.jpeg) in ![](5/images/00068.jpeg)time
*   Find  the longest common substrings of strings ![](5/images/00069.jpeg) and ![](5/images/00070.jpeg) in ![](5/images/00071.jpeg) time

The list is very long and cannot be reported here. The interested reader can find these articles relevant

*   [http://www.di.unipi.it/~grossi/IND/survey.pdf](http://www.di.unipi.it/~grossi/IND/survey.pdf)
*   [http://www.inf.fu-berlin.de/lehre/WS02/ALP3/material/sufficTree.pdf](http://www.inf.fu-berlin.de/lehre/WS02/ALP3/material/sufficTree.pdf)

The suffix tree for the string ![](5/images/00065.jpeg) of length ![](5/images/00013.jpeg) is defined as a tree such that:

*   The tree has exactly ![](5/images/00013.jpeg) leaves
*   Every internal node has at least two children, with the only exception of the root
*   Each edge is labeled with a non-empty substring of ![](5/images/00065.jpeg)
*   It is not allowed to have two edges starting out of a node with labels beginning with the same character
*   The string obtained by concatenating all the labels on the path from the root to leaf ![](5/images/00046.jpeg) represents suffix ![](5/images/00072.jpeg), ![](5/images/00073.jpeg)

![](5/images/00065.jpeg) is padded with a terminal symbol not seen in the string (usually denoted ![](5/images/00074.jpeg)). This ensures that no suffix is a prefix of another.

![](5/images/00075.jpeg)

### Code

The interested reader can access these libraries:

*   [http://codingplayground.blogspot.de/2010/05/suffix-tree-with-unicode-support.html](http://codingplayground.blogspot.de/2010/05/suffix-tree-with-unicode-support.html)

*   [https://code.google.com/p/patl/](https://code.google.com/p/patl/)

### Complexity

The construction of a suffix tree takes linear time and also linear space (although with very large constants).

ABOUT THE AUTHOR

An experienced data mining engineer, passionate about technology and innovation in consumers’ space. Interested in search and machine learning on massive dataset with a particular focus on query analysis, suggestions, entities, personalization, freshness and universal ranking. Antonio Gullì has worked in small startups (Ideare.com, StudioITech), medium (Ask.com, Tiscali) and large corporations (Microsoft, Elsevier). His carrier path is about mixing industry with academic experience.

“Nowadays you must have a great combination of research skills and a just-get-it-done attitude.”

* * *

[[1]](#part0000_split_036.html__ftnref1)  [http://en.wikipedia.org/wiki/Suffix_tree](http://en.wikipedia.org/wiki/Suffix_tree)

A collection of Data Science Interview Questions Solved in Python and Spark

Hands-on Big Data

and Machine Learning

(volume I)

Antonio Gulli

Copyright © 2015 Antonio Gulli

All rights reserved.

ISBN:  1517216710

ISBN-13: 978-1517216719

“Data Science” is the sixth of a series of 25 Chapters devoted to algorithms, problem solving, machine learning, big data and C++/Python programming.

DEDICATION

To Lorenzo, Leonardo, Aurora and Francesca

“I heard there was a secret chord
That David played and it pleased the Lord
But you don't really care for music, do ya?”

[Leonard Cohen, 1984]

“La tua bocca si apre al sorriso e la tua mano ad aiutare gli altri”

ACKNOWLEDGMENTS

Thanks to Eric, Francesco, Michele, Dario, Domenico, Carla, Antonio, Ettore, Federica, Laura, Antonella, Susana, and Antonello for their friendship.

Table of Contents

[1. What are the most important machine learning techniques?](#part0000_split_005.html__Toc432770255)

[Solution](#part0000_split_005.html__Toc432770256)

[2. Why is it important to have a robust set of metrics for machine learning?](#part0000_split_006.html__Toc432770257)

[Solution](#part0000_split_006.html__Toc432770258)

[Code](#part0000_split_006.html__Toc432770259)

[3. Why are Features extraction and engineering so important in machine learning?](#part0000_split_007.html__Toc432770260)

[Solution](#part0000_split_007.html__Toc432770261)

[4. Can you provide an example of features extraction?](#part0000_split_008.html__Toc432770262)

[Solution](#part0000_split_008.html__Toc432770263)

[Code](#part0000_split_008.html__Toc432770264)

[5. What is a training set, a validation set, a test set and a gold set in supervised and unsupervised learning?](#part0000_split_009.html__Toc432770265)

[Solution](#part0000_split_009.html__Toc432770266)

[6. What is a Bias - Variance tradeoff?](#part0000_split_010.html__Toc432770267)

[Solution](#part0000_split_010.html__Toc432770268)

[7. What is a cross-validation and what is an overfitting?](#part0000_split_011.html__Toc432770269)

[Solution](#part0000_split_011.html__Toc432770270)

[Code](#part0000_split_011.html__Toc432770271)

[8. Why are vectors and norms used in machine learning?](#part0000_split_012.html__Toc432770272)

[Solution](#part0000_split_012.html__Toc432770273)

[Code](#part0000_split_012.html__Toc432770274)

[9. What are Numpy, Scipy and Spark essential datatypes?](#part0000_split_013.html__Toc432770275)

[Solution](#part0000_split_013.html__Toc432770276)

[Code](#part0000_split_013.html__Toc432770277)

[10. Can you provide an example for Map and Reduce in Spark? (Let’s compute the Mean Square Error)](#part0000_split_014.html__Toc432770278)

[Solution](#part0000_split_014.html__Toc432770279)

[Code](#part0000_split_014.html__Toc432770280)

[11. Can you provide examples for other computations in Spark?](#part0000_split_015.html__Toc432770281)

[Solution](#part0000_split_015.html__Toc432770282)

[Code](#part0000_split_015.html__Toc432770283)

[12. How does Python interact with Spark](#part0000_split_016.html__Toc432770284)

[Solution](#part0000_split_016.html__Toc432770285)

[13. What is Spark support for Machine Learning?](#part0000_split_017.html__Toc432770286)

[Solution](#part0000_split_017.html__Toc432770287)

[14. How does Spark work in a parallel environment](#part0000_split_018.html__Toc432770288)

[Solution](#part0000_split_018.html__Toc432770289)

[Code](#part0000_split_018.html__Toc432770290)

[15. What is the mean, the variance, and the covariance?](#part0000_split_019.html__Toc432770291)

[Solution](#part0000_split_019.html__Toc432770292)

[Code](#part0000_split_019.html__Toc432770293)

[16. What are percentiles and quartiles?](#part0000_split_020.html__Toc432770294)

[Solution](#part0000_split_020.html__Toc432770295)

[Code](#part0000_split_020.html__Toc432770296)

[17. Can you transform an XML file into Python Pandas?](#part0000_split_021.html__Toc432770297)

[Solution](#part0000_split_021.html__Toc432770298)

[Code](#part0000_split_021.html__Toc432770299)

[18. Can you read HTML into Python Pandas?](#part0000_split_022.html__Toc432770300)

[Solution](#part0000_split_022.html__Toc432770301)

[Code](#part0000_split_022.html__Toc432770302)

[19. Can you read JSON into Python Pandas?](#part0000_split_023.html__Toc432770303)

[Solution](#part0000_split_023.html__Toc432770304)

[Code](#part0000_split_023.html__Toc432770305)

[20. Can you draw a function from Python?](#part0000_split_024.html__Toc432770306)

[Solution](#part0000_split_024.html__Toc432770307)

[Code](#part0000_split_024.html__Toc432770308)

[21. Can you represent a graph in Python?](#part0000_split_025.html__Toc432770309)

[Solution](#part0000_split_025.html__Toc432770310)

[Code](#part0000_split_025.html__Toc432770311)

[22. What is an Ipython notebook?](#part0000_split_026.html__Toc432770312)

[Solution](#part0000_split_026.html__Toc432770313)

[Code](#part0000_split_026.html__Toc432770314)

[23. What is a convenient tool for performing data statistics?](#part0000_split_027.html__Toc432770315)

[Solution](#part0000_split_027.html__Toc432770316)

[Code](#part0000_split_027.html__Toc432770317)

[24. How is it convenient to visualize data statistics](#part0000_split_028.html__Toc432770318)

[Solution](#part0000_split_028.html__Toc432770319)

[Code](#part0000_split_028.html__Toc432770320)

[25. How to compute covariance and correlation matrices with pandas](#part0000_split_029.html__Toc432770321)

[Solution](#part0000_split_029.html__Toc432770322)

[Code](#part0000_split_029.html__Toc432770323)

[26. Can you provide an example of connection to the Twitter API?](#part0000_split_030.html__Toc432770324)

[Solution](#part0000_split_030.html__Toc432770325)

[Code](#part0000_split_030.html__Toc432770326)

[27. Can you provide an example of connection to the LinkedIn API?](#part0000_split_031.html__Toc432770327)

[Solution](#part0000_split_031.html__Toc432770328)

[Code](#part0000_split_031.html__Toc432770329)

[28. Can you provide an example of connection to the Facebook API?](#part0000_split_032.html__Toc432770330)

[Solution](#part0000_split_032.html__Toc432770331)

[Code](#part0000_split_032.html__Toc432770332)

[29. What is a TFxIDF?](#part0000_split_033.html__Toc432770333)

[Solution](#part0000_split_033.html__Toc432770334)

[Code](#part0000_split_033.html__Toc432770335)

[30. What is “features hashing”? And why is it useful for BigData?](#part0000_split_034.html__Toc432770336)

[Solution](#part0000_split_034.html__Toc432770337)

[31. What is “continuous features binning”?](#part0000_split_035.html__Toc432770338)

[Solution](#part0000_split_035.html__Toc432770339)

[32. What is an ![](6/images/00001.jpeg)normalization?](#part0000_split_036.html__Toc432770340)

[Solution](#part0000_split_036.html__Toc432770341)

[Code](#part0000_split_036.html__Toc432770342)

[33. What is a Chi Square Selection?](#part0000_split_037.html__Toc432770343)

[Solution](#part0000_split_037.html__Toc432770344)

[34. What is mutual information and how can it be used for features selection?](#part0000_split_038.html__Toc432770345)

[Solution](#part0000_split_038.html__Toc432770346)

[35. What is a loss function, what are linear models, and what do we mean by regularization parameters in machine learning?](#part0000_split_039.html__Toc432770347)

[Solution](#part0000_split_039.html__Toc432770348)

[36. What is an odd ratio?](#part0000_split_040.html__Toc432770349)

[37. What is a sigmoid function and what is a logistic function?](#part0000_split_041.html__Toc432770350)

[Code](#part0000_split_041.html__Toc432770351)

[38. What is a gradient descent?](#part0000_split_042.html__Toc432770352)

[Solution](#part0000_split_042.html__Toc432770353)

[39. What is a stochastic gradient descent?](#part0000_split_043.html__Toc432770354)

[Solution](#part0000_split_043.html__Toc432770355)

[Code](#part0000_split_043.html__Toc432770356)

[40. What is a Linear Least Square Regression?](#part0000_split_044.html__Toc432770357)

[Solution](#part0000_split_044.html__Toc432770358)

[Code](#part0000_split_044.html__Toc432770359)

[41. What are Lasso, Ridge, and ElasticNet regularizations?](#part0000_split_045.html__Toc432770360)

[Solution](#part0000_split_045.html__Toc432770361)

[42. What is a Logistic Regression?](#part0000_split_046.html__Toc432770362)

[Solution](#part0000_split_046.html__Toc432770363)

[Code](#part0000_split_046.html__Toc432770364)

[43. What is a stepwise regression?](#part0000_split_047.html__Toc432770365)

[Solution](#part0000_split_047.html__Toc432770366)

[44. How to include nonlinear information into linear models](#part0000_split_048.html__Toc432770367)

[Solution](#part0000_split_048.html__Toc432770368)

[45. What is a Naïve Bayes classifier?](#part0000_split_049.html__Toc432770369)

[Solution](#part0000_split_049.html__Toc432770370)

[46. What is a Bernoulli and a Multivariate Naïve Bayes?](#part0000_split_050.html__Toc432770371)

[Solution](#part0000_split_050.html__Toc432770372)

[Code](#part0000_split_050.html__Toc432770373)

[47. What is a Gaussian?](#part0000_split_051.html__Toc432770374)

[Solution](#part0000_split_051.html__Toc432770375)

[Code](#part0000_split_051.html__Toc432770376)

[48. What is a Standard Scaling?](#part0000_split_052.html__Toc432770377)

[Solution](#part0000_split_052.html__Toc432770378)

[Code](#part0000_split_052.html__Toc432770379)

[49. Why are statistical distributions important?](#part0000_split_053.html__Toc432770380)

[Solution](#part0000_split_053.html__Toc432770381)

[Code](#part0000_split_053.html__Toc432770382)

[50. Can you compare your data with some distribution? What is a qq-plot?](#part0000_split_054.html__Toc432770383)

[Solution](#part0000_split_054.html__Toc432770384)

[Code](#part0000_split_054.html__Toc432770385)

[51. What is a Gaussian Naïve Bayes?](#part0000_split_055.html__Toc432770386)

[Solution](#part0000_split_055.html__Toc432770387)

[52. What is another way to use Naïve Bayes with continuous data?](#part0000_split_056.html__Toc432770388)

[Solution](#part0000_split_056.html__Toc432770389)

[53. What is the Nearest Neighbor classification?](#part0000_split_057.html__Toc432770390)

[Solution](#part0000_split_057.html__Toc432770391)

[Code](#part0000_split_057.html__Toc432770392)

[54. What are Support Vector Machines (SVM)?](#part0000_split_058.html__Toc432770393)

[Solution](#part0000_split_058.html__Toc432770394)

[Code](#part0000_split_058.html__Toc432770395)

[55. What are SVM Kernel tricks?](#part0000_split_059.html__Toc432770396)

[Solution](#part0000_split_059.html__Toc432770397)

[56. What is K-Means Clustering?](#part0000_split_060.html__Toc432770398)

[Solution](#part0000_split_060.html__Toc432770399)

[Code](#part0000_split_060.html__Toc432770400)

[57. Can you provide an example for Text Classification with Spark?](#part0000_split_061.html__Toc432770401)

[Solution](#part0000_split_061.html__Toc432770402)

[Code](#part0000_split_061.html__Toc432770403)

[58. Where to go from here](#part0000_split_062.html__Toc432770404)

[Appendix A](#part0000_split_063.html__Toc432770405)

[59. Ultra-Quick introduction to Python](#part0000_split_063.html__Toc432770406)

[60. Ultra-Quick introduction to Probabilities](#part0000_split_064.html__Toc432770407)

[61. Ultra-Quick introduction to Matrices and Vectors](#part0000_split_065.html__Toc432770408)

## 1. What are the most important machine learning techniques?

### Solution

In his famous essay “Computing Machinery and Intelligence”  Alan Turing asked a fundamental question "Can machines do what we (as thinking entities) can do?" Machine learning is not about thinking but more about a related activity: Learning or better, according to Arthur Samuel, the "Field of study that gives computers the ability to learn without being explicitly programmed". 

Machine learning techniques are typically classified into two categories:

In supervised learning pairs of examples made up by (inputs, desired output) are available and the computer learns a model according to which given an input, a desired output with a minimal error is predicted. Classification, Neural Networks and Regression are all examples of supervised learning. For all techniques we assume that there is an oracle or a teacher that can teach to computers what to do in order for them to apply the learned lessons on new unseen data.

In unsupervised learning computers have no teachers and they are left alone in searching for structures, patterns and anomalies in data. Clustering and Density Estimations are typical examples of unsupervised machine learning.

Let us now review the main machine learning techniques:

In classification the teacher presents pairs of (inputs, target classes) and the computer learns to attribute classes to new unseen data. Naïve Bayesian, SVM, Decision Trees and Neural Networks are all classification methodologies. The first two are discussed in this volume, while the remaining ones will be part of the next volume.

In Regression the teacher presents pairs of (inputs, continuous targets) and computers learn how to predict continuous values on new and unseen data. Linear and Logistic regression are examples which will be discussed in the present volume. Decision Trees, SVM and Neural Networks can also be used for Regression.

In Associative rule learning computers are presented with a large set of observations, all being made up of multiple variables. The task is then to learn relations between variables such us A & BC (if A and B happen, then C will also happen).

In Clustering computers learn how to partition observations in various subsets, so that each partition will be made up of similar observations according to some well-defined metric. Algorithms like K-Means and DBSCAN belong also to this class.

In Density estimation computers learn how to find statistical values that describe data. Algorithms like Expectation Maximization belong also to this class.

## 2. Why is it important to have a robust set of metrics for machine learning?

### Solution

Any machine learning technique should be evaluated by using metrics for analytically assessing the quality of results. For instance: if we need to categorize objects such as people, movies or songs into different classes, precision and recall might be suitable metrics.

Precision is the ratio![](6/images/00002.jpeg) where ![](6/images/00003.jpeg) is the number of true positives and ![](6/images/00004.jpeg)is the number of false positives. Recall is the ratio![](6/images/00005.jpeg) where![](6/images/00006.jpeg) is the number of true positives and ![](6/images/00007.jpeg)is the number of false negatives. True and false are attributes derived by using manually created data. Precision and Recall are typically reported in a 2-d graph known as P/R Curves, where different algorithmic graphs can be compared by reporting the achieved Precision for fixed values of Recall.

In addition, F1 is another frequently used metric, which combines Precision and Recall into a single value:

![](6/images/00008.jpeg)

Scikit-learn provides a comprehensive set of metrics for classification, clustering, regression, ranking and pairwise judgment[[1]](#part0000_split_066.html__ftn1). As an example the code below computes Precision and Recall.

### Code

import numpy as np

from sklearn.metrics import precision_recall_curve

y_true = np.array([0,1,1,0,  1])

y_scores = np.array([0.5,  0.6,  0.38,  0.9,  1])

precision, recall, thresholds = precision_recall_curve(y_true, y_scores)

print precision

print recall

## 3. Why are Features extraction and engineering so important in machine learning?

### Solution

The Features are the selected variables for making predictions. For instance, suppose you’d like to forecast whether tomorrow there will be a sunny day then you will probably pick features like humidity (a numerical value), speed of wind (another numeric value), some historical information (what happened during the last few years), whether or not it is sunny today (a categorical value yes/no) and a few other features. Your choice can dramatically impact on your model for the same algorithm and you need to run multiple experiments in order to find what the right amount of data and what the right features are in order to forecast with minimal error. It is not unusual to have problems represented by thousands of features and combinations of them and a good feature engineer will use tools for stack ranking features according to their contribution in reducing the error for prediction.

Different authors use different names for different features including attributes, variables and predictors. In this book we consistently use features. 

Features can be categorical such as marital status, gender, state of residence, place of birth, or numerical such as age, income, height and weight. This distinction is important because certain algorithms such as linear regression work only with numerical attributes and if categorical features are present,              they need to be somehow encoded into numerical values.

In other words, feature engineering is the art of extracting, selecting and transforming essential characteristics representing data. It is sometimes considered less glamourous than machine learning algorithms but in reality any experienced Data Scientist knows that a simple algorithm on a well-chosen set of features performs better than a sophisticated algorithm on a not so good set of features.

Also simple algorithms are frequently easier to implement in a distributed way and therefore they scale well with large datasets. So the rule of thumb is in what Galileo already said many centuries ago: “Simplicity is the ultimate sophistication”. Pick your algorithm carefully and spend a lot of time in investigating your data and in creating meaningful summaries with appropriate feature engineering.

Real world objects are complex and features are used to analytically represent those objects. From one hand this representation has an inherent error which can be reduced by carefully selecting a right set of representatives. From the other hand we might not want to create a too complex representation because it might be computationally expensive for the machine to learn a sophisticate model, indeed such model could possibly not generalize well to the unseen data.

Real world data is noisy. We might have very few instances (outliers) which show a sensible difference from the majority of the remaining data, while the selected algorithm should be resilient enough to outliers.

Real world data might have redundant information. When we extract features, we might be interested in optimizing simplicity of learned models and discard new features which show a high correlation with the already observed ones.

ETL is the process of Extraction, Transformation and Loading of features from real data for creating various learning sets. Transformation in particular refers to operations such as features weighting, high correlated features discarding, the creation of synthetic features derivative of the one observed in the data and the reduction of high dimension features space into a lower one by using either hashing or rather sophisticate space projection techniques.  For example in this book we discuss:

*   TFxIDF, an example of features weighting used in text classification
*   ChiSquare, an example of filtering of highly correlated features
*   Kernel Trick, an example of creation of derivative features
*   Hashing, a simple technique to reduce feature space dimensions
*   Binning, an example of transformation of continuous features into a discrete one. New synthetic features might be created in order to represent the bins.

## 4. Can you provide an example of features extraction?

### Solution

Let’s suppose that we want to perform machine learning on textual files. The first step is to extract meaningful feature vectors from a text. A typical representation is the so called bag of words where:

a) Each word  ![](6/images/00009.jpeg) in the text collection is associated with a unique integer![](6/images/00010.jpeg) assigned to it.

b) For each document![](6/images/00011.jpeg), the number of occurrences of each word ![](6/images/00009.jpeg) is computed and this value is stored in a matrix![](6/images/00012.jpeg). Please, note that ![](6/images/00013.jpeg) is typically a sparse matrix because when a word is not present in a document, its count will be zero.

Numpy, Scikit-learn and Spark all support sparse vectors[[2]](#part0000_split_066.html__ftn2). Let’s see an example where we start to load a dataset made up of Usenet articles[[3]](#part0000_split_066.html__ftn3) where the alt.atheism category is considered and the collection of text documents is converted into a matrix of token counts. We then print the![](6/images/00014.jpeg).

### Code

from sklearn.datasets import fetch_20newsgroups

from sklearn.feature_extraction.text import CountVectorizer

categories =  ['alt.atheism']

newsgroups_train = fetch_20newsgroups(subset='train', categories=categories)

count_vect = CountVectorizer()

Train_counts = count_vect.fit_transform(newsgroups_train.data)

print count_vect.vocabulary_.get(u'man')

## 5. What is a training set, a validation set, a test set and a gold set in supervised and unsupervised learning?

### Solution

In machine learning a set of true labels is called the gold set. This set of examples is typically built manually either by human experts or via crowdsourcing with tools like the Amazon Mechanical Turk[[4]](#part0000_split_066.html__ftn4) or via explicit/implicit feedback collected by users online. For instance: a gold set can contain news articles that are manually assigned to different categories by experts of the various subjects, or it might contain movies with associated rating provided by Netflix users, or ratings of images collected via crowdsourcing.

Supervised machine learning consists of four phases:

1.  Training phase: A sample extracted by the gold set is used to learn a family of data models. Each model can be generated from this family by choosing an appropriate set of hyper-parameters, i.e. factors which can be used for algorithms fine-tuning s;
2.  Validation phase: The best learned model is selected from the family by picking hyper-parameters which minimize a computed error function on a gold set sample called “validation set”; This phase is used for identifying the best configuration for a given algorithm;
3.  Test phase: The error for the best learned model is evaluated on a gold set sample called “test set”. This phase is useful for comparing models built by adopting different algorithms;
4.  Application phase: The learned model is applied to the real-world data.

Two additional observations can be here highlighted: first, the training set, the validation set and the test set are all sampled from the same gold set but those samples are independent. Second, it has been assumed that the learned model can be described by means of two different functions ![](6/images/00015.jpeg) and ![](6/images/00016.jpeg) combined by using a set of hyper-parameters![](6/images/00017.jpeg).

Unsupervised machine learning consists in tests and application phases only because there is no model to be learned a-priori. In fact unsupervised algorithms adapt dynamically to the observed data.

## 6. What is a Bias - Variance tradeoff?

### Solution

Bias and Variance are two independent sources of errors for machine learning which prevent algorithms to generalize the models learned beyond the training set.

*   Bias is the error representing missing relations between features and outputs. In machine learning this phenomenon is called underfitting.
*   Variance is the error representing sensitiveness to small training data fluctuations. In machine learning this phenomenon is called overfitting.

A good learning algorithm should capture patterns in the training data (low bias), but it should also generalize well with unseen application data (low variance). In general, a complex model can show low bias because it captures many relations in the training data and, at the same time, it can show high variance because it will not necessarily generalize well. The opposite happens with models with high bias and low variance. In many algorithms an error can be analytically decomposed in three components: bias, variance and the irreducible error representing a lower bound on the expected error for unseen sample data.

One way to reduce the variance is to try to get more data or to decrease the complexity of a model. One way to reduce the bias is to add more features or to make the model more complex, as adding more data will not help in this case. Finding the right balance between Bias and Variance is an art that every Data scientist must be able to manage.

![](6/images/00018.jpeg)

## 7. What is a cross-validation and what is an overfitting?

### Solution             

Learning a model on a set of examples and testing it on the same set is a logical mistake because the model would have no errors on the test set but it will almost certainly have a poor performance on the real application data. This problem is called overfitting and it is the reason why the gold set is typically split into independent sets for training, validation and test. An example of random split is reported in the code section, where a toy dataset with diabetics’ data has been randomly split into two parts: the training set and the test set.

Given a family of learned models, the validation set is used for estimating the best hyper-parameters. However, by adopting this strategy there is still the risk that the hyper-parameters overfit a particular validation set.

The solution to this problem is called cross-validation. The idea is simple: the test set is split in ![](6/images/00019.jpeg) smaller sets called folds and the model is then learned on ![](6/images/00020.jpeg) folds, while the remaining data is used for validation. This process is repeated in a loop and the metrics achieved for each iteration are averaged. An example of cross validation is reported in the section below where our toy dataset is classified via SVM and accuracy is computed via cross-validation. SVM is a classification technique and “accuracy” is a quality measurement (the number of correct predictions made, divided by the total number of predictions made and multiplied by 100 to turn it into a percentage).

[Stratified KFold](http://scikit-learn.org/stable/modules/generated/sklearn.cross_validation.StratifiedKFold.html#sklearn.cross_validation.StratifiedKFold) is a variation of k-fold where each set contains approximately the same balanced percentage of samples for each target class as the complete set.

### Code

import numpy as np

from sklearn import cross_validation

from sklearn import datasets

from sklearn import svm

diabets = datasets.load_diabetes()

X_train, X_test, y_train, y_test = \

cross_validation.train_test_split(

     diabets.data, diabets.target, test_size=0.2, random_state=0)

print X_train.shape, y_train.shape # test size 20%

print X_test.shape, y_test.shape    

clf = svm.SVC(kernel='linear', C=1)

scores = cross_validation.cross_val_score(

    clf, diabets.data, diabets.target, cv=4)  # 4-folds

print scores

print("Accuracy: %0.2f (+/- %0.2f)"  %  (scores.mean(), scores.std()))

## 8. Why are vectors and norms used in machine learning?

### Solution

Objects such as movies, songs and documents are typically represented by means of vectors of features. Those features are a synthetic summary of the most salient and discriminative objects characteristics.

Given a collection of vectors (the so-called vector space)![](6/images/00021.jpeg), a norm on ![](6/images/00022.jpeg) is a [function](https://en.wikipedia.org/wiki/Function_(mathematics)) ![](6/images/00023.jpeg)satisfying the following properties: For all complex numbers ![](6/images/00024.jpeg) and all![](6/images/00025.jpeg),

1.  ![](6/images/00026.jpeg)
2.  ![](6/images/00027.jpeg)
3.  ![](6/images/00028.jpeg) thenv is the zero vector

The intuitive notion of length for a vector is captured by the norm 2

![](6/images/00029.jpeg)

More generally we have the norm ![](6/images/00030.jpeg)

![](6/images/00031.jpeg)

The special case of infinity norm is  ![](6/images/00032.jpeg) is defined as

![](6/images/00033.jpeg)

### Code

from numpy import linalg as LA

import numpy as np

a = np.arange(22)

print LA.norm(a)

print LA.norm(a,  1)             

## 9. What are Numpy, Scipy and Spark essential datatypes?

### Solution

Numpy provides efficient support for memorizing vectors and matrices and for linear algebra operations[[5]](#part0000_split_066.html__ftn5). For instance: ![](6/images/00034.jpeg) is the dot product of two vectors, while ![](6/images/00035.jpeg)and ![](6/images/00036.jpeg) are respectively the inner and outer products.

Scipy provides support for sparse matrices and vectors with multiple memorization strategies in order to save space when dealing with zero entries.[[6]](#part0000_split_066.html__ftn6)  In particular the COOrdinate format specifies the non-zero ![](6/images/00037.jpeg)value for the coordinates![](6/images/00038.jpeg), while the Compressed Sparse Colum matrix (CSC) satisfies the relationship![](6/images/00039.jpeg)

Spark has many native datatypes for local and distributed computations. The primary data abstraction is a distributed collection of items called “Resilient Distributed Dataset (RDD)”. RDDs can be created from Hadoop InputFormats[[7]](#part0000_split_066.html__ftn7) or by transforming other RDDs. Numpy arrays, Python list and Scipy CSC sparse matrices are all supported. In addition: MLIB, the Spark library for machine learning, supports SparseVectors and [LabeledPoint](http://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LabeledPoint), i.e.  local vectors, either dense or sparse, associated with a label/response

### Code

import numpy as np

from scipy.sparse import csr_matrix

M = csr_matrix([[4,  1,  0],  [4,  0,  3],  [0,  0,  1]])

from pyspark.mllib.linalg import SparseVector

from pyspark.mllib.regression import LabeledPoint

label =  0.0

point = LabeledPoint(label, SparseVector(3,  [0,  2],  [1.0,  3.0]))

textRDD = sc.textFile("README.md")

print textRDD.count()  # count items in RDD

## 10.  Can you provide an example for Map and Reduce in Spark? (Let’s compute the Mean Square Error)

### Solution

Spark is a powerful paradigm for parallel computations which are mapped into multiple servers with no need of dealing with low level operations such as scheduling, data partitioning, communication and recovery. Those low level operations were typically exposed to the programmers by previous paradigms. Now Spark solves these problems on our behalf.

A simple form of parallel computation supported by Spark is the “Map and Reduce” which has been made popular by Google[[8]](#part0000_split_066.html__ftn8).

![](6/images/00040.jpeg)

In this framework a set of keywords is mapped into a number of workers (e.g. parallel servers available for computation) and the results are then reduced (e.g. collected) by applying a “reduce” operator. The reduce operator could be very simple (for instance a sum) or sophisticated (e.g. a user defined function).

As an example of distributed computation let’s compute the Mean Square Error (MSE), the average of the squares of the difference between the estimator and what is estimated. In the following example we suppose thatvaluesAndPreds is an RDD of many (![](6/images/00041.jpeg)  tuples. Those are mapped into values ![](6/images/00042.jpeg)  . All intermediate results computed by parallel workers are then reduced by applying a sum operator. The final result is then divided by the total number of tuples as defined by the mathematical definition![](6/images/00043.jpeg). Note that Spark hides all the low level details to the programmer by allowing to write a distributed code which is very close to a mathematical formulation. The code adopts python lambda computation for compact representations of anonymous functions.

### Code

MSE = valuesAndPreds.map(lambda  (v, p):  (v - p)**2).reduce(lambda x, y: x + y)  / valuesAndPreds.count()

Spark can however support additional forms of parallel computation by taking inspiration from the 20 years of work on skeletons computations and, more recently, on Microsoft’s Cosmos.[[9]](#part0000_split_066.html__ftn9)

## 11.  Can you provide examples for other computations in Spark?

### Solution

The first code fragment is an example of map reduction, where we want to find the line with most words in a text. First each line is mapped into the number of words it contains. Then those numbers are reduced and the maximum is taken. Pretty simple: one single line of code stays here for something which requires hundreds of lines in other parallel paradigms such as Hadoop.

Spark supports two types of operations: transformations, which create a new RDD dataset from an existing one, and actions, which return a value to the driver program after running a computation on the dataset. All transformations in Spark are lazy because the computation is postponed as much as possible until the results are really needed by the program. This allows Spark to run efficiently – for example the compiler can realize that an RDD created through map will be used in a reduce and return only the result of thereduce to the driver, rather than the larger mapped dataset. Intermediate results can be persisted and cached.

Basic transformations include (the list below is not comprehensive. Check online for a full list[[10]](#part0000_split_066.html__ftn10))

| Transformation | Use |
| map(func) | Returns a new distributed dataset formed by passing each element of the source through a function func. |
| filter(func) | Returns a new dataset formed by selecting those elements of the source on which func returns true. |
| flatMap(func) | Similar to map, but each input item can be mapped to 0 or more output items (so func should return a Seq rather than a single item). |
| sample(withReplacement, fraction, seed) | Samples a fraction of the data, with or without replacement, using a given random number generator seed. |
| union(otherDataset) | Returns a new dataset that contains the union of the elements in the source dataset and argument. |
| intersection(otherDataset) | Returnsa new RDD that contains the intersection of elements in the source dataset and argument. |
| distinct([numTasks])) | Returns a new dataset that contains the distinct elements of the source dataset. |
| groupByKey([numTasks]) | When called on a dataset of (K, V) pairs, a dataset of (K, Iterable<V>) pairs returns.  |
| reduceByKey(func, [numTasks]) | When called on a dataset of (K, V) pairs, a dataset of (K, V) pairs returns, where the values for each key are aggregated using the given reduce function func, which must be of type (V,V) => V |
| sortByKey([ascending], [numTasks]) | When called on a dataset of (K, V) pairs, where K implements Ordered, a dataset of (K, V) pairs sorted by keys in ascending or descending order returns, as specified in the boolean ascending argument. |
| join(otherDataset, [numTasks]) | When called on datasets of type (K, V) and (K, W), a dataset of (K, (V, W)) pairs with all pairs of elements for each key returns. Outer joins are here supported throughleftOuterJoin, rightOuterJoin, andfullOuterJoin. |

Basic actions include (the list below is not comprehensive. Check it online for a full list[[11]](#part0000_split_066.html__ftn11))

| Actions | Use |
| reduce(func) | Aggregates the elements of the dataset using a function func (which takes two arguments and returns one). The function should be commutative and associative so that it can be computed correctly in parallel. |
| collect() | Returns all the elements of the dataset as an array at the driver program. This is usually useful after a filter or other operations that return a sufficiently small subset of data. |
| count() | Returnsthe number of elements in the dataset. |
| take(n) | Returns an array with the first n elements of the dataset. |
| takeSample(withReplacement,num, [seed]) | Returns an array with a random sample of numelements of the  dataset, with or without replacement, optionally pre-specifying a random number generator seed. |
| countByKey() | Only available on RDDs of type (K, V). A hashmap of (K, Int) pairs with the count of each key returns. |
| foreach(func) | Runs a function func on each element of the dataset. This is usually done for side effects such as updating an Accumulator or interacting with external storage systems.  |

Spark supports also two special types of variables. Broadcasts, that  allow the programmer to keep a read-only variable cached on each machine, and Accumulators for efficient implementation of counters.

The second code fragment is another map reduction, where the text is transformed into a flatmap of words. Words are then mapped into number 1 because we count each occurrence as pairs (words, 1). Then a reduceByKey() operation allows to aggregate each word and sum the occurrences.  Again pretty simple: one single line in Spark using a functional programming style. The third code segment introduces accumulators and broadcast variables.

### Code

# map reduce

textFile.map(lambda line: len(line.split())).reduce(lambda a, b: a if  (a > b)  else b)

# word count

wordCounts = textFile.flatMap(lambda line: line.split()).map(lambda word:  (word,  1)).reduceByKey(lambda a, b: a+b)

# broadcast

broadcastVar = sc.broadcast([1,  2,  3])

# accumulators

accum = sc.accumulator(0)

sc.parallelize([1,  2,  3,  4]).foreach(lambda x: accum.add(x))

## 12.  How does Python interact with Spark

### Solution

Spark has a dedicate API for Python called PySpark exposing access to the Spark programming framework. Internally Spark has been developed using Scala, a functional programming language which integrates well with JVM, the java virtual machine. One important observation is that Python is dynamically typed, so RDDs can hold objects of multiple types. Another observation is that the PySpark APIs reflect the Scala APIs but the former typically take a Python function and return a Python collection. Also lambda functions are supported and used quite frequently.

Functions used for transformations are sent to the workers for code execution together with serialized data and instances of classes. Python also supports an interactive shell./bin/pysparkfor performing Data science at the command line.

It is important to point out that Spark compilers allocate the computation on the underlying network of servers with no explicit need of dealing with low level details for programmers, unless this is explicitly desired.

## 13.  What is Spark support for Machine Learning?

### Solution

Spark has a powerful library called MLIB for Machine learning. Mlib supports computation of Basic Statistics and Features extraction, selection and transformation. It also supports Classification and Regression with linear models, naïve Bayes, decision trees and ensembles. Plus, Mlib implements Collaborative Filtering, Clustering with k-means, Gaussian, LDA, Associative Rule mining and Dimensional Reduction. Many optimization problems are solved by using the Distributed Stochastic Gradient Descent. We will discuss all these techniques in this volume and in the next one.

## 14.  How does Spark work in a parallel environment

### Solution

Spark adopts a simple model for parallel computation. A driver program interacts with the worker nodes by using the SparkContext environment variable.  This interaction is transparent to the user. Each worker node executes assigned tasks and can cache locally the results for computation for future reuse. The results of computations are sent back to the driver program.

![Spark cluster components](6/images/00044.jpeg)

### Code

conf = SparkConf().setAppName(appName).setMaster(master)

sc = SparkContext(conf=conf)

## 15.  What is the mean, the variance, and the covariance?

### Solution

In arithmetic terms the mean, or mathematical expectation, is the central value of a discrete set of numbers![](6/images/00045.jpeg), which is the so-called random variable, the value of which is subjected to variations due to chance. The mean is defined as the sum of values divided by the number of ![](6/images/00046.jpeg) values:

![](6/images/00047.jpeg)

The variancemeasures how far a set of numbers is spread out. A variance of zero shows that all the values are equal; a small variance indicates that the data points tend to be very close to the mean and therefore to each other, while a high variance indicates that the data points are more spread out. Variance is always positive. Given a random variable ![](6/images/00048.jpeg) the variance is defined as

![](6/images/00049.jpeg)

The covariance is a measure of how much two random variables change together. Mathematically:

![](6/images/00050.jpeg)

### Code

import numpy as np

x = np.array([[0,  2],  [1,  1],  [2,  0]]).T

print np.mean(x[1,])

print np.var(x[1,])

print np.cov(x)

1.0

0.666666666667

[[ 1\. -1.]

[-1.  1.]]

## 16.  What are percentiles and quartiles?

### Solution

A percentile is a metric indicating a value, below which a given percentage of observations falls. For instance: the 50th percentile is the median of a vector of observations; the 25th percentile is the first quartile, the 50th percentile is the second and the 75th percentile is the third one. When the time to provide a service is considered, the 90th, the 95th and the 99th percentiles are generally reported. Percentiles are more resilient than mathematical averages to the contribution of the so-called outliers, e.g. data points that are significantly spread out by the majority of the observations.

### Code

import numpy as np

x = np.array([0,  1,  4,  5,  6,  8,  8,  9,  11,  10,  19,  19.2,  19.7,  3])

for i in  [75,  90,  95,  99]: 

 print i, np.percentile(x, i)

## 17.  Can you transform an XML file into Python Pandas?

### Solution

This is a question about data transformation. XML is commonly used for representing structured information. For instance this could be an XML fragment for representing books data:

<?xml  version="1.0"?>

<catalog>

 <book  id="bk101">

 <author>Gambardella, Matthew</author>

 <title>XML Developer's Guide</title>

 <genre>Computer</genre>

 <price>44.95</price>

 <publish_date>2000-10-01</publish_date>

 <description>An in-depth look at creating applications

      with XML.</description>

 </book>

...

</catalog>

Pandas are a powerful set of Python libraries for data analysis. One key data structure in Pandas is the DataFrame, which is a Two-dimensional size-mutable, potentially heterogeneous tabular data structure with labeled axes (rows and columns). Each row is called a Series.

Pandas offer a rich set of APIs for manipulating DataFrames. In this code example an XML file is read using the convenient objectify module and a Pandas data structure is then created accordingly.

### Code

from lxml import objectify

import pandas as pd

# open and parse xml

xml = objectify.parse(open('book.xml'))

root = xml.getroot()

# pandas and dataframes

df = pd.DataFrame(columns=('Author',  'Title',  'Genre'))

for i in range(0,  10):

row = dict(zip(['Author',  'Title',  'Genre'],

 [root.book[i].author, root.book[i].title,

    root.book[i].genre

 ]))

rowSeries = pd.Series(row)

    rowSeries.name = i

df = df.append(rowSeries)

print df

                       Author                                        Title  \

0  [[[Gambardella, Matthew]]]                  [[[XML Developer's Guide]]]

1            [[[Ralls, Kim]]]                          [[[Midnight Rain]]]

2           [[[Corets, Eva]]]                        [[[Maeve Ascendant]]]

3           [[[Corets, Eva]]]                        [[[Oberon's Legacy]]]

4           [[[Corets, Eva]]]                     [[[The Sundered Grail]]]

5      [[[Randall, Cynthia]]]                            [[[Lover Birds]]]

6        [[[Thurman, Paula]]]                          [[[Splish Splash]]]

7         [[[Knorr, Stefan]]]                        [[[Creepy Crawlies]]]

8          [[[Kress, Peter]]]                           [[[Paradox Lost]]]

9          [[[O'Brien, Tim]]]  [[[Microsoft .NET: The Programming Bible]]]

                   Genre

0         [[[Computer]]]

1          [[[Fantasy]]]

2          [[[Fantasy]]]

3          [[[Fantasy]]]

4          [[[Fantasy]]]

5          [[[Romance]]]

6          [[[Romance]]]

7           [[[Horror]]]

8  [[[Science Fiction]]]

9         [[[Computer]]]

## 18.  Can you read HTML into Python Pandas?

### Solution

Another question about accessing data. Python Pandas are also convenient for working with HMTL files downloaded from the network. This small code fragment is all we need to download some HTML data, parse it and load it into a suitable DataFrame.

### Code

import pandas as pd

url =  'http://www.fdic.gov/bank/individual/failed/banklist.html'

dfs = pd.read_html(url)

print dfs

[                                             Bank Name             City  ST  \

0                                         Premier Bank           Denver  CO

1                                       Edgebrook Bank          Chicago  IL

2                                 Doral BankEn Espanol         San Juan  PR

3                    Capitol City Bank & Trust Company          Atlanta  GA

4                              Highland Community Bank          Chicago  IL

5                     First National Bank of Crestview        Crestview  FL

## 19.  Can you read JSON into Python Pandas?

### Solution

Json is a compact representation of structured data. This simple code snippet loads data from the network and transforms it into Pandas data structure.

### Code

from urllib2 import Request, urlopen

import json

import pandas as pd

from pandas.io.json import json_normalize

path1 =  '42.974049,-81.205203|42.974298,-81.195755'

request=Request('http://maps.googleapis.com/maps/api/elevation/json?locations='+path1+'&sensor=false')

response = urlopen(request)

elevations = response.read()

data = pd.read_json(elevations)

print json_normalize(data['results'])

elevation  location.lat  location.lng  resolution

0  243.346268     42.974049    -81.205203   19.087904

## 20.  Can you draw a function from Python?

### Solution

Visualizing data is key for any machine learning activity and a good Data Scientist knows how to use data visualization tools. For instance Matplotlib is a convenient plotting tool in Python. The following code snippet shows how to plot a function.

### Code

import matplotlib.pyplot as plt

import numpy as np

from scipy.special import expit

x = np.arange(-10.,  10.,  0.2)

sig = expit(x)

plt.plot(x,sig)

plt.show()

![](6/images/00051.jpeg)

## 21.  Can you represent a graph in Python?

### Solution

Python provides a convenient library for graph representation named Networkx[[12]](#part0000_split_066.html__ftn12) , which provides support for direct / indirect graphs and multigraphs. Also many graph algorithms are already implemented in the framework. This simple code snippet computes the connected components algorithm.

### Code

import networkx as nx

G=nx.Graph()

#add nodes (1,2,3) and edges(1,2), (1,3)

G.add_edges_from([(1,2),(1,3)])

c = nx.connected_components(G)

## 22.  What is an Ipython notebook?

### Solution

Ipython notebook is a convenient interface for executing Python codes directly from a web browser. The following command starts the environment and the browser:

ipython notebook

[I 21:17:06.706 NotebookApp] Using MathJax from CDN: https://cdn.mathjax.org/mathjax/latest/MathJax.js

[I 21:17:07.252 NotebookApp] Serving notebooks from local directory: C:\Users\agull_000\Dropbox\python

[I 21:17:07.252 NotebookApp] 0 active kernels

[I 21:17:07.252 NotebookApp] The IPython Notebook is running at: http://localhost:8888/

[I 21:17:07.252 NotebookApp] Use Control-C to stop this server and shut down all kernels (twice to skip confirmation).

[I 21:17:21.631 NotebookApp] Creating new notebook in

[I 21:17:30.592 NotebookApp] Kernel started: 50260c3a-e7cc-426f-84fa-9ea630886103

### Code

This code fragment prints few circles and it is executed directly from the browser.

![](6/images/00052.jpeg)

![](6/images/00053.jpeg)

## 23.  What is a convenient tool for performing data statistics?

### Solution

Pandas provide a nice framework for data-analysis. In this code example an iris toy dataset is loaded and then the mean, the standard deviation and different percentiles are computed.

### Code

import pandas as pd

import numpy as np

from sklearn.datasets import load_iris

iris = load_iris()

irisNP = iris.data

irisDF = pd.DataFrame(iris.data, columns=iris.feature_names)

# group by target category

irisDF['group']  = pd.Series([iris.target_names[k]  for k in iris.target], dtype='category')

#mean, std, quantile

print irisDF.mean(numeric_only=True)

print irisDF.std()

print irisDF.quantile(np.array([0,  .25,  0.50,  .75,  .90,  .99]))

sepal length (cm)    5.843333

sepal width (cm)     3.054000

petal length (cm)    3.758667

petal width (cm)     1.198667

sepal length (cm)    0.828066

sepal width (cm)     0.433594

petal length (cm)    1.764420

petal width (cm)     0.763161

      sepal length (cm)  sepal width (cm)  petal length (cm)  petal width (cm)

0.00                4.3             2.000               1.00               0.1

0.25                5.1             2.800               1.60               0.3

0.50                5.8             3.000               4.35               1.3

0.75                6.4             3.300               5.10               1.8

0.90                6.9             3.610               5.80               2.2

0.99                7.7             4.151               6.70               2.5

## 24.  How is it convenient to visualize data statistics

### Solution

Pandas provide support for a boxplot visualization, a convenient way of graphically representing groups of numerical values through their quartiles. Boxplots may also have vertically extending lines from the boxes indicating variability outside the upper and lower quartiles. Outliers may be plotted as individual points. In this example of code we have represented a set of trials of 10 observations of a uniform random variable on ![](6/images/00054.jpeg)

### Code

import pandas as pd

import numpy as np

import matplotlib

import matplotlib.pyplot as plt

df = pd.DataFrame(np.random.rand(10,  5), columns=['A',  'B',  'C',  'D',  'E'])

df.plot(kind='box')

plt.show()

![](6/images/00055.jpeg)

## 25.  How to compute covariance and correlation matrices with pandas

### Solution

Pandas provides support for covariance computation. This simple code snippet computes covariance and correlation for an iris toy dataset. Remember that correlation is equivalent to computing covariance on standardized random variables. For instance it can be observed that sepal length is positively correlated with petal length.

### Code

import pandas as pd

import numpy as np

from sklearn.datasets import load_iris

iris = load_iris()

irisNP = iris.data

irisDF = pd.DataFrame(iris.data, columns=iris.feature_names)

# group by target category

irisDF['group']  = pd.Series([iris.target_names[k]  for k in iris.target], dtype='category')

print irisDF.cov()

print irisDF.corr()

                   sepal length (cm)  sepal width (cm)  petal length (cm)  \

sepal length (cm)           0.685694         -0.039268           1.273682

sepal width (cm)           -0.039268          0.188004          -0.321713

petal length (cm)           1.273682         -0.321713           3.113179

petal width (cm)            0.516904         -0.117981           1.296387

                   petal width (cm)

sepal length (cm)          0.516904

sepal width (cm)          -0.117981

petal length (cm)          1.296387

petal width (cm)           0.582414

                   sepal length (cm)  sepal width (cm)  petal length (cm)  \

sepal length (cm)           1.000000         -0.109369           0.871754

sepal width (cm)           -0.109369          1.000000          -0.420516

petal length (cm)           0.871754         -0.420516           1.000000

petal width (cm)            0.817954         -0.356544           0.962757

                   petal width (cm)

sepal length (cm)          0.817954

sepal width (cm)          -0.356544

petal length (cm)          0.962757

petal width (cm)           1.000000

## 26.  Can you provide an example of connection to the Twitter API?

### Solution

Twitter provides a convenient API for accessing data. The first step is to register within the site at [https://apps.twitter.com/app/new](https://apps.twitter.com/app/new) and require a Consumer Key, a Consumer Secret, an Access Key and an Access Secret. Then this code fragment can be used for accessing the live stream of twitter trends.

### Code

import tweepy, json

CONSUMER_KEY =  'mX------------------------------------'

CONSUMER_SECRET =  '------------------------------------------------------------------------'

ACCESS_KEY =  '-----------------------------------------------------------------------'

ACCESS_SECRET =  '---------------------------------------------------------'

auth = tweepy.OAuthHandler(CONSUMER_KEY, CONSUMER_SECRET)

auth.set_access_token(ACCESS_KEY, ACCESS_SECRET)

api = tweepy.API(auth)

trends1 = api.trends_place(1)

print trends1

[{u'created_at': u'2015-09-08T09:33:39Z', u'trends': [{u'url': u'http://twitter.com/search?q=%23Vatan%C4%B1mU%C4%9Fruna', u'query':

u'%23Vatan%C4%B1mU%C4%9Fruna', u'name': u'#Vatan\u0131mU\u011fruna', u'promoted_content': None}, {u'url': u'http://twitter.com/searc

h?q=%23I%C4%9Fd%C4%B1r', u'query': u'%23I%C4%9Fd%C4%B1r', u'name': u'#I\u011fd\u0131r', u'promoted_content': None}, {u'url': u'http:

//twitter.com/search?q=%23%D9%85%D8%A7%D8%B0%D8%A7_%D8%A7%D8%B3%D8%AA%D9%81%D8%AF%D9%86%D8%A7_%D9%85%D9%86_%D8%B3%D9%86%D8%A7%D8%A8_

%D8%B4%D8%A7%D8%AA', u'query': u'%23%D9%85%D8%A7%D8%B0%D8%A7_%D8%A7%D8%B3%D8%AA%D9%81%D8%AF%D9%86%D8%A7_%D9%85%D9%86_%D8%B3%D9%86%D8

%A7%D8%A8_%D8%B4%D8%A7%D8%AA', u'name': u'#\u0645\u0627\u0630\u0627_\u0627\u0633\u062a\u0641\u062f\u0646\u0627_\u0645\u0646_\u0633\u

0646\u0627\u0628_\u0634\u0627\u062a', u'promoted_content': None}, {u'url': u'http://twitter.com/search?q=%EB%92%B7%EB%8B%B4%ED%99%94

', u'query': u'%EB%92%B7%EB%8B%B4%ED%99%94', u'name': u'\ub4b7\ub2f4\ud654', u'promoted_content': None}, {u'url': u'http://twitter.c

om/search?q=%23FelizMartes', u'query': u'%23FelizMartes', u'name': u'#FelizMartes', u'promoted_content': None}, {u'url': u'http://tw

itter.com/search?q=%23%D8%AA%D8%A7%D9%88%D8%B1_%D8%AC%D8%AF%D9%8A%D8%AF_%D8%A8%D8%A7%D9%84%D8%B3%D8%B9%D9%88%D8%AF%D9%8A%D9%87', u'q

uery': u'%23%D8%AA%D8%A7%D9%88%D8%B1_%D8%AC%D8%AF%D9%8A%D8%AF_%D8%A8%D8%A7%D9%84%D8%B3%D8%B9%D9%88%D8%AF%D9%8A%D9%87', u'name': u'#\

u062a\u0627\u0648\u0631_\u062c\u062f\u064a\u062f_\u0628\u0627\u0644\u0633\u0639\u0648\u062f\u064a\u0647', u'promoted_content': None}

, {u'url': u'http://twitter.com/search?q=%22Sam+Smith%22', u'query': u'%22Sam+Smith%22', u'name': u'Sam Smith', u'promoted_content':

None}, {u'url': u'http://twitter.com/search?q=%22Felices+140%22', u'query': u'%22Felices+140%22', u'name': u'Felices 140', u'promot

ed_content': None}, {u'url': u'http://twitter.com/search?q=%22%EC%B2%9C%EC%82%AC%EC%99%80+%EC%95%85%EB%A7%88%22', u'query': u'%22%EC

%B2%9C%EC%82%AC%EC%99%80+%EC%95%85%EB%A7%88%22', u'name': u'\ucc9c\uc0ac\uc640 \uc545\ub9c8', u'promoted_content': None}, {u'url': u

'http://twitter.com/search?q=%22Alexander+Pacteau%22', u'query': u'%22Alexander+Pacteau%22', u'name': u'Alexander Pacteau', u'promot

ed_content': None}], u'as_of': u'2015-09-08T09:37:06Z', u'locations': [{u'woeid': 1, u'name': u'Worldwide'}]}]

## 27.  Can you provide an example of connection to the LinkedIn API?

### Solution

Linkedin has an API for accessing the content. First, the application should be registered within the site on [https://www.linkedin.com/developer/apps/](https://www.linkedin.com/developer/apps/) for getting the API_KEY and the API_SECRET. It is also important to register the correct RETURN_URL. The authentication.authorization_url should be then opened in a browser for letting the user logging in via OAUTH standard protocol[[13]](#part0000_split_066.html__ftn13). The returned code can be used as authentication.authorization_code for getting access.

### Code

from linkedin import linkedin

API_KEY =  '-------'

API_SECRET =  '---'

RETURN_URL =  'http://localhost:8000'

authentication = linkedin.LinkedInAuthentication(API_KEY, API_SECRET, RETURN_URL, linkedin.PERMISSIONS.enums.values())

print authentication.authorization_url # open this url on your browser

application = linkedin.LinkedInApplication(authentication)

authentication.authorization_code = ‘-----------------------------------'

authentication.get_access_token()

connections = application.get_connections()

print connections

## 28.  Can you provide an example of connection to the Facebook API?

### Solution

Facebook has a nice API accessible on [https://developers.facebook.com/docs/graph-api/overview](https://developers.facebook.com/docs/graph-api/overview) and the following code fragment provides basic usage for getting friends’ connections with the user’s profile and for posting them on the Facebook wall.

### Code

import facebook

# how to get the access token https://developers.facebook.com/docs/graph-api/overview

graph = facebook.GraphAPI(oauth_access_token)

profile = graph.get_object("me")

friends = graph.get_connections("me",  "friends")

graph.put_object("me",  "feed", message="Posting in my wall")

## 29.  What is a TFxIDF?

### Solution

TFxIDF is a weighting technique frequently used for text classifications. The key intuition is to boost a term ![](6/images/00056.jpeg) which is frequent for a document d![](6/images/00057.jpeg) in a collection of documents ![](6/images/00058.jpeg)(Term Frequency=TF) but ![](6/images/00056.jpeg) is not so frequent in all the remaining documents in ![](6/images/00058.jpeg) (Inverse Document Frequency, IDF). Mathematically

*   ![](6/images/00059.jpeg) is the number of times for term t to appear in document![](6/images/00060.jpeg) 
*   ![](6/images/00061.jpeg)   is the number of documents containing term ![](6/images/00056.jpeg) 
*   ![](6/images/00062.jpeg)

Note that ![](6/images/00063.jpeg) is zero, if a term appears in all the documents. Also note that a smoothing factor of one has been used if a term does not appear in a document for avoiding a division by zero. Spark implements TFxIDF by hashing the words into a more compact representation which avoids global and expensive terms-to-index mapping, involving all the words in the collection regardless of the server where the data has been partitioned.

### Code

from pyspark import SparkContext

from pyspark.mllib.feature import HashingTF

from pyspark.mllib.feature import IDF

sc = SparkContext()

# Load documents (one per line).

documents = sc.textFile("...").map(lambda line: line.split(" "))

#hash the terms and compute the TF on documents

hashingTF = HashingTF()

tf = hashingTF.transform(documents)

# force the real computation

tf.cache()

# compute the global IDF: ignore too rare terms < 2 documents

idf = IDF(minDocFreq=2).fit(tf)

# do the TFxIDF in a distributed fashion

tfidf = idf.transform(tf)

## 30.  What is “features hashing”? And why is it useful for BigData?

### Solution

If the space of features is high dimensional, one way to reduce dimensionality is via hashing. For instance: we might combine two discrete but sparse features into one and only denser discrete synthetically created feature by transforming the original observations. This transformation introduces an error because it suffers from potential hash collisions, since different raw features may become the same term after hashing.

However this model might be more compact and, in some situations, we might decide to trade off this risk either for simplicity or because this is the only viable option to handle very large datasets (Big Data).

More sophisticate forms of hashing such as Bloom Filters[[14]](#part0000_split_066.html__ftn14), Count Min-Sketches[[15]](#part0000_split_066.html__ftn15), minHash[[16]](#part0000_split_066.html__ftn16)  and Local Sensitive Hashing[[17]](#part0000_split_066.html__ftn17) are more advanced techniques which will be discussed in the next volume.

## 31.  What is “continuous features binning”?

### Solution

If a feature assumes continuous values then it could be convenient to discretize it via hashing or binning. This intuition is very simple: the space of continuous values is divided into buckets, in which the first ones are hashed.

## 32.  What is an ![](6/images/00064.jpeg)normalization?

### Solution

Features might be transformed in such a way that they have unit norm![](6/images/00065.jpeg), where ![](6/images/00064.jpeg)can be either norm-1, or norm-2, or norm-![](6/images/00066.jpeg)

### Code

from pyspark.mllib.util import MLUtils

from pyspark.mllib.linalg import Vectors

from pyspark.mllib.feature import Normalizer

data = MLUtils.loadLibSVMFile(sc,  "data/mllib/sample_libsvm_data.txt")

labels = data.map(lambda x: x.label)

features = data.map(lambda x: x.features)

normalizer1 = Normalizer()

# scale every feature normalizing with norm-2

data1 = labels.zip(normalizer1.transform(features))

## 33.  What is a Chi Square Selection?

### Solution

Chi-Square is a statistical test used to understand if two categorical features are correlated. In this case it might be useful to discard one of them in order to keep the model simpler.  This method works by ordering features based on a Chi-Squared test of independence from the class, and then by filtering all top features, which are most closely related to the label.Suppose that an event has expected frequencies of observations ![](6/images/00067.jpeg) and observed frequencies ![](6/images/00068.jpeg) , then the Chi Square test is

![](6/images/00069.jpeg)

Spark supports Chi-Square tests for feature selection since version 1.4.0

## 34.  What is mutual information and how can it be used for features selection?

### Solution

Recalling that information entropy is![](6/images/00070.jpeg), where ![](6/images/00071.jpeg)is a random variable, mutual information computes how much two features have in common. This is defined as

![](6/images/00072.jpeg)

The normalized mutual information is in interval ![](6/images/00073.jpeg) defined as

![](6/images/00074.jpeg)

Computing mutual information in Spark is left as an exercise.

## 35.  What is a loss function, what are linear models, and what do we mean by regularization parameters in machine learning?

### Solution             

A loss function maps a set of observed events represented by one or more variables onto a real number, which represents the associated “cost”. Machine learning frequently deals with modelling the observed data by minimizing the costs of a suitable loss function. In particular given an algorithmic prediction ![](6/images/00030.jpeg) and a true label![](6/images/00075.jpeg) from a gold set, a loss function![](6/images/00076.jpeg)measures the difference between ![](6/images/00030.jpeg) and![](6/images/00075.jpeg). 

An important class of machine learning methods is the one of linear methods, where the task is to minimize a convex function ![](6/images/00015.jpeg) on a variable vector ![](6/images/00009.jpeg) with ![](6/images/00019.jpeg) real entries (![](6/images/00077.jpeg).

It should be noticed that if function ![](6/images/00015.jpeg) is convex and has a derivative, then ![](6/images/00015.jpeg) will have a unique minimum and this minimum can be analytically derived[[18]](#part0000_split_066.html__ftn18).

This minimization task error can be formally expressed as ![](6/images/00078.jpeg) where the objective function ![](6/images/00015.jpeg) has the following form:

![](6/images/00079.jpeg)

where ![](6/images/00080.jpeg) are the training examples, ![](6/images/00075.jpeg) is the vector of true labels and ![](6/images/00081.jpeg) is a set of weights which are algorithmically computed in such a way that the error of the model learned from the training data ![](6/images/00082.jpeg) is minimized. This error is expressed by a well-chosen loss function![](6/images/00083.jpeg) (see next question for few examples).

This method is called “linear” because prediction ![](6/images/00084.jpeg)is a linear combination of w and x, computed with a simple vector multiplication ![](6/images/00085.jpeg), and ![](6/images/00086.jpeg) is a function of ![](6/images/00030.jpeg) and ![](6/images/00087.jpeg).

The factor ![](6/images/00088.jpeg) is introduced also to control the complexity of this model. In turn the regularization hyper-parameter ![](6/images/00089.jpeg) balances the trade-off between the goal of minimizing the loss function and the goal of minimizing the model complexity. For instance, it could be sometimes better to have a slightly more expensive model in terms of loss function costs, if the model is simpler from the point of view of sparsity of weights (number of zero entries in![](6/images/00090.jpeg)).

The two tables below contain a summary of the most common used loss functions and regularization factors for linear methods:

| Name | Loss Function | Derivative | Labels | Meaning/ Usage | Example |
| Squared | ![](6/images/00091.jpeg) | ![](6/images/00092.jpeg) | Real,![](6/images/00093.jpeg) | It expresses the squared distance between the prediction and the true label | Linear regression,for example expected return on stock investment |
| Logistic | ![](6/images/00094.jpeg)![](6/images/00095.jpeg) | ![](6/images/00096.jpeg) | Positive / Negative,![](6/images/00097.jpeg) | It is used to predict a binary response | Logistic regression,for example expected click on search ads |
| Hinge | max![](6/images/00098.jpeg) | ![](6/images/00099.jpeg) | Positive / Negative,![](6/images/00097.jpeg) | It is used for classification | SVM,for example image recognition |

This is a typical plot for squared, logistic and hinge loss functions

![](6/images/00100.jpeg)

This is a summary of the most commonly used regularization factors.

| Name | R(W) | Derivative | Meaning |
| L1 | ![](6/images/00101.jpeg) | ![](6/images/00102.jpeg) | norm-1 for vectors |
| L2 | ![](6/images/00103.jpeg) | ![](6/images/00009.jpeg) | squared norm-2 for vectors |

## 36.  What is an odd ratio?

Solution

Given a probability ![](6/images/00030.jpeg) the odd ratio simply identifies the chances for the event to happen over the chances for the event not to happen. The event ![](6/images/00104.jpeg) is a function![](6/images/00105.jpeg). If we take the logarithm, we have ![](6/images/00106.jpeg) and we can thus map the range of probabilities [0, 1] into the full range![](6/images/00107.jpeg).

The concept of “odd ratio” is also useful to introduce “logistic regression” (the topic of the next question). Let us assume that we have a linear equation ![](6/images/00108.jpeg) , we can imagine that ![](6/images/00109.jpeg) is represented in terms of log odds so that ![](6/images/00110.jpeg)which can be solved for ![](6/images/00111.jpeg) as ![](6/images/00112.jpeg) and the problem becomes the one of finding the lowest error for all training examples ![](6/images/00113.jpeg)

## 37.  What is a sigmoid function and what is a logistic function?

A sigmoid function has the following mathematical formulation ![](6/images/00114.jpeg)

![](6/images/00115.jpeg)  

Sigmoid functions are used frequently in machine learning in particular in neural networks. Their name is related to the typical "S" shape when plotted. Note that for input in![](6/images/00116.jpeg),![](6/images/00117.jpeg) the output is in [0, 1], so the sigmoid is useful to map real values into probabilities.

![https://upload.wikimedia.org/wikipedia/commons/thumb/8/88/Logistic-curve.svg/320px-Logistic-curve.svg.png](6/images/00118.jpeg)

One important property is that the first order derivative of a sigmoid has a very simple formula![](6/images/00119.jpeg)

![](6/images/00120.jpeg)

![](6/images/00121.jpeg)

A logistic function is a particular type of sigmoid function used in linear regression![](6/images/00122.jpeg) , where ![](6/images/00013.jpeg) is the maximum value,  ![](6/images/00123.jpeg)  is the steepness of the curve and  ![](6/images/00124.jpeg)  is the x-value of the sigmoid midpoint.

### Code

from scipy.special import expit

expit(0.467)

Note that in a previous question we already plotted a sigmoid.

## 38.  What is a gradient descent?

### Solution

Mathematically the gradient![](6/images/00125.jpeg) of a function ![](6/images/00015.jpeg) is a vector, the components of which are the![](6/images/00046.jpeg) partial derivatives of![](6/images/00126.jpeg). Similarly to the derivative, the gradient represents the slope of the function graph tangent and therefore the gradient points in the direction of the greatest rate of the function increase rate, while its magnitude is the slope of the graph in that direction. As a consequence ![](6/images/00127.jpeg) points to the direction of a function maximum decrease rate.

In many Supervised Machine Learning problems, we need to learn a model by using a training dataset. A popular and easy-to-use technique to estimate the model parameters is to minimize the error associated to the model by using the appropriate Gradient Descent technique. The Gradient Descent iteratively estimates the weights by moving in the direction which minimizes a chosen cost function at every step.

![](6/images/00128.jpeg)

The pseudo-code is here very simple. Until either some convergence or termination criteria is met, the weights of the model are updated according the following rule

![](6/images/00129.jpeg)

where ![](6/images/00130.jpeg) is the gradient in ![](6/images/00009.jpeg) and ![](6/images/00123.jpeg) is a learning rate parameter.

If the function is convex, then the gradient descend will find a unique minimum, otherwise the technique can be trapped into a local minimum or it might incur into the risk of not converging. Therefore, it is mandatory to stop iterations if a chosen maximum number of iteration is reached. In addition to that, it could be useful to repeat the process for different initial values ![](6/images/00131.jpeg) in order to detect if the process is trapped in a local minimum.

The learning rate parameter ![](6/images/00123.jpeg) determines how fast or slow we will move towards the optimal solution. If λ is very large, the optimal solution will be skipped. If it is too small, we will need many iterations to converge to the best values. One possible solution is to scale ![](6/images/00123.jpeg) according to how close the solution is. In other words: λ could be scaled according to the error rate measured in each iteration.

## 39.  What is a stochastic gradient descent?

### Solution

Many machine learning problems can be formulated as minimization problems of an objective function, which is the sum of many functions![](6/images/00132.jpeg) , each one associated to the ![](6/images/00133.jpeg)-th observation in the training set:

![](6/images/00134.jpeg)where ![](6/images/00135.jpeg)

The gradient ![](6/images/00136.jpeg) can be computationally very expensive because at each iteration all dataset observations should be taken into account and the standard update rule would be

![](6/images/00137.jpeg)

One solution is  to sample a subset of summand functions at every step. This approach is called “stochastic gradient descent” and it is very effective in the case of large-scale machine learning problems. One simple variant of stochastic gradient descent is to consider one training example at time and update only that gradient component. Another more sophisticated approach is called “mini-batches” which computes the gradient against more than one training example at each step. This can be a vectorial operation which is very efficient for modern computers.

### Code

In Spark the sampling of training examples is performed using RDD distributed datasets, while the computation of the partial results sum is performed by using local working machines which then update a master server.[[19]](#part0000_split_066.html__ftn19) The following is an abstract from Spark API

![](6/images/00138.jpeg)

## 40.  What is a Linear Least Square Regression?

### Solution

Linear models are simple and provide data partition based on straight lines. In general, they require a reasonably small amount of training data. More complex models, such as SVM with kernels and ensembles (which will be introduced in the next volume), allow data separation with more sophisticate curves - not only with straight lines -  but they are in general more expensive to train, require more data, and are also more expensive when they predict results on unseen data.

In many real applications linear models with regularizations are instead providing good performances and are extremely fast for training or when deployed. Also linear models show a very nice characteristic for they allow to easily understand the importance of each feature. This is called “variable importance information” and it consists in ranking each selected feature: a highly ranked feature contributes more to reduce the error for a model than a low ranked feature. So this ranking operation can guide Data scientists to pick the right set of features by discarding some of them and by adding others. Note that a linear model with regularization provides sparse solutions for learning.

When new unseen data is applied the forecast can therefore be computed with very simple operations consisting in few sums and few multiplications.

As discussed, Regression is the task of forecasting a numeric value. Linear Regression is a method of finding ![](6/images/00078.jpeg) where the objective function is a loss function

![](6/images/00139.jpeg)

![](6/images/00140.jpeg) and ![](6/images/00088.jpeg) is the regularizer factor.

The minimum can be here identified by using the stochastic gradient descend or with other more advanced methodologies which are outside the scope of this introductory book.

The code below is an example of Spark for Linear Regression. This image represents an example of linear regression and related regression line.

![](6/images/00141.jpeg)

### Code

from pyspark.mllib.regression import LabeledPoint, LinearRegressionWithSGD

from numpy import array

# parse the point into a LabeledPoint

#  made up of (label, set of features)

def  parsePoint(line):

values =  [float(x)  for x in line.replace(',',  ' ').split(' ')]

 return LabeledPoint(values[0], values[1:])

# load the data into a resilient distributed data (RDD)

data = sc.textFile("data/mllib/ridge-data/lpsa.data")

#trasform the RDD into an RDD of LabeledPoint

parsedData = data.map(parsePoint)

# Build the model by training a linear regression on the parsedData

model = LinearRegressionWithSGD.train(parsedData)

# Evaluate the model on training data

# We are creating an RDD of pairs (label, prediction) via a lambda call

valuesAndPreds = parsedData.map(lambda p:  (p.label, model.predict(p.features)))

# compute the MSE by mapping the label and prediction into the squared diff

# then reduce the distributed differences by summing them

# spark collects all the intermediate results via reduction

# this value is then divided by the total number of (label, prediction) tuples 

MSE = valuesAndPreds.map(lambda  (v, p):  (v - p)**2).reduce(lambda x, y: x + y)  / valuesAndPreds.count()

print("Mean Squared Error = "  + str(MSE))

## 41.  What are Lasso, Ridge, and ElasticNet regularizations?

### Solution

Linear least squares method uses no regularization. Ridge regression uses L2 regularizations and Lasso uses L1 regularization. Both Lasso and Ridge produce coefficients for the learned model that are smaller than the version of regression with no regularization. However, Lasso tends to produce more zero coefficients, thus increasing the model sparsity and its compactness. Sometimes Ridge and Lasso are used together and those are the so-called ElasticNet models.

## 42.  What is a Logistic Regression?

### Solution

A “Logistic Regression” is the problem of finding ![](6/images/00078.jpeg) , where the objective function is a loss function

![](6/images/00142.jpeg)

Each prediction is made by using a logistic function ![](6/images/00143.jpeg) , where ![](6/images/00144.jpeg) for each new unseen observation![](6/images/00145.jpeg). [Logistic regression](http://en.wikipedia.org/wiki/Logistic_regression)s are widely used to predict binary responses.  If ![](6/images/00146.jpeg) , then the outcome is positive, otherwise the outcome is negative.

A variant of logistic regression is the multinomial one which can predict ![](6/images/00147.jpeg) different outcomes, where one class is used as pivot and all the other ones are chosen in turn against the pivot. In other words, ![](6/images/00148.jpeg) models are run and the one with higher probability is picked as prediction.

Stochastic or mini-batch Gradient descents can be used for solving logistic regression problems.

The following spark code is very similar to the one presented for linear regression and indeed the only difference here is the class used to learn models.

### Code

from pyspark.mllib.regression import LabeledPoint, LogisticRegressionWithLBFGS

from numpy import array

# parse the point into a LabeledPoint

#  made up of (label, set of features)

def  parsePoint(line):

values =  [float(x)  for x in line.replace(',',  ' ').split(' ')]

 return LabeledPoint(values[0], values[1:])

# load the data into a resilient distributed data (RDD)

data = sc.textFile("data/mllib/ridge-data/lpsa.data")

#trasform the RDD into an RDD of LabeledPoint

parsedData = data.map(parsePoint)

# Build the model by training a linear regression on the parsedData

model = LogisticRegressionWithLBFGS.train(parsedData)

# Evaluate the model on training data

# We are creating an RDD of pairs (label, prediction) via a lambda call

valuesAndPreds = parsedData.map(lambda p:  (p.label, model.predict(p.features)))

# compute the MSE by reducing the squared difference between label and prediction

# then we reduce the distributed differences by summing them

# spark collects all the intermediate results via reduction

# this value is then divided by the total number of (label, prediction) tuples 

MSE = valuesAndPreds.map(lambda  (v, p):  (v - p)**2).reduce(lambda x, y: x + y)  / valuesAndPreds.count()

print("Mean Squared Error = "  + str(MSE))

## 43.  What is a stepwise regression?

### Solution

In a stepwise selection the choice of predictive variables is automatically carried out by exploring the space of features. Stepwise regression can reduce the risk of overfitting and can help to find a simple model with good performances but it can be very expensive. This is particularly true if the feature space is explored brute-force with no additional hints on how to pick the right set of features. There are three variants of stepwise regression:

*   Forward selection, which starts with no features in the model, tests the addition of each feature using some error estimation and adds the variable only if it improves the model. The selection is repeated until no feature improves the model
*   Backward elimination, which starts with all candidate features, tests the deletion of each feature using some error estimation and then deletes the variable that improves the model the most after being deleted. This elimination is repeated until no feature deletion improves the model
*   Bidirectional elimination, which combines the previous two steps together.

## 44.  How to include nonlinear information into linear models

### Solution

Linear methods are created to make forecasts as a linear combination of features. However, if the data is inherently not linearly separable, then it is still possible to use linear models in a few situations. The key idea is to approximate nonlinearities in the problem as features polynomials. This is the so called basis expansion. As an example, if you believe that one feature can have quadratic impact on the forecast, then you can add the square of the feature to the feature space.  Picking the right basis expansion for the right set of features is an art which requires a lot of fine-tuning and experience. We will see another example of this technique when we will discuss about the SVM trick.

![](6/images/00149.jpeg)

## 45.  What is a Naïve Bayes classifier?

### Solution

A naïve Bayes classifier is a machine learning methodology which assigns class labels to each instance of real application data. The naïve attribute is related to the assumption that each feature provides a probabilistic contribution to the learned model, which is independent from the other features.

For instance a text article can be assigned to the category “sports” because it contains the word °first°, independently from the fact that it also contains the word °base°. These two words are considered separately but not in correlation. Despite their naive scheme and apparently simplified assumptions, naïve Bayes classifiers have worked quite well in many difficult and practical situations.

Mathematically the problem can be formulated by considering an instance observation characterized by means of a suitable vector of ![](6/images/00046.jpeg) features ![](6/images/00150.jpeg) where the goal is to assign the best class probability![](6/images/00151.jpeg), ![](6/images/00152.jpeg)conditioned to the observation of X. This is statistically described as ![](6/images/00153.jpeg) and the Bayes theorem[[20]](#part0000_split_066.html__ftn20) allows to estimate this probability as follows:

![](6/images/00154.jpeg)

According to this theorem the posterior probability of assigning class ![](6/images/00155.jpeg) given the observation of ![](6/images/00071.jpeg)is equal to the prior probability of observing class ![](6/images/00155.jpeg) in the training set, multiplied by the likelihood of observing ![](6/images/00048.jpeg) conditioned to the observation of class ![](6/images/00155.jpeg) in the training set, divided by the probability of observing ![](6/images/00048.jpeg) in it. In other words this posterior prediction can be formulated in terms of observations in the training set.

In plain English:

![](6/images/00156.jpeg)

Now let’s focus on each single equation component: ![](6/images/00157.jpeg) is a constant scaling factor which will not influence the respective rank of each predicted category, so it can be safely ignored. ![](6/images/00158.jpeg) can be estimated for instance by considering the frequency of each category in the training set.

![](6/images/00159.jpeg)

The estimation of ![](6/images/00160.jpeg) can be done by using the chaining rule[[21]](#part0000_split_066.html__ftn21) which permits the calculation of any member of the joint distribution of a set of random variables using only conditional probabilities.

![](6/images/00161.jpeg)

![](6/images/00162.jpeg)

![](6/images/00163.jpeg)

![](6/images/00164.jpeg) 

The naïve assumption is that each feature is independent from all the remaining ones. So under this assumption:

![](6/images/00164.jpeg)

![](6/images/00165.jpeg)

And the Naive Bayes Classifier becomes very simple

![](6/images/00166.jpeg)

Where the symbol ![](6/images/00167.jpeg) denotes proportionality.

In short all categories are evaluated against the above formula and we pick just the one maximizing it:

![](6/images/00168.jpeg)

Note that multiplying small probabilities in ![](6/images/00073.jpeg) can be problematic, so usually it is more convenient to operate in a log-space by using a well-known algebraic property of logarithms![](6/images/00169.jpeg).

In order to estimate![](6/images/00170.jpeg) , we should distinguish between discrete training data (for instance the features used for textual classification) and continuous training data (for instance: the features used for image classification that might be continuous). The former one can be modelled using Bernoulli or Multinomial distributions, while the latter one is typically modelled using Gaussians.

## 46.  What is a Bernoulli and a Multivariate Naïve Bayes?

### Solution

In Bernoulli all features are simple binary variables describing the presence or absence of one particular attribute in the observed training set. Therefore, Bernoulli can be modelled as

![](6/images/00171.jpeg)

where ![](6/images/00172.jpeg)  is the probability of observing feature ![](6/images/00173.jpeg) in class ![](6/images/00174.jpeg) Bernoulli is frequently used for text classification by explicitly modelling the presence or the absence of a word term ![](6/images/00175.jpeg) in the text.

A multivariate is a variant of Bernoulli, where ![](6/images/00173.jpeg) counts               the number of times an event was observed in a particular instance. Multivariates are very popular for text classifications where the text is represented by an independent collection of words: the so called bag of words. The likelihood of observing a word is mathematically expressed by

![](6/images/00176.jpeg)

Again, when computing small probabilities in![](6/images/00177.jpeg) , it is better to move into the log-space, so that ignoring the constant scaling factors we have

![](6/images/00178.jpeg)

Note that the latter one is a simple linear form of ![](6/images/00179.jpeg) with ![](6/images/00180.jpeg)  ![](6/images/00181.jpeg) and![](6/images/00182.jpeg). Also note that with this formulation if a probability is zero, this will wipe all other contributions. This problem is solved with the so called smoothing strategy, where some small constant factors are used to replace zero.

The code here below uses Spark to train a multinomial Bayes classifier on text data. The metric adopted for evaluating quality is accuracy, which is the number of correct predictions made, divided by the total number of predictions made and multiplied by 100 to turn it into a percentage. Accuracy is calculated by using a map-reduce computation on Spark. Note that the dataset has been split in training (70% of the data) and test (30% of the data). The smoothing factor is set to![](6/images/00183.jpeg).

### Code             

from pyspark.mllib.classification import NaiveBayes

from pyspark.mllib.linalg import Vectors

from pyspark.mllib.regression import LabeledPoint

# create an appopriate LabeledPoint of tuples (label, features)

def  parseLine(line):

parts = line.split(',')

label = float(parts[0])

features = Vectors.dense([float(x)  for x in parts[1].split(' ')])

 return LabeledPoint(label, features)

#create an RDD from the text file made up of LabeledPoint  

data = sc.textFile('data/mllib/sample_naive_bayes_data.txt').map(parseLine)

# Split data into training (70%) and test (30%)

# Fix the seed for reproducipility of the experiment

training, test = data.randomSplit([0.7,  0.3], seed =  0)

# Train a multinomial naive Bayes with smoothing factor 1.0

model = NaiveBayes.train(training,  1.0)

# Make prediction and test accuracy

predictionAndLabel = test.map(lambda p :  (model.predict(p.features), p.label))

accuracy =  1.0  * predictionAndLabel.filter(lambda  (x, v): x == v).count()  / test.count()

## 47.  What is a Gaussian?

### Solution

A Gaussian is a family of mathematical functions which shows a characteristic symmetric “bell curve” shape.  Mathematically: given the mean ![](6/images/00123.jpeg) and the variance ![](6/images/00184.jpeg), a Gaussian is defined as

![](6/images/00185.jpeg)

The Gaussian distribution is a very common continuous probability distribution frequently used in statistics because of the Central Limit Theorem. This theorem states that average random variables independently drawn from independent distributions (also known as i.i.d.) are normally distributed.

The simplest case of normal distribution is![](6/images/00186.jpeg). In the following examples 500 random numbers are sampled with ![](6/images/00187.jpeg) and associated to buckets. The drawn values have the classical bell shape. The function has its peak at the mean and the “spread” increases by increasing the standard deviation ![](6/images/00188.jpeg)

### Code

import matplotlib.pyplot as plt

import numpy as np

mu, sigma =  0,  1  # mean and standard deviation

s = np.random.normal(mu, sigma,  500)

count, bins, ignored = plt.hist(s,  50, normed=True)

plt.plot(bins,  1/(sigma * np.sqrt(2  * np.pi))  *

               np.exp(  -  (bins - mu)**2  /  (2  * sigma**2)  ),

               linewidth=2, color='r')

plt.show()

![](6/images/00189.jpeg)

As an exercise try to plot the image for different values of ![](6/images/00123.jpeg) and remark the differences.

## 48.  What is a Standard Scaling?

### Solution

If a data is described by a Gaussian then it might be convenient to transform it by scaling its features to unit variance and/or removing the mean using column summary statistics on the samples in the training set. The code here below implements the scaling to unit variance and the removing of the mean in Spark.

### Code

from pyspark.mllib.util import MLUtils

from pyspark.mllib.linalg import Vectors

from pyspark.mllib.feature import StandardScaler

data = MLUtils.loadLibSVMFile(sc,  "data/mllib/sample_libsvm_data.txt")

label = data.map(lambda x: x.label)

features = data.map(lambda x: x.features)

scaler1 = StandardScaler().fit(features)

scaler2 = StandardScaler(withMean=True, withStd=True).fit(features)

scaler3 = StandardScalerModel(scaler2.std, scaler2.mean)

# data1 is scaled to the unit variance

data1 = label.zip(scaler1.transform(features))

# data2 is scaled to the unit variance and has zero mean.

data2 = label.zip(scaler1.transform(features.map(lambda x: Vectors.dense(x.toArray()))))

# features are mapped into  dense vectors, for avoiding exceptions

# for transformation with zero mean on sparse vector.

## 49.  Why are statistical distributions important?

### Solution

Statistical distributions are important for modelling events and data. Distributions are characterized by functions such as the probability mass function (pmf), which provides the probability that a discrete[random variable](https://en.wikipedia.org/wiki/Random_variable)is exactly equal to some value, and the cumulative distribution function (CDF), which describes the probability of a real-valued random variable ![](6/images/00048.jpeg) to have a value less than or equal to![](6/images/00082.jpeg).  In addition to the Normal ones the following distributions are frequently used in Data Science:

|  | What | PMF | CMF | E(X) | VAR(X) |
| Bernoulli | A discrete distribution. It takes value 1 with ![](6/images/00190.jpeg) probability and value 0 with probability![](6/images/00191.jpeg)A classic example is a single toss of a coin. | ![](6/images/00192.jpeg)![](6/images/00193.jpeg) | ![](6/images/00194.jpeg) | ![](6/images/00190.jpeg) | ![](6/images/00195.jpeg) |
| Binomial | A discrete distribution. It describes the number of successes in a series of independent yes/no experiments all with the same probability of success. | ![](6/images/00196.jpeg)n, number of trialsk, number of successesp, probability of success in each trialwhere ![](6/images/00197.jpeg) | ![](6/images/00198.jpeg)![](6/images/00199.jpeg)![](6/images/00200.jpeg) | ![](6/images/00201.jpeg) | ![](6/images/00202.jpeg) |
| Poisson binomial | It describes the number of successes in a series of independent Yes/No experiments with different probabilities of success | ![](6/images/00203.jpeg)where ![](6/images/00204.jpeg) is the set of all subsets of k integers that can be selected from {1,2,3,...,n}. ![](6/images/00205.jpeg) is the complement of set A. | ![](6/images/00206.jpeg)where ![](6/images/00207.jpeg) | ![](6/images/00208.jpeg) | ![](6/images/00209.jpeg)![](6/images/00210.jpeg) |
| Poisson | A discrete distribution.  It describes the probability of events in a fixed interval of time / space with a known average rate arriving independently from time since the last event. | ![](6/images/00211.jpeg)![](6/images/00212.jpeg)![](6/images/00213.jpeg)The positive real number λ is the expected value of the random variable X and also of its variance.![](6/images/00214.jpeg) is an integer | ![](6/images/00215.jpeg) | ![](6/images/00216.jpeg) | ![](6/images/00216.jpeg) |
| Gaussian | A distribution on real. The central limit theorem: every variable modelled as a sum of many i.i.d, variables with finite mean, [variance](https://en.wikipedia.org/wiki/Variance) is normal. | ![](6/images/00217.jpeg)![](6/images/00218.jpeg) | ![](6/images/00219.jpeg) | ![](6/images/00216.jpeg) | ![](6/images/00220.jpeg) |

### Code

Numpy provides full support for all the distributions described above and many others more. The interested reader is encouraged to check them on Wikipedia.[[22]](#part0000_split_066.html__ftn22)

import numpy as np

n, p =  10,  .5  # number of trials, probability of each trial

s = np.random.binomial(n, p,  100)

print s

## 50.  Can you compare your data with some distribution? What is a qq-plot?

### Solution

If you want to investigate whether your data follow some distribution (normal, uniform), one useful way is to use a qq-plot, which can compare two probability distributions by plotting their quantiles against each other. If the distributions are similar, then the graph will show a straight line.

### Code

import numpy as np

import pylab

import scipy.stats as stats

measurements = np.random.normal(loc =  40, scale =  10, size=80)  

stats.probplot(measurements, dist="norm", plot=pylab)

pylab.show()

![](6/images/00221.jpeg)

## 51.  What is a Gaussian Naïve Bayes?

### Solution

If the data is continuous, it might be convenient to estimate the probability by using a Gaussian distribution. So if feature ![](6/images/00173.jpeg) is continuous, we compute the mean ![](6/images/00222.jpeg) and the variance ![](6/images/00222.jpeg)of ![](6/images/00173.jpeg) in ![](6/images/00223.jpeg) , then we model the probabilities as Gaussians in this way:

![](6/images/00224.jpeg)

As discussed, it could be useful to check whether our data is indeed showing a Gaussian distribution by using tools such as qq-plot.

## 52.  What is another way to use Naïve Bayes with continuous data?

### Solution

Another approach for dealing with continuous features is to discretize them in buckets and use Multinomial Naïve Bayes for the discrete model. However some attention should be put in place for determining the right number of buckets.

## 53.  What is the Nearest Neighbor classification?

### Solution

A “nearest neighbor” is a very simple form of classification where each instance is assigned to the objects which are closer to the instance. During the training phase the space of features is partitioned in regions according to the position of the training instances. Then during the application phase the distance with respect to the training instances is used to classify real data.

There are many choices that can be made. For instance we can consider the closest object or we consider up to ![](6/images/00019.jpeg) objects and let them vote to pick the winning class. This is the so called k-NN classifier. Also we might define different types of vectorial distances. Given two vectors![](6/images/00225.jpeg) and ![](6/images/00226.jpeg)

|  | Formula | Description | Visually |
| Euclidean | ![](6/images/00227.jpeg) | The Euclidean formula represents the intuitive notion of distance of two points in space. | ![http://resumbrae.com/ub/dms423_f06/12/euclidean.png](6/images/00228.jpeg) |
| Manhattan | ![](6/images/00229.jpeg) | “Manhattan” intuitively maps all the points into a squared grid (similar to the Manhattan map) and the connections can only happen either vertically or horizontally | ![https://upload.wikimedia.org/wikipedia/commons/thumb/0/08/Manhattan_distance.svg/283px-Manhattan_distance.svg.png](6/images/00230.jpeg) |
| Hamming | #(![](6/images/00231.jpeg)) | Number of positions where the single vector components are different. | 2473996 2233796Have distance 3 |
| Jaccard | ![](6/images/00232.jpeg) | Jaccard distance represents the similarity between two sets | ![](6/images/00233.jpeg)![](6/images/00234.jpeg)![](6/images/00235.jpeg) |

Implementing the exact nearest neighbor can be very expensive. Therefore many approximate variants have been proposed, which are generally based on the idea of sampling the feature of space. The interested reader can find here an experimental alpha implementation for Spark.[[23]](#part0000_split_066.html__ftn23)

The code snippet implements here a simple version of Knn where K=1\. More sophisticate implementations are based on advanced data structures such as KD-Trees.[[24]](#part0000_split_066.html__ftn24)

### Code

import numpy as np

def  dist(p0, p1):

 return np.sum((p0-p1)**2)

def  knn(training, trainingLabels, newPoint):

dists = np.array([distance(t, newPoint)]  for t in training)

nearest = dists.argmin()

 return trainingLabels[nearest]

## 54.  What are Support Vector Machines (SVM)?

### Solution

Support vector machines aim to identify a hyperplane in a high dimensional space of features. Intuitively the best hyperplane is the one having the largest distance to the nearest data point observed in any training data. In fact this hyperplane provides the best separation among the training data. The image below provides a toy example where in ![](6/images/00236.jpeg) line ![](6/images/00237.jpeg) does not provide any separation between the training data, while e line ![](6/images/00238.jpeg) provides a non optimal separation. Instead ![](6/images/00239.jpeg) provides the maximum separation margin.

| ![](6/images/00240.jpeg) |  |

Mathematically let us assume to have a training set made of pairs of features and true binary labels: ![](6/images/00241.jpeg) and let us assume that the data here can be linearly separated by a hyperplane, which is described by the linear relation ![](6/images/00242.jpeg) for a suitable weight vector![](6/images/00090.jpeg).  Let us consider two additional hyperplanes: one for the positive examples ![](6/images/00243.jpeg) and one for the negative examples![](6/images/00244.jpeg) .

Recalling the distance from a point ![](6/images/00245.jpeg) to a line: ![](6/images/00246.jpeg) is ![](6/images/00247.jpeg) and as consequence the distance between ![](6/images/00248.jpeg) and ![](6/images/00237.jpeg)is then ![](6/images/00249.jpeg).

Therefore the total distance between ![](6/images/00237.jpeg)and ![](6/images/00238.jpeg) is ![](6/images/00250.jpeg) and for minimizing the distance we need to maximize the![](6/images/00251.jpeg). However we also want that no data point touches the margins which can be expressed as

![](6/images/00252.jpeg).

More synthetically we want to solve the optimization problem

![](6/images/00253.jpeg) under the constrains![](6/images/00254.jpeg)

Since the square root is a monotonic function, we can more conveniently solve the problem in this way:

![](6/images/00255.jpeg) under the constrains![](6/images/00254.jpeg)

Fortunately there are packages which can solve this optimization problem with advanced mathematical tools. For instance: Spark implements SVM with hinge loss function ![](6/images/00256.jpeg), regularization of type L1 or L2\. The optimization problem is solved by using the Stochastic Gradient Descent.

Once the model is learned, the prediction is simply a vector multiplication. For each application instance ![](6/images/00257.jpeg) if ![](6/images/00258.jpeg) the outcome is positive, otherwise it is negative.

Note that the data points in each class lying closest to the classification line are called “support vectors” and they are the reason for the name of this methodology.

### Code

from pyspark.mllib.classification import SVMWithSGD, SVMModel

from pyspark.mllib.regression import LabeledPoint

# Load and parse the data into LabeledPoint

def  parsePoint(line):

values =  [float(x)  for x in line.split(' ')]

 return LabeledPoint(values[0], values[1:])

data = sc.textFile("data/mllib/sample_svm_data.txt")

parsedData = data.map(parsePoint)

# Build the model for SVM with Stocastic Gradient Descent

model = SVMWithSGD.train(parsedData, iterations=100)

# Evaluating the model on training data

labelsAndPreds = parsedData.map(lambda p:  (p.label, model.predict(p.features)))

# Compute the accuracy

trainErr = labelsAndPreds.filter(lambda  (v, p): v != p).count()  / float(parsedData.count())

print("Training Error = "  + str(trainErr))

## 55.  What are SVM Kernel tricks?

### Solution

If a linear separation is not enough, then it is still possible to use SVM with simple tricks.  For example, if the original data consists of 3-dimensional vectors [x, y, z] , then we could compute a new 9-dimensional feature vector ![](6/images/00259.jpeg). This basic idea can be extended as explained in “Random Features for Large-Scale Kernel Machines”[[25]](#part0000_split_066.html__ftn25). The intuition here is that Kernel methods remember the![](6/images/00133.jpeg)-th training example ![](6/images/00260.jpeg)and combine it with a another training example.

In certain situations an additional structure is added and the kernel is a special function which maps the input space ![](6/images/00123.jpeg) into another space ![](6/images/00261.jpeg) so that ![](6/images/00262.jpeg)  ![](6/images/00263.jpeg) and the Kernel is an inner product between ![](6/images/00264.jpeg) and ![](6/images/00265.jpeg) , where two features ![](6/images/00266.jpeg) are provided from the original input space. In other words a kernel function maps a non-linear boundary in the problem space to a linear boundary in a higher dimensional space.

![SVM linearly non-separable](6/images/00267.jpeg)

These are examples of kernels frequently used in machine learning

| Examples of kernels | Meaning |
| ![](6/images/00268.jpeg) | Polynomial for some degrees ![](6/images/00269.jpeg) |
| ![](6/images/00270.jpeg) | Sigmoid for some parameters ![](6/images/00271.jpeg) |
| ![](6/images/00272.jpeg) | Radial basis for some parameters ![](6/images/00123.jpeg) |

## 56.  What is K-Means Clustering?

### Solution

K-means is a form of flat clustering where the goal is to partition space into a set of groups without creating relations among them. In the next volume we will present a form of hierarchical clustering where the groups are organized in a hierarchical tree.

K-Means is a form of unsupervised learning, where the actual data is grouped in ![](6/images/00147.jpeg) different clusters.  Mathematically: given ![](6/images/00273.jpeg)observations![](6/images/00274.jpeg), where each observation is a vector of ![](6/images/00060.jpeg) features![](6/images/00275.jpeg), ![](6/images/00147.jpeg)-means method partitions the ![](6/images/00276.jpeg) observations in ![](6/images/00277.jpeg) sets ![](6/images/00278.jpeg) in such a way that the within-cluster error expressed as sum of squares is minimized

![](6/images/00279.jpeg)

An approximate solution to the problem is computed iteratively. The algorithm starts by randomly picking ![](6/images/00147.jpeg) points in![](6/images/00280.jpeg)the so-called centroids. Then alternatively two steps are repeated until either a convergence or a stopping criteria is met. First, each observation is assigned to the group, the centroid of which has the least within-cluster sum of squares from the observation. Then the mean for each group is updated by considering the observations layingwithin the group. The algorithm has converged when the assignments no longer change. Since both steps optimize the infra-cluster distance and only a finite number of such partitions exists, the algorithm must converge to a (local) optimum.  

K-Means++ is a variant of K-Means where the initial K clusters are spread out:  the first cluster center is chosen uniformly at random from the application data points, after which each successive cluster center is chosen from the remaining data points with a probability that is proportional to its squared distance from the closest existing cluster center point. Spark implements a variant of K-Means++ called K-Means||[[26]](#part0000_split_066.html__ftn26) , suitable for parallel computation.

### Code

from pyspark.mllib.clustering import KMeans, KMeansModel

from numpy import array

from math import sqrt

# Load and parse the data into an appropriate RDD

data = sc.textFile("data/mllib/kmeans_data.txt")

parsedData = data.map(lambda line: array([float(x)  for x in line.split(' ')]))

# Build the model for a maxIterations=10

# and with 10 runs, with random centroid

clusters = KMeans.train(parsedData,  2, maxIterations=10,

        runs=10, initializationMode="random")

# Evaluate clustering by computing Within Set Sum of Squared Errors

def  error(point):

center = clusters.centers[clusters.predict(point)]

 return sqrt(sum([x**2  for x in  (point - center)]))

# each point is mapped into the error and all the errors are summed

WSSSE = parsedData.map(lambda point: error(point)).reduce(lambda x, y: x + y)

print("Within Set Sum of Squared Error = "  + str(WSSSE))

## 57.  Can you provide an example for Text Classification with Spark?

### Solution

Let’s discuss about Text Classification in Spark and leverage multiple techniques introduced in previous questions.  In this example textual words are loaded and transformed into a vector space. Then the examples are split (70%, 30%) into training and test datasets where a Naïve Bayes model is learned. The error metric adopted is accuracy.

### Code

from pyspark import SparkContext, SparkConf

from pyspark.mllib.feature import HashingTF

from pyspark.mllib.regression import LabeledPoint

from pyspark.mllib.classification import NaiveBayes

conf = SparkConf().setMaster("local[*]").setAppName("Naive_Bayes")

sc = SparkContext(conf=conf)

# Hash words a discrete vector space

# with the limit of 10000 words

htf = HashingTF(10000)

#tokenize sentences and transform them into vector space model

# examples

dataRDD = sc.textFile("./positiveData.txt")

data = dataRDD.map(lambda text : LabeledPoint(1, htf.transform(text.split(" "))))

data.persist()

# Build training and test data sets for examples

# Training set is 70% of data, while test set is 30% of data

trainData, testData = data.randomSplit([0.7,  0.3])

# Train a Naive Bayes model on the training data

model = NaiveBayes.train(trainData)

# Compare predicted labels to actual labels

prediction_and_labels = testData.map(lambda point:  (model.predict(point.features), point.label))

# Filter to only correct predictions

correct = prediction_and_labels.filter(lambda  (predicted, actual): predicted == actual)

# Calculate and print accuracy rate

accuracy = correct.count()  / float(testh.count())

print  "Classifier correctly predicted category "  + str(accuracy *  100)  +  " percent of the time"

## 58.  Where to go from here

The best next step is to start playing with real data and applying the algorithms presented in this volume. Kaggle[[27]](#part0000_split_066.html__ftn27) is a platform for data prediction in competitions. Companies, organizations and researchers post their data and have it scrutinized by the best experts worldwide. So you can go there and run few competitions for showcasing your value!

Remember: great machine learning results can be achieved by finding the right mix among the steps described in the below image.

![](6/images/00281.jpeg)Every problem is represented by means of observed data. Data is noisy. So you need to select the right summaries via feature engineering along with the appropriate algorithm for learning. At the same time it is certainly useful to provide a good mathematical formulation to the machine learning problem. Then it is a matter of training (for supervised learning) and evaluation. For supervised learning a good gold set can help. The process is iterative: when you reach satisfying results or when you are stuck and don’t make any progress, that is exactly the right moment for iterating and improving, trying to refine and frequently re-assess all the choices made so far. After a few iterations you might be satisfied of your results and deploy the model online for making forecasts on real unseen data. Users will provide you with feedback (either explicit or implicit) and those are new signals that you might want to collect for further refining your models.

A great Data scientist always works in incremental and lean way!!!

 ![](6/images/00282.jpeg)

 ![](6/images/00283.jpeg)![](6/images/00284.jpeg)

![](6/images/00285.jpeg) ![](6/images/00286.jpeg)![](6/images/00287.jpeg)

![](6/images/00288.jpeg) ![](6/images/00289.jpeg) ![](6/images/00290.jpeg) ![](6/images/00291.jpeg)

![](6/images/00292.jpeg) ![](6/images/00293.jpeg)![](6/images/00293.jpeg)![](6/images/00293.jpeg)

 ![](6/images/00294.jpeg)

![](6/images/00295.jpeg) ![](6/images/00296.jpeg) ![](6/images/00297.jpeg)

I hope that this first volume provided you with some basic tools for machine learning and also reduced the halo of mystery surrounding the role of Data science (after all it is all about data, math, coding and lots of creativity!). The second volume will discuss in more details more advanced topics such as decision trees, random forests, mars, gradient boosted trees, ensembles, hyper-parameters search, density estimation, expectation-maximization, dimensional reduction, bagging, recommendations, neural networks, deep learning and associative rules.

## Appendix A

## 59.  Ultra-Quick introduction to Python

I assume that you are already familiar with programming languages and hopefully you already have some experience with Python. However it is useful to recall some peculiarities of the languages which are used in this book.

Python does not use { } for delimiting code blocks but instead it uses indentation, which can be confusing at the beginning if you are used to C/C++ programming. Importing a module and defining a function have a simple syntax

import numpy as np

def  dist(p0, p1):

 return np.sum((p0-p1)**2)

Lists are defined with square brackets and slicing operations are easily supported.

l=[1,2,3,4,5]

x[:3]  #first three

x[3:]  #three to end

x[2:4]  #2nd, 3rd, 4th

y = x[:]  #copy

List comprehension is useful for transforming a list into another list by selecting some elements or by transforming other elements with a suitable function. This example creates a list of 100 tuples ![](6/images/00298.jpeg)

pairs =  [(x, y)  for x in range(10)  for y in range(10)]

Python supports anonymous functions also known as lambda computation. This is frequently used in Spark as reported in this example:

# map reduce

textFile.map(lambda line: len(line.split())).reduce(lambda a, b: a if  (a > b)  else b)

Numpy is a library for efficient linear algebra and numerical computation. In this book we used numpy vectors intensively.

import numpy as np

def  dist(p0, p1):

 return np.sum((p0-p1)**2)

def  knn(training, trainingLabels, newPoint):

dists = np.array([distance(t, newPoint)]  for t in training)

nearest = dists.argmin()

 return trainingLabels[nearest]

Anaconda is a very convenient Python distribution for Data Science.[[28]](#part0000_split_066.html__ftn28)

## 60.  Ultra-Quick introduction to Probabilities

Probabilities can be seen as a way to quantify the uncertainty for an event ![](6/images/00299.jpeg) from a universe of events. Mathematically this is denoted with![](6/images/00300.jpeg). Two events ![](6/images/00301.jpeg)are independent if the probability of having both of them happening is![](6/images/00302.jpeg). If the events are not independent, then ![](6/images/00303.jpeg) , which means that the joint probability is equal to the conditional probability of seeing ![](6/images/00299.jpeg) given the![](6/images/00304.jpeg) times the probability of ![](6/images/00305.jpeg).

The Bayes theorem is a powerful tool for learning because it allows to reverse conditional probabilities. Mathematically the theorem states that:

![](6/images/00306.jpeg)

## 61.  Ultra-Quick introduction to Matrices and Vectors

Vectors of length ![](6/images/00046.jpeg) represent points in an ![](6/images/00046.jpeg)-dimensional space. Vectors are typically represented with the notation ![](6/images/00173.jpeg) with ![](6/images/00307.jpeg) and sometimes with bold letters ![](6/images/00082.jpeg) when there is no ambiguity. Matrices are tables with rows and columns. They are typically represented as ![](6/images/00308.jpeg) and when there is no ambiguity as A. The transpose of a matrix ![](6/images/00309.jpeg)is ![](6/images/00310.jpeg)and it is denoted as ![](6/images/00311.jpeg). The transpose of a vector ![](6/images/00082.jpeg)  of dimension n × 1 is the same vector 1 × n. 

Given a vector x, we define the norm ![](6/images/00312.jpeg)  and![](6/images/00313.jpeg), ![](6/images/00314.jpeg)

Given two vectors ![](6/images/00315.jpeg) y, the inner product![](6/images/00316.jpeg). Given the inner product, we define the cosine similarity as ![](6/images/00317.jpeg) , where ![](6/images/00123.jpeg) is the angle between the vectors represented by ![](6/images/00082.jpeg) and![](6/images/00075.jpeg).

Given two vectors x, y, the outer product ![](6/images/00318.jpeg) is equivalent to a matrix multiplication![](6/images/00319.jpeg), provided that ![](6/images/00082.jpeg) is represented as a![](6/images/00320.jpeg)column vector and ![](6/images/00087.jpeg) as an n × 1 column vector.

![](6/images/00321.jpeg)

ABOUT THE AUTHOR

An experienced data mining engineer, passionate about technology and innovation in consumers’ space. Interested in search and machine learning on massive dataset with a particular focus on query analysis, suggestions, entities, personalization, freshness and universal ranking. Antonio Gullì has worked in small startups, medium (Ask.com, Tiscali) and large corporations (Microsoft, RELX). His carrier path is about mixing industry with academic experience.

Antonio holds a Master Degree in Computer Science and a Master Degree in Engineering, and a Ph.D. in Computer Science. He founded two startups, one of them was one of the earliest search engine in Europe back in 1998\. He filed more than 20 patents in search, machine learning and distributed system. Antonio wrote several books on algorithms and currently he serves as (Senior) Program Committee member in many international conferences. 

“Nowadays, you must have a great combination of research skills and a just-get-it-done attitude.”

* * *

[[1]](#part0000_split_006.html__ftnref1)  [http://scikit-learn.org/stable/modules/classes.html#module-sklearn.metrics](http://scikit-learn.org/stable/modules/classes.html#module-sklearn.metrics)

[[2]](#part0000_split_008.html__ftnref2)  [http://docs.scipy.org/doc/scipy/reference/sparse.html](http://docs.scipy.org/doc/scipy/reference/sparse.html)

[[3]](#part0000_split_008.html__ftnref3)  [http://scikit-learn.org/stable/datasets/](http://scikit-learn.org/stable/datasets/)

[[4]](#part0000_split_009.html__ftnref4)  [https://www.mturk.com/mturk/welcome](https://www.mturk.com/mturk/welcome)

[[5]](#part0000_split_013.html__ftnref5)  [http://docs.scipy.org/doc/numpy/reference/routines.linalg.html](http://docs.scipy.org/doc/numpy/reference/routines.linalg.html)

[[6]](#part0000_split_013.html__ftnref6)  [http://docs.scipy.org/doc/scipy/reference/sparse.html](http://docs.scipy.org/doc/scipy/reference/sparse.html)

[[7]](#part0000_split_013.html__ftnref7)[http://hadoop.apache.org/docs/r2.6.0/api/org/apache/hadoop/mapred/InputFormat.html](http://hadoop.apache.org/docs/r2.6.0/api/org/apache/hadoop/mapred/InputFormat.html)

[[8]](#part0000_split_014.html__ftnref8)  [http://research.google.com/archive/mapreduce.html](http://research.google.com/archive/mapreduce.html)

[[9]](#part0000_split_014.html__ftnref9)  [http://codingplayground.blogspot.co.at/2010/09/cosmos-massive-computation-in-microsoft.html](http://codingplayground.blogspot.co.at/2010/09/cosmos-massive-computation-in-microsoft.html) 

[[10]](#part0000_split_015.html__ftnref10)[http://spark.apache.org/docs/latest/programming-guide.html#transformations](http://spark.apache.org/docs/latest/programming-guide.html#transformations)

[[11]](#part0000_split_015.html__ftnref11)[http://spark.apache.org/docs/latest/programming-guide.html#transformations](http://spark.apache.org/docs/latest/programming-guide.html#transformations)

[[12]](#part0000_split_025.html__ftnref12)  [https://networkx.github.io/documentation/latest/tutorial/tutorial.html](https://networkx.github.io/documentation/latest/tutorial/tutorial.html)

[[13]](#part0000_split_031.html__ftnref13)  [http://oauth.net/2/](http://oauth.net/2/)

[[14]](#part0000_split_034.html__ftnref14)  [https://en.wikipedia.org/wiki/Bloom_filter](https://en.wikipedia.org/wiki/Bloom_filter)

[[15]](#part0000_split_034.html__ftnref15)  [https://en.wikipedia.org/wiki/Count%E2%80%93min_sketch](https://en.wikipedia.org/wiki/Count%E2%80%93min_sketch)

[[16]](#part0000_split_034.html__ftnref16)  [https://en.wikipedia.org/wiki/MinHash](https://en.wikipedia.org/wiki/MinHash)

[[17]](#part0000_split_034.html__ftnref17)  [https://en.wikipedia.org/wiki/Locality-sensitive_hashing](https://en.wikipedia.org/wiki/Locality-sensitive_hashing)

[[18]](#part0000_split_039.html__ftnref18)  [https://en.wikipedia.org/wiki/Convex_function](https://en.wikipedia.org/wiki/Convex_function)

[[19]](#part0000_split_043.html__ftnref19)[https://spark.apache.org/docs/latest/api/scala/index.html#org.apache.spark.mllib.optimization.GradientDescent](https://spark.apache.org/docs/latest/api/scala/index.html#org.apache.spark.mllib.optimization.GradientDescent)

[[20]](#part0000_split_049.html__ftnref20)  [https://en.wikipedia.org/wiki/Bayes%27_theorem](https://en.wikipedia.org/wiki/Bayes%27_theorem)

[[21]](#part0000_split_049.html__ftnref21)  [https://en.wikipedia.org/wiki/Chain_rule_(probability)](https://en.wikipedia.org/wiki/Chain_rule_(probability))

[[22]](#part0000_split_053.html__ftnref22)  [https://en.wikipedia.org/wiki/List_of_probability_distributions](https://en.wikipedia.org/wiki/List_of_probability_distributions)

[[23]](#part0000_split_057.html__ftnref23)  [https://issues.apache.org/jira/browse/SPARK-2336](https://issues.apache.org/jira/browse/SPARK-2336)

[[24]](#part0000_split_057.html__ftnref24)  [https://en.wikipedia.org/wiki/K-d_tree](https://en.wikipedia.org/wiki/K-d_tree)

[[25]](#part0000_split_059.html__ftnref25)[http://www.eecs.berkeley.edu/~brecht/papers/07.rah.rec.nips.pdf](http://www.eecs.berkeley.edu/~brecht/papers/07.rah.rec.nips.pdf)

[[26]](#part0000_split_060.html__ftnref26)  [http://spark.apache.org/docs/latest/mllib-clustering.html#k-means](http://spark.apache.org/docs/latest/mllib-clustering.html#k-means)

[[27]](#part0000_split_062.html__ftnref27)  [https://www.kaggle.com/](https://www.kaggle.com/)

[[28]](#part0000_split_063.html__ftnref28)  [https://store.continuum.io/cshop/anaconda/](https://store.continuum.io/cshop/anaconda/)