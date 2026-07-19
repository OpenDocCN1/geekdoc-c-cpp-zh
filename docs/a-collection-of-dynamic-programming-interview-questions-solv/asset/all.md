![](images/00352.jpeg)

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

[5. Integer Knapsack – A knapsack has max capacity ![](images/00001.jpeg) and there are ![](images/00002.jpeg) items each with weight ![](images/00003.jpeg) and value![](images/00004.jpeg). Maximize the value in the knapsack without exceeding its max capacity](#part0000.html__Toc382123411)

[6. Edit Distance -– Given two strings, compute the edit distance between them](#part0000.html__Toc382123412)

[7. Neat Print – Given a sequence of words and a max number of words which can be put in a line, print the sequence of words neatly. Assume that no word is split across lines.](#part0000.html__Toc382123413)

[8. Eggs Drop – Given ![](images/00005.jpeg) eggs and ![](images/00002.jpeg) floors in a building, find the minimum number of trials required to determine the lowest floor from which an egg can be dropped without getting broken.](#part0000.html__Toc382123414)

[9. Jump Stairs – There is a stair with ![](images/00002.jpeg) steps. You can climb either one step or two steps at a time. How many different ways there are to climb the stair?](#part0000.html__Toc382123415)

[10. Jumping Array – Given an array of non-negative numbers, start at the first element and reach the end with a minimum number of jumps. A jump cannot exceed the length contained in the current position.](#part0000.html__Toc382123416)

[11. Dice -– Given n dice, count how many ways to get sum s.](#part0000.html__Toc382123417)

[12. Coin Change – Given ![](images/00002.jpeg) dollars, how many different ways there are to make the change into a set of coins![](images/00006.jpeg)?](#part0000.html__Toc382123418)

[13. Longest Palindrome String – Given a string, compute the longest palindromic substring](#part0000.html__Toc382123419)

[14. String Palindromes -– Given a string, find the minimum number of characters to be inserted for converting the string into a palindrome](#part0000.html__Toc382123420)

[15. LCS -– Given two strings S1 and S2, find the longest common substring](#part0000.html__Toc382123421)

[16. LCS – Given two strings, find the longest common subsequence](#part0000.html__Toc382123422)

[17. LIS – Given an array of integers, find the longest increasing subsequence](#part0000.html__Toc382123423)

[18. Bridge Matching – n cities are on the northern bank of a river and n cities are on the southern bank. You can build a bridge only between cities with the same number](#part0000.html__Toc382123424)

[19. LBS – Given an array of integers, find the longest bitonic sequence](#part0000.html__Toc382123425)

[20. Box Stacking – Given a set of ![](images/00007.jpeg) boxes, compute the largest stack of boxes. A box can be stacked only on top of another box with larger base.](#part0000.html__Toc382123426)

[21. Sum Subset -– Given an array of integers of size![](images/00008.jpeg), partition it in such a way that the two subsets have equal sum ![](images/00009.jpeg)](#part0000.html__Toc382123427)

[22. Partition Set – partition a multiset S of positive integers into two subsets ![](images/00010.jpeg) and![](images/00011.jpeg), such that the sum of the numbers in ![](images/00012.jpeg)equals the sum of the numbers in ![](images/00013.jpeg)](#part0000.html__Toc382123428)

[23. Segment Partition -– Given a segment of integer length![](images/00008.jpeg), cut it into different integer parts in such a way to maximize the product of the lengths of all parts.](#part0000.html__Toc382123429)

[24. Cutting a Rod – given a rod of length n and a vector of prices for different lengths, cut the rod for maximizing the gain](#part0000.html__Toc382123430)

[25. Bellman-Ford – Given a graph ![](images/00014.jpeg) and a source vertex, find the shortest paths from the source ![](images/00015.jpeg) to all vertices. The graph may contain negative edges](#part0000.html__Toc382123431)

[26. Max Submatrix 0/1 - Given a matrix consisting only of ![](images/00016.jpeg) and![](images/00017.jpeg), find the maximum size square sub-matrix with all ![](images/00018.jpeg)](#part0000.html__Toc382123432)

[27. Matrix Parenthesization -- Given a set of ![](images/00019.jpeg) Matrices find the most efficient way of multiplying them](#part0000.html__Toc382123433)

[28. Max Submatrix – Given a matrix of size ![](images/00020.jpeg) find the maximum sum rectangle](#part0000.html__Toc382123434)

[29. Given a Binary Search Tree, find the size of the largest independent set of nodes](#part0000.html__Toc382123435)

[30. Optimal Binary Tree – given a set ![](images/00021.jpeg) of tuples ![](images/00022.jpeg) , where ![](images/00005.jpeg) is an integer and ![](images/00023.jpeg) is the number of times that ![](images/00005.jpeg) has been observed, build a binary search three such that the total cost of all single searches is minimized](#part0000.html__Toc382123436)

[31. Boolean Parenthesization – given a Boolean expression of and, or, xor, true, false, find the number of ways to parenthesize and evaluate to true](#part0000.html__Toc382123437)

[32. Games of Coins – a set of coins are aligned and two players can pick one coin from each side in turn. Maximize the value of the coins picked by the first player](#part0000.html__Toc382123438)

[33. Maximum value contiguous subsequence – given an array of real numbers, find a contiguous subsequence with max sum ![](images/00009.jpeg)](#part0000.html__Toc382123439)

[34. Balanced partition – given an array of integers between 0 and![](images/00024.jpeg), divide the integers into two sets such that the difference of their sums is minimized](#part0000.html__Toc382123440)

[35. Scheduling – given ![](images/00002.jpeg) jobs, each one with a processing time ![](images/00025.jpeg), a profit ![](images/00026.jpeg) and a deadline ![](images/00027.jpeg), maximize the profit](#part0000.html__Toc382123441)

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

![](images/00028.jpeg)

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

Complexity is here exponential since ![](images/00029.jpeg) . An alternative and more efficient solution memorizes the intermediate results and it avoids to recompute the same sub-problem for multiple times. A solution is:

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

The binomial coefficient indexed by ![](images/00002.jpeg) and ![](images/00005.jpeg) and denoted by ![](images/00030.jpeg) is the coefficient of the ![](images/00031.jpeg) term in the polynomial expansion of the binomial power![](images/00032.jpeg). The value of this coefficient is given by![](images/00033.jpeg).

Solution

Computing the binomial coefficient directly from the closed formula ![](images/00034.jpeg) would be inefficient. However, we can prove by induction that  ![](images/00030.jpeg) = ![](images/00035.jpeg)  and we know that ![](images/00036.jpeg)  and![](images/00037.jpeg)  .Therefore, we have a direct way to compute the binomial coefficient with dynamic programming. Note that Matrix is a class defined in the appendix.

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

Linear in time![](images/00038.jpeg)). Space occupancy is ![](images/00039.jpeg)

# 3. Max sub-array problem - given an array of integers, compute the largest sum continuous sub array

Solution

This problem is a little gem. An elegant solution has been provided by Kadane.[[1]](#part0000.html__ftn1) The key intuition for this algorithm is illustrated by this picture

 ![](images/00040.jpeg)![](images/00041.jpeg)![](images/00042.jpeg)

![](images/00043.jpeg) represents the maximum value computed before analysing the current subsequence, while ![](images/00044.jpeg) represents the maximum for the current subsequence. If ![](images/00045.jpeg) , we violate the sequence continuity and therefore we can safely reset![](images/00046.jpeg) , a value which represents the empty string. If![](images/00047.jpeg), then we have found a new maximum and we can update the ![](images/00048.jpeg)accordingly:

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

Linear in the size of the input ![](images/00049.jpeg)

# 4. Catalan Numbers

Catalan numbers are mathematically defined as:

![](images/00050.jpeg)

Those numbers have multiple applications in combinatorics.  For example:  ![](images/00051.jpeg) counts the number of expressions containing![](images/00002.jpeg)pairs of parentheses which are correctly matched (e.g. ![](images/00052.jpeg) represents  ((()))     ()(())     ()()()     (())()     (()()) ).  Also, ![](images/00051.jpeg) is the number of different ways ![](images/00053.jpeg) factors can be completely parenthesized (e.g. ![](images/00052.jpeg) represents ((ab)c)d     (a(bc))d     (ab)(cd)     a((bc)d)     a(b(cd))) ). In addition, ![](images/00051.jpeg) is also the number of full binary trees with ![](images/00054.jpeg) leaves. For a complete description of the applications please refer Wikipedia[[2]](#part0000.html__ftn2).

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

Linear in the size of the input, ![](images/00055.jpeg)

Solution

Notice that we can leverage the symmetry in the definition. For instance![](images/00056.jpeg). This observation leads to the following recursive implementation.

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

# 5. Integer Knapsack – A knapsack has max capacity C and there are n items each with weight w[i] and value![](images/00057.jpeg)v[i]. Maximize the value in the knapsack without exceeding its max capacity

Solution

An item can be inserted in the knapsack or not: if the ![](images/00058.jpeg) item is inserted, then the total value contained in the knapsack will increase of ![](images/00059.jpeg) and the capacity ![](images/00060.jpeg)will decreases of![](images/00061.jpeg). If the item is not inserted, than the capacity will remain unchanged.  This means that the solution can be then obtained recursively. Mathematically, we can define:

![](images/00062.jpeg)

![](images/00063.jpeg)

In the remaining, we provide two different solutions: the first is top-down and recursive, while the second is based on dynamic programming and it is built bottom-up by storing partial results in a support array![](images/00064.jpeg).

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

Pseudolinear in time ![](images/00065.jpeg) and Pseudolinear in space ![](images/00065.jpeg)

# 6. Edit Distance -– Given two strings, compute the edit distance between them

Solution

The edit distance is the minimum number of edits required to convert one string into another. For simplicity, we assume that the cost of insertion and deletion is 1\. Consider two strings ![](images/00066.jpeg) and![](images/00067.jpeg), we can define a cursor ![](images/00068.jpeg) for scanning S1 and a cursor ![](images/00069.jpeg) for scanning S2\. The edit distance ![](images/00070.jpeg) is defined as it follows:

![](images/00071.jpeg)

In other words: if the characters are aligned, the edit distance for the problem ![](images/00072.jpeg) will not increase, otherwise we need to align the strings by reducing the size of S1, or S2 or both.

Now let’s consider the base cases. Clearly, ![](images/00073.jpeg) because this case represents the empty strings. We can also define ![](images/00074.jpeg) and ![](images/00075.jpeg) , because in this case we are comparing a string of length ![](images/00076.jpeg) (respectively ![](images/00077.jpeg)) with the empty string. We can use the above definition for computing the edit distance by tabulating all the values ![](images/00078.jpeg) with complexity![](images/00079.jpeg).

However, we can significantly improve the complexity by taking into account that we only need the input from the previous column in the table for computing the current column. This will allow us to require only![](images/00080.jpeg). The code uses initialize the column ![](images/00081.jpeg) for each![](images/00082.jpeg) and this represents the maximum cost for position![](images/00083.jpeg). Then, we have two loops. The most external loop scans the string ![](images/00010.jpeg) for each ![](images/00068.jpeg) and it initializes ![](images/00084.jpeg) which the maximum cost for the position. The internal loop scans the string ![](images/00013.jpeg) for each ![](images/00069.jpeg) and updates the edit distance value by directly applying the recursive definition. When the internal loop is concluded the columns ![](images/00085.jpeg) and ![](images/00086.jpeg) are swapped and the scan of ![](images/00010.jpeg) continues.

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

Complexity is  ![](images/00087.jpeg)

# 7. Neat Print – Given a sequence of words and a max number of words which can be put in a line, print the sequence of words neatly. Assume that no word is split across lines.

Solution

Let ![](images/00088.jpeg) be the length of  word![](images/00089.jpeg). Intuitively, the cost of the first word is ![](images/00090.jpeg) and for the remaining words we can initially define![](images/00091.jpeg). Also, let ![](images/00092.jpeg) and consider the following recurrence, where we build the optimal cost for word![](images/00093.jpeg), by considering the optimal cost for word![](images/00094.jpeg):

![](images/00095.jpeg)

However this definition is not yet meeting our goal for two reasons. First, ![](images/00096.jpeg) only considers the cost of the previous word, while it should consider all the words that can fit a line up to a maximal cost![](images/00097.jpeg). Therefore we need to redefine ![](images/00096.jpeg) in such a way to accumulate the cost of the previous words and stop before at the point where this cost becomes negative. Intuitively for each given word we need to scan no more than a ![](images/00098.jpeg) position backwards. This can be addressed by defining ![](images/00099.jpeg) for a leftmost word ![](images/00100.jpeg)  such that![](images/00101.jpeg). Second, the cost should be non-linear because we want to balance across lines  (e.g. leaving two positions in one same line should intuitively cost more than leaving a position in one and the other position in another line). This requirement can be fulfilled in multiple ways, for instance by defining ![](images/00102.jpeg) or more conveniently for bitwise computation: ![](images/00103.jpeg). To summarize our goal is to find:

![](images/00104.jpeg) such that![](images/00105.jpeg). In the code the vector ![](images/00106.jpeg) will contain final decreasing values containing the residuals for each word added to a given line. The values will increase again anytime that there is a need to change line.

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

Note that ![](images/00107.jpeg) can be computed in linear time of the input size, while ![](images/00108.jpeg) can be computed in ![](images/00109.jpeg) time.

# 8. Eggs Drop – Given k eggs and n floors in a building, find the minimum number of trials required to determine the lowest floor from which an egg can be dropped without getting broken.

Solution

This is a classical puzzle, frequently asked during interviews. Let ![](images/00110.jpeg) be the minimum number of attempts given ![](images/00005.jpeg)  eggs and n floors. A dynamic solution can be computed by considering that when we drop an egg from floor f there are only two possible outcomes:

a) If the egg breaks, then we have ![](images/00111.jpeg) eggs and we need to check the ![](images/00112.jpeg) floor

b) If the egg does not break, then we have ![](images/00005.jpeg) eggs  and the remaining ![](images/00113.jpeg) floors left

Since we want to minimize the number of attempts, in the worst scenario we have to consider the maximum between a) and b). The relation then becomes:

![](images/00114.jpeg)

![](images/00115.jpeg)

The base case are: ![](images/00116.jpeg)because if we have only one egg then we have no other option but to climb the floors one by one, and ![](images/00117.jpeg) because if we have only one floor then we just need to check it. In addition, we can define![](images/00118.jpeg) and![](images/00119.jpeg) because those are borderline cases.

This characterization leads to a straightforward recursion implementation given below where we memorize partial solutions in a support ![](images/00120.jpeg) for avoiding the recompute those solutions again and again.

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

The DP solution is left as exercise. A straightforward implementation needs ![](images/00121.jpeg) entries in a table where each entry is computed at most![](images/00008.jpeg)  times. Therefore, the algorithm runs in ![](images/00122.jpeg) time. Time complexity can be reduced to ![](images/00123.jpeg) , if we consider that the optimal floor  ![](images/00124.jpeg) for ![](images/00125.jpeg) is certainly equal or larger than the one for![](images/00126.jpeg), so we can avoid to restart the minimum computation from 1\. Also, it could be useful to prove that the function ![](images/00127.jpeg)  is convex in f so the minimum is unique and can be computed with a linear scan.

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

![](images/00128.jpeg)

This formula has a straightforward interpretation: we jump to the n step either from the ![](images/00129.jpeg) step or from the ![](images/00130.jpeg) step. Note that the base cases are different with respect to Fibonacci.

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

Given the array![](images/00131.jpeg)], the base cases are when ![](images/00132.jpeg) or when![](images/00133.jpeg). For those cases, we have no solution. Otherwise, the mathematical formulation can be computed for each  position ![](images/00076.jpeg)  by finding the maximum jump length for position ![](images/00134.jpeg) such that the required constrain ![](images/00135.jpeg) is not violated. Mathematically![](images/00136.jpeg).

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

Let’s suppose that each die has m faces and define a function ![](images/00137.jpeg) which counts how many ways we have to get sum ![](images/00138.jpeg)for ![](images/00002.jpeg)  dices with ![](images/00019.jpeg)  faces.  We can compute this function starting from the result with ![](images/00129.jpeg)  dices. In particular, if we get a sum ![](images/00139.jpeg) from ![](images/00129.jpeg) dice we need to add ![](images/00140.jpeg)from the ![](images/00141.jpeg) die for each![](images/00142.jpeg):

![](images/00143.jpeg)

Note that we have![](images/00144.jpeg) terms in this sum. We use a support table ![](images/00145.jpeg) where we store the current sum and the current dice. The base case is with only one die and in this case there is only one way to get the sum![](images/00146.jpeg)  therefore ![](images/00147.jpeg) for![](images/00148.jpeg). Then, for each possible sum value ![](images/00149.jpeg) and for each possible dice ![](images/00150.jpeg) and for each possible valid value produced by a die ![](images/00151.jpeg) we update ![](images/00145.jpeg) according to the above definition.

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

Complexity is ![](images/00152.jpeg)

# 12.  Coin Change – Given n dollars, how many different ways there are to make the change into a set of coins![](images/00153.jpeg)S?

Solution

Let’s define ![](images/00154.jpeg) and let ![](images/00155.jpeg) be the change for ![](images/00002.jpeg) dollars given a set ![](images/00156.jpeg)of![](images/00157.jpeg) coins. We suppose to a have an infinite amount of each type of coin![](images/00158.jpeg). A coin ![](images/00159.jpeg) can either be part of the change or not. This simple observation is used for a dynamic programming solution

![](images/00160.jpeg)

where ![](images/00161.jpeg) counts when the coin ![](images/00159.jpeg) has been not selected, while ![](images/00162.jpeg) counts the selection of a new coin![](images/00158.jpeg). The base cases are for ![](images/00163.jpeg) where the only solution is not to change any money, ![](images/00164.jpeg) for ![](images/00165.jpeg) where there is no solution because we have a negative amount of money![](images/00166.jpeg) and ![](images/00164.jpeg)  ![](images/00167.jpeg) because we have money but there is no change available. The first implementation is recursive, while the second is based on dynamic programming.

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

Time complexity is ![](images/00168.jpeg)

# 13.  Longest Palindrome String – Given a string, compute the longest palindromic substring

A string is palindromic if it is read the same backward and forward, as Madam, I’m Adam or Poor Dan is in a droop.

Solution

A solution can be computed for the string ![](images/00169.jpeg)  by considering that![](images/00170.jpeg) and

![](images/00171.jpeg)

This definition computes the longest palindromic substring by starting from the whole string![](images/00172.jpeg) and it is easy to directly write the code implementing this recursive formulation.

However, another more convenient approach is to define ![](images/00173.jpeg) if the string is palindromic for![](images/00174.jpeg) . The following base cases hold for single characters and for couple of characters:

![](images/00175.jpeg)

In addition, we can define the recurrence![](images/00176.jpeg) for increasing lengths ![](images/00177.jpeg) where ![](images/00178.jpeg) and![](images/00179.jpeg).

Note that with this definition the interval ![](images/00180.jpeg) is contained in the interval ![](images/00181.jpeg) and therefore we just need to test the two characters in the border![](images/00182.jpeg)). The code keep tracks of the starting position where the palindromic string begins (![](images/00183.jpeg)) and its length (![](images/00184.jpeg)).

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

Complexity is![](images/00185.jpeg) and space is![](images/00185.jpeg). Providing a solution with reduced space is left as exercise.

# 14.  String Palindromes -– Given a string, find the minimum number of characters to be inserted for converting the string into a palindrome

Solution

Consider the string ![](images/00186.jpeg) and define ![](images/00187.jpeg) as the number of characters to be inserted for getting a palindrome. We have:

![](images/00188.jpeg)

The base case are ![](images/00189.jpeg) if ![](images/00190.jpeg)  and

![](images/00191.jpeg)

A dynamic programming implementation can be realized by adopting a ![](images/00192.jpeg) which stores the minimum number of insertions needed to convert ![](images/00186.jpeg) into a palindrome. The table is filled in by incremental gap such that![](images/00193.jpeg) and by considering the subintervals contained between the positions![](images/00194.jpeg),![](images/00195.jpeg)

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

Complexity is ![](images/00196.jpeg) in time and space

# 15.  LCS -– Given two strings S1 and i, find the longest common substring

The longest common substring problem consists in finding the longest string that is a substring of two strings.[[3]](#part0000.html__ftn3)

Solution

On way to solve the problem is to find the longest common suffix for all the pairs of prefixes for the strings  ![](images/00010.jpeg) and S2\. The longest common suffix is:

![](images/00197.jpeg)

Given![](images/00198.jpeg), we can compute the longest common substring because the maximal of the longest common suffixes of all possible prefixes is the longest common substring of S1 and T1.

![](images/00199.jpeg)

![](images/00200.jpeg)

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

Complexity is ![](images/00123.jpeg) and space is![](images/00201.jpeg). Reducing the space to ![](images/00202.jpeg) is left as an exercise.

# 16.  LCS – Given two strings, find the longest common subsequence

Given the two strings, two subsequences are in common if they appear in the same order but not necessarily contiguous. The main difference with the previous problem is that here the terms are not consecutive.

Solution

A dynamic programming solution can be computed for the string ![](images/00203.jpeg)  and the string ![](images/00204.jpeg)1] by defining a recursive function ![](images/00205.jpeg) on the prefixes ![](images/00206.jpeg) and ![](images/00207.jpeg) of length ![](images/00076.jpeg) and ![](images/00077.jpeg)

![](images/00208.jpeg)

A dynamic programming solution can be built by using a table where we store the partial results of the above computation (function![](images/00209.jpeg)). In addition we store the direction that generated the table for reconstructing the common subsequence in a next step (function![](images/00210.jpeg))

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

Complexity is![](images/00201.jpeg) and space is![](images/00201.jpeg).

# 17.  LIS – Given an array of integers, find the longest increasing subsequence

Solution

The solution can be quickly identified by dynamic programming. Suppose that we scan the array A, then at position ![](images/00076.jpeg) we have that ![](images/00211.jpeg)   

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

Complexity is ![](images/00212.jpeg) and space is![](images/00213.jpeg).  An ![](images/00214.jpeg) algorithm is described here[[4]](#part0000.html__ftn4).

# 18.  Bridge Matching – n cities are on the northern bank of a river and n cities are on the southern bank. You can build a bridge only between cities with the same number

Solution

Let ![](images/00215.jpeg) be the number of cit![](images/00216.jpeg) on the northern bank and ![](images/00217.jpeg) the number of cit![](images/00218.jpeg) on the southern bank. The problem can be reduced to the one of finding the longest common subsequence. Suppose to sort the bridges built by their first city. If two bridges cross, then we have one bridge ![](images/00219.jpeg) and another bridge ![](images/00220.jpeg) such that either ![](images/00221.jpeg) and ![](images/00222.jpeg) or ![](images/00223.jpeg) and![](images/00224.jpeg). We can sort the tuples by increasing ![](images/00225.jpeg) indexes and then compute the longest increasing sequence (LIS) on the sequence of![](images/00158.jpeg).

Code

Left as exercise

Complexity

Since we need to sort the complexity is ![](images/00226.jpeg)

# 19.  LBS – Given an array of integers, find the longest bitonic sequence

Solution

A sequence is bitonic, if it initially increases and then decreases. For an array ![](images/00227.jpeg)  we can compute the longest increasing sequence ![](images/00228.jpeg) ending at position ![](images/00076.jpeg) and the longest decreasing sequence ![](images/00229.jpeg) starting at position![](images/00093.jpeg). For each position ![](images/00076.jpeg) we define:

![](images/00230.jpeg)

and

![](images/00231.jpeg)

Code

Left as exercise

Complexity

Complexity is![](images/00232.jpeg).

# 20.  Box Stacking – Given a set of 3d boxes, compute the largest stack of boxes. A box can be stacked only on top of another box with larger base.

Solution

This problem is a variation of the longest increasing sequence. Each box![](images/00093.jpeg) has three dimensions ![](images/00233.jpeg) which can be rotated to form the base: either (![](images/00234.jpeg)), or![](images/00235.jpeg), or![](images/00236.jpeg). If we suppose having infinite amount of each box types, then we can solve this problem by computing the LIS for the remaining dimensions of the box.

Code

Left as exercise

Complexity

Complexity is![](images/00237.jpeg).

# 21.  Sum Subset -– Given an array of integers of size![](images/00153.jpeg)n, partition it in such a way that the two subsets have equal sum s

Solution

Sum subset problem is and important problem in computer science with application in cryptography and complexity[[5]](#part0000.html__ftn5). The problem is NP-Complete. The most naïve solution generates all the subsets and for each of them it checks whether the sum is the right number. The complexity is ![](images/00238.jpeg) where ![](images/00239.jpeg)the size of the array.  

We can use Dynamic programming for providing a pseudo-polynomial solution. First, if the sum is odd there is no solution, while if the sum is even we can try to find a subset. Second, if the current element is larger than the sum we must skip it, otherwise we can decide whether we want to include it or not. Therefore ![](images/00240.jpeg) depends on![](images/00241.jpeg), if we don't include the element ![](images/00242.jpeg) for the position ![](images/00243.jpeg) and for the current sum value![](images/00244.jpeg). While it depends on ![](images/00245.jpeg) if we include the element.

![](images/00246.jpeg)

The base cases are ![](images/00247.jpeg) because there is always a subset with zero sum, and ![](images/00248.jpeg) because the empty set cannot have a subset of sum![](images/00093.jpeg). The code implements a recursive and a dynamic programming solution

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

Complexity is pseudo-polynomial ![](images/00249.jpeg)

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

Complexity is pseudo-polynomial![](images/00250.jpeg)), where ![](images/00251.jpeg) is the sum of elements in the vector.

# 23.  Segment Partition -– Given a segment of integer length![](images/00153.jpeg)n, cut it into different integer parts in such a way to maximize the product of the lengths of all parts.

Solution

We can split the segment for all the integer positions and compute the max product of the two parts. If we split it in position![](images/00093.jpeg), then the product is![](images/00252.jpeg). In addition, the part![](images/00253.jpeg) can be further split. So the product can be reclusively computed as![](images/00254.jpeg). The base cases are![](images/00255.jpeg).

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

The idea is very similar to the one of the previous problem. Let’s suppose to have an array of ![](images/00256.jpeg) we can define ![](images/00257.jpeg) for ![](images/00258.jpeg)

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

This is a classical dynamic programming problem and the solution is due to Bellman-Ford[[6]](#part0000.html__ftn6). Let’s suppose that ![](images/00259.jpeg) is the weight associated to the![](images/00260.jpeg) for each edge in a directed graph![](images/00261.jpeg). For our computation we need a support array ![](images/00262.jpeg) of size![](images/00263.jpeg). The first step is to initialize all entries in ![](images/00262.jpeg) to infinite with the only exception of ![](images/00264.jpeg) because ![](images/00015.jpeg) is reachable with zero distance. Then, for ![](images/00265.jpeg) times we compute:

![](images/00266.jpeg)

![](images/00267.jpeg)

![](images/00268.jpeg)

At the end a negative edge can be detected by checking for each edge whether![](images/00269.jpeg) , if ![](images/00270.jpeg)

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

Time complexity is![](images/00271.jpeg)

# 26.  Max Submatrix 0/1 - Given a matrix consisting only of 0s and![](images/00153.jpeg)1s, find the maximum size square sub-matrix with all 1s

Solution

A dynamic programming solution can be defined as follows. Let ![](images/00106.jpeg) be the matrix of 0s and 1s of size ![](images/00272.jpeg) and consider another matrix ![](images/00156.jpeg)of same size. If ![](images/00273.jpeg), then it can contribute to either position ![](images/00274.jpeg)[j], or![](images/00275.jpeg), or![](images/00276.jpeg)] which can be expressed as![](images/00277.jpeg). If ![](images/00278.jpeg) then![](images/00279.jpeg). Here is the code

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

Complexity is ![](images/00280.jpeg)

# 27.  Matrix Parenthesization -- Given a set of m Matrices find the most efficient way of multiplying them

Solution

Matrix multiplication is associative so there are multiple ways of performing the multiplication and therefore the number of operations (sum and multiplications) performed on scalars is different. Let’s suppose that the dimensions of the ![](images/00281.jpeg) matrix is contained in positions ![](images/00282.jpeg)  for a vector![](images/00283.jpeg).We can scan the vector and find a solution recursively.

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

Complexity is ![](images/00284.jpeg)

# 28.  Max Submatrix – Given a matrix of size n x n find the maximum sum rectangle

Solution

The problem is a natural generalization of the Kandane’s problem discussed previously. Suppose that we fix columns ![](images/00076.jpeg)  and![](images/00083.jpeg), then we can compute in linear time the top and bottom rows which maximize the rectangle.

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

Complexity is ![](images/00285.jpeg) , because Kandane is linear.

# 29.  Given a Binary Search Tree, find the size of the largest independent set of nodes

Solution

A set of nodes in a tree is independent if there are no edges directly connecting them in a father-children relation. A dynamic programming solution is based on the consideration that a node can be either part of the largest independent set or not. In the former case the size of the largest set will be the sum of the largest set of grandchildren plus 1 because we skip the grandchildren’s father. In the latter case the size of the largest set is the sum of the largest set of children because by construction we do not add any new node to the set. Formally:

![](images/00286.jpeg)

If a node is null then![](images/00287.jpeg).For avoiding re-computing partial results we can store the LIS(x) inside the node X.

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

The total complexity is ![](images/00049.jpeg) where ![](images/00002.jpeg) is  the number of nodes in the binary search tree.

# 30.  Optimal Binary Tree – given a set S of tuples <k, freq[k]> , where k is an integer and freq[k] is the number of times that k has been observed, build a binary search three such that the total cost of all single searches is minimized

Solution

One key intuition is that the cost of accessing a key is ![](images/00288.jpeg) , where ![](images/00289.jpeg) is the depth of key![](images/00290.jpeg).  A tuple can be the root of the binary search tree (BST) provided that it respects the BST properties:

*   The left [subtree](http://en.wikipedia.org/wiki/Tree_(data_structure)#Subtree) of a node contains only nodes with keys less than the node's key
*   The right subtree of a node contains only nodes with keys greater than the node's key
*   For the left and right subtree: each one must also be a binary search tree
*   There must be no duplicate nodes

Therefore we can write the cost function for the keys in ![](images/00291.jpeg) as it follows:

![](images/00292.jpeg)

In other words: when the node ![](images/00293.jpeg) becomes a root and we need to minimize the cost of the left keys ![](images/00294.jpeg) and the right keys ![](images/00295.jpeg). In addition, all the nodes below the new root node will have an additional level of depth and therefore we need to sum all their frequencies. The code provided uses memorization for avoiding recomputation of the same values again and again. The solution is built bottom-up.

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

The cost is ![](images/00296.jpeg) and space is ![](images/00212.jpeg)

# 31.  Boolean Parenthesization – given a Boolean expression of and, or, xor, true, false, find the number of ways to parenthesize and evaluate to true

Solution

Let ![](images/00297.jpeg) be the number of parenthesizations which are evaluated to true between positions ![](images/00076.jpeg) and![](images/00083.jpeg); and  ![](images/00298.jpeg)  be the number of parenthesization which are evaluated to false between positions ![](images/00076.jpeg) and![](images/00083.jpeg). Recursively

![](images/00299.jpeg)

Code

Left as exercise

Complexity

The running time is![](images/00300.jpeg), where ![](images/00002.jpeg) are the number of items in the expression.

# 32.  Games of Coins – a set of coins are aligned and two players can pick one coin from each side in turn. Maximize the value of the coins picked by the first player

Solution

Let suppose that the coins are represented in an array![](images/00301.jpeg). The value picked when the coins left are ![](images/00302.jpeg)must satisfy the recursive relation![](images/00303.jpeg):

![](images/00304.jpeg)

The key intuition is that the first player should select either coin ![](images/00305.jpeg) or coin ![](images/00306.jpeg) with the goal of maximizing his gain. For the sake of simplicity, let’s suppose he selects![](images/00307.jpeg): the other case is symmetric. We count ![](images/00308.jpeg) plus we aim at minimizing the value of the second player who can either pick another coin from the ![](images/00305.jpeg) side (position a+2) or pick a coin from the ![](images/00306.jpeg) side. The value is clearly 0 if![](images/00309.jpeg).

Code

Left as exercise

Complexity

There are ![](images/00310.jpeg) values for ![](images/00311.jpeg) and each single evaluation is ![](images/00312.jpeg), so the total run time is ![](images/00310.jpeg)

# 33.  Maximum value contiguous subsequence – given an array of real numbers, find a contiguous subsequence with max sum s

Solution

Let’s define ![](images/00313.jpeg)as the maximum value subsequence which ends at![](images/00093.jpeg). The element in position ![](images/00140.jpeg)can be either added or not. Recursively

![](images/00314.jpeg)

Code

Left as exercise

Complexity

There are ![](images/00239.jpeg)elements in ![](images/00106.jpeg) and the computing of each element requires to compute the maximum between two values. Therefore complexity is ![](images/00049.jpeg)

# 34.  Balanced partition – given an array of integers between 0 and M, divide the integers into two sets such that the difference of their sums is minimized

Solution

Let ![](images/00315.jpeg) , if the subset![](images/00316.jpeg)} sums to j. Recursively for the set of ![](images/00076.jpeg) elements we can start with a set of ![](images/00317.jpeg) elements and keep it as it is, or we can expand it by adding the element ![](images/00318.jpeg)

![](images/00319.jpeg)

Then considering the row ![](images/00320.jpeg) representing![](images/00321.jpeg)} we search the value![](images/00322.jpeg) such that ![](images/00323.jpeg) and the difference![](images/00324.jpeg) is minimized.

Code

Left as exercise

Complexity

There are ![](images/00002.jpeg) elements bounded by ![](images/00106.jpeg) while ![](images/00077.jpeg) needs to scan ![](images/00002.jpeg) elements. Therefore the complexity is ![](images/00325.jpeg)

# 35.  Scheduling – given n jobs, each one with a processing time ti a profit pi  and a deadline di, maximize the profit

Solution

Suppose that each job ![](images/00326.jpeg) has processing time ![](images/00327.jpeg) profit ![](images/00328.jpeg) and deadline ![](images/00329.jpeg) for ![](images/00330.jpeg) and that we get no profit, if the job is executed after its deadline. We want to maximize the profit ![](images/00331.jpeg) for ![](images/00330.jpeg) jobs executed at time![](images/00083.jpeg). Recursively,

![](images/00332.jpeg)

Code

Left as exercise

Complexity

If we assume that the processing time is bounded by![](images/00333.jpeg), then we need to compute ![](images/00077.jpeg) up to ![](images/00334.jpeg) and we have ![](images/00002.jpeg) jobs to consider. Therefore the total complexity is ![](images/00335.jpeg)

# 36.  Stock prices – Given a histogram array of unsigned integers encoding the price of a stock title during the previous year, compute the area for the largest rectangle contained in this histogram

Solution

Let A be the histogram array, we need to compute

![](images/00336.jpeg))

The most naïve implementation has complexity![](images/00337.jpeg). However we can achieve complexity![](images/00338.jpeg) by processing each element ![](images/00330.jpeg) and looking for the largest rectangle with height being at least![](images/00339.jpeg). Complexity can be further improved by considering that if we have ![](images/00340.jpeg)and ![](images/00341.jpeg) , then we can immediately discard ![](images/00342.jpeg) when processing the ![](images/00281.jpeg)entry and this can be efficiently achieved by using a stack.

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

Code runs in![](images/00338.jpeg).

# 37.  Ship Battle – Given a matrix M and an array V, match the array in the matrix

Solution

Let ![](images/00106.jpeg) be the matrix of size![](images/00343.jpeg), and ![](images/00227.jpeg) the array of size![](images/00344.jpeg). We can scan the matrix by rows ![](images/00330.jpeg) and by columns ![](images/00345.jpeg) and if ![](images/00346.jpeg)  , with vector at position![](images/00347.jpeg), we can recursively check, if there is a match for the eight positions adjacent to ![](images/00291.jpeg) with![](images/00348.jpeg).  Particular attention must be put for the corner cases as explained in the code. If we cache the situations where the match does not happen for tuples ![](images/00349.jpeg) , we can obtain complexity ![](images/00350.jpeg)

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

Code runs in![](images/00351.jpeg).

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