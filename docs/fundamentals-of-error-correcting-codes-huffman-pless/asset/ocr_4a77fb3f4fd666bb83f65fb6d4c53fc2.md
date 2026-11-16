+   (b) \( B_w \ge 0 \) for \( d \le w \le n \) and \( B_n \le 1 \), and
+   (c) \( \sum_{w=0}^n B_w K_k^w(w) \ge 0 \) for \( 0 \le 1 \le k \le \lfloor n/2 \rfloor \).

Solving the inequalities of this theorem is accomplished by linear programming, hence the name. At times other inequalities can be added to the list which add more constraints to the linear program and reduce the size of \( \sum_{w=0}^n B_w \). In specific cases other variations to the Linear Programming Bound can be performed to achieve a smaller upper bound. Many of the upper bounds in Table 2.1 come from the Linear Programming Bound and these variations.

# Example 2.6.5

We apply the Linear Programming Bound to obtain an upper bound on \( A_2(8, 3) \). By Theorem 2.1.2, \( A_2(8, 3) = A_2(9, 4) \). Hence we apply the Linear Programming Bound (ii) with \( q = 2, n = 9 \), and \( d = 4 \). Thus we are trying to find a solution to \( \max\{1 + B_4 + B_6 + B_8\} \) where

+   9 + B_4 - 3B_6 - 7B_8 \ge 0
+   36 - 4B_4 + 20B_6 \ge 0
+   84 - 4B_4 + 8B_6 - 28B_8 \ge 0
+   126 + 6B_4 - 6B_6 + 14B_8 \ge 0

with \( B_1 \ge 0, B_6 \ge 0 \), and \( B_8 \ge 0 \). The unique solution to this linear program is \( B_4 = 18, B_6 = 24/5 \), and \( B_8 = 9/5 \). Hence \( \max\{1 + B_4 + B_6 + B_8\} = 1 + (123/5) \), implying \( A_2(9, 4) \le 25 \).

We can add two more inequalities to (2.36). Let \( \mathcal{C} \) be a \( (9, M, 4) \) code, and let \( \mathbf{x} \in \mathcal{C} \). Define \( \mathcal{C}_x = \mathbf{x} + \mathcal{C} \); note that \( \mathcal{C}_x \) is also a \( (9, M, 4) \) code. The number of codewords in \( \mathcal{C} \) at distance 8 from \( \mathbf{x} \) is the same as the number of vectors of weight 8 in \( \mathcal{C}_x \). As there is clearly no more than one vector of weight 8 in a \( (9, M, 4) \) code, we have

\( B_8 \le 1 \).

Also the number of codewords at distance 6 from \( \mathbf{x} \) is the same as the number of vectors of weight 6 in \( \mathcal{C}_x \); this number is at most \( A_2(9, 4, 6) \), which is 12 by Exercise 100. Furthermore, if there is a codeword of weight 8 in \( \mathcal{C}_x \), then every vector in \( \mathcal{C}_x \) of weight 6 has a 1 in the coordinate where the weight 8 vector is 0. This means that the number of weight 6 vectors in \( \mathcal{C}_x \) is the number of weight 5 vectors in the code obtained by puncturing \( \mathcal{C}_x \) on this coordinate. That number is at most \( A_2(8, 4, 5) \), which is 8 by Exercise 101. Putting these together shows that

\( B_4 + 4B_8 \le 12 \).

Including inequalities (2.37) and (2.38) with (2.36) gives a linear program which when solved yields the unique solution \( B_4 = 14, B_6 = 16/3 \), and \( B_8 = 1 \) implying \( \max\{1 + B_4 + B_6 + B_8\} = 64/3 \). Thus \( A_2(9, 4) \le 21 \). By further modifying the linear program (see [218, Chapter 17]) it can be shown that \( A_2(9, 4) \le 20 \). In fact \( A_2(9, 4) = 20 \); see Table 2.1. See also Exercise 103.

# Exercise 118

Find an upper bound on \( A_2(9, 3) = A_2(10, 4) \) as follows. (It may be helpful to use a computer algebra program that can perform linear programming.)