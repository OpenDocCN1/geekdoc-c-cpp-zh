# More NP-Complete Problems ■ 217

Not although only 0 and 1 are used as digits when constructing numbers, this is not binary representation! Each row in Figure 9.23 is one integer, base 10.

As shown in Figure 9.23, we begin by constructing two numbers for each variable x₁ ... xk—one for the positive literal xi and one for its negation ¬xi. As indicated in the upper left quadrant (I) in Figure 9.23, each pair of numbers corresponding to variable xi, has a 1 in column i of the table, with 0s in the following k-i columns to complete this quadrant.

The upper right quadrant (II) is constructed by cross-indexing each variable class. If the positive literal x, appears in class Ci, we place a 1 in the corresponding (k + j)th column for x; otherwise, the digit is 0. If the negative literal ¬x, appears in class Ci, we place a 1 in the corresponding (k + j)th column for ¬x; otherwise, the value is 0. Thus, each partial row in II may have any number of 1s since x, or ¬x, can appear in any of classes. Each partial column in II can have one (if the three-clause is x v x), twos (one repeated literal), or threes (three distinct literals).

For example, the literal x, occurs in Ci in the Boolean expression above, so the column for 1 in the upper right quadrant is set to 1; x does not appear in C2 or C3, so a 0 is placed in columns 2 and 3. The literal ¬x occurs in C+, so the column for 3 in the upper right quadrant is set to 1; ¬x does not appear in Ci, or C+, and so a 0 is placed in the columns for clauses 1 and 2. This is shown in Figure 9.24.

The lower right quadrant (III) adds a pair of numbers 10^{i-1} for each class Ci. These numbers serve as a reserve, so that we have the option of adding these numbers to reach the target of 3. If one literal is true in the class, we add both reserves; if two, we add one of the extras; and if all three are true, we ignore these numbers completely.

Note that if we do not satisfy Ci, we cannot reach 3 even if we add these reserves!

The target T for the list of numbers is 1³m; that is, the target has k + m digits, the first k of which are 1, the remaining m of which are 3—T the digit has 3 in final m positions, since our reduction from 3-CNF-SAT, meaning that each clause has exactly three literals. The upper right quadrant shows what variable assignment "hits" which clause. It is possible to satisfy a clause with all three literals true. For example, choosing ¬x₁, x₃, and ¬x₄ would hit C₃ three times; choosing the numbers corresponding to these literals would add 3 in the last column. However, it is also possible to satisfy a clause with two literals true (