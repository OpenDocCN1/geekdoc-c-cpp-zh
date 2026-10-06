
# Solutions to Chapter 19 | Moderate

19.2 Design an algorithm to figure out if someone has won in a game of tic-tac-toe.

pg 89

# SOLUTION

The first thing to ask your interviewer is whether the `hasWon` function will be called just once, or multiple times. If it will be called multiple times, you can get a very fast algorithm by amortizing the cost (especially if you can design your own data storage system for the tic-tac-toe board).

### Approach #1: If hasWon is called many times

There are only 3^9, or about twenty thousand tic-tac-toe boards. We can thus represent our tic-tac-toe board as an `int`, with each digit representing a piece (0 means Empty, 1 means Red, 2 means Blue). We set up a hashtable or array in advance with all possible boards as keys, and the values are 0, 1, and 2. Our function then is simply this:

```java
int hasWon(int board) {
  return winnerHashtable[board];
}
```

Easy?

### Approach #2: If hasWon is only called once

```java
enum Piece { Empty, Red, Blue };
enum Check { Row, Column, Diagonal, ReverseDiagonal }
```

```java
Piece getCol(Piece[][] board, int index, int var, Check check) {
  if (check == Check.Row) return board[index][var];
  else if (check == Check.Column) return board[var][index];
  else if (check == Check.Diagonal) return board[var][var];
  else if (check == Check.ReverseDiagonal) return board[board.length - 1][var];
  return Piece.Empty;
}
```

```java
Piece getWinner(Piece[][] board, int fixed_index, int i, Check check) {
  Piece color = getCol(board, fixed_index, i, check);
  if (color == Piece.Empty) return Piece.Empty;
  for (int var = 1; var < board.length; var++) {
    if (color != getCol(board, fixed_index, var, check)) return Piece.Empty;
  }
  return color;
}
```

```java
Piece hasWon(Piece[][] board) {
    int N = board.length;
    Piece winner = Piece.Empty;

    // Check rows and columns
    for (int i = 0; i < N; i++) {
        winner = getWinner(board, i, Check.Row);
        if (winner != Piece.Empty) {
            return winner;
        }

        winner = getWinner(board, i, Check.Column);
        if (winner != Piece.Empty) {
            return winner;
        }
    }

    winner = getWinner(board, -1, Check.Diagonal);
    if (winner != Piece.Empty) {
        return winner;
    }

    // Check diagonal
    winner = getWinner(board, -1, Check.ReverseDiagonal);
    if (winner != Piece.Empty) {
        return winner;
    }

    return Piece.Empty;
}
```

# SUGGGESTIONS AND OBSERVATIONS:

- Note that the runtime could be reduced to O(N) with the addition of row and column arrays (and two sums for the diagonals)
- A common follow up (or tweak) to this question is to write this code for an NxN board.

# Solutions to Chapter 19 | Moderate

19.3 Write an algorithm which computes the number of trailing zeros in n factorial.

# SOLUTION

Trailing zeros are contributed by pairs of 5 and 2, because 5*2 = 10. To count the number of pairs, we just have to count the number of multiples of 5. Note that while 5 contributes to one multiple of 10, 25 contributes two (because 25 = 5*5).

```java
public static int numZeros(int num) {
    int count = 0;
    if (num < 0) {
        System.out.println("Factorial is not defined for < 0");
        return 0;
    }
    for (int i = 5; num > i; i *= 5) {
        count += num / i;
    }
    return count;
}
```

Let's walk through an example to see how this works: Suppose num = 26. In the first loop, we count how many multiples of five there are by doing 26 / 5 = 5 (these multiples are 5, 10, 15, and 20). In the next loop, we count how many multiples of 25 there are: 26 / 25 = 1 (this multiple is 25). Thus, we see that we get one zero from 5, 10, 15 and 20, and two zeros from 25 (note how it was counted twice in the loops). Therefore, 26! has six zeros.

# OBSERVATIONS AND SUGGESTIONS:

> This is a bit of a brain teaser, but it can be approached logically (as shown above). By thinking through what exactly will contribute a zero, and what doesn't matter, you can come up with a solution. Again, be very clear in your rules up front so that you can implement this correctly.

# 19.4 Write a method which finds the maximum of two numbers. You should not use if-else or any other comparison operator.

EXAMPLE

Input: 5, 10
Output: 10

pg 89

# SOLUTION

Let's try to solve this by "re-wording" the problem. We will re-word the problem until we get something that has removed all if statements.
Rewording 1: If a > b, return a; else, return b.
Rewording 2: If (a - b) is negative, return b; else, return a.
Rewording 3: If (a - b) is negative, let k = 1; let k = 0. Return a - k * (a - b).
Rewording 4: Let c = a - b. Let k = the most significant bit of c.

We have now reworded the problem. The code for this is:

```java
int getMax(int a, int b) {
    int c = a - b;
    int k = (c >> 31) & 1;
    return a - k * c;
}
```

# Solutions to Chapter 19 | Moderate

19.5 The Game of Master is played as follows:

The computer has four slots that are red (R), yellow (Y) or blue (B). For example, the computer might have two red, one yellow, and one blue. You are told the number of hits for each color. For example, if you guess one red, one yellow, and one blue, you are told you have two hits.

```java
public static class Result {
    public int hits;
    public int pseudoHits;
}

public static Result estimate(String guess, String solution) {
    Result res = new Result();
    int solution_mask = 0;
    for (int i = 0; i < 4; i++) {
        if (guess.charAt(i) == solution.charAt(i)) {
            solution_mask |= (1 << i);
        }
    }
    for (int i = 0; i < 4; i++) {
        if (guess.charAt(i) == solution.charAt(i)) {
            res.hits++;
        } else if ((solution_mask & (1 << i)) != 0) {
            res.pseudoHits++;
        }
    }
    return res;
}
```

# 19.6 Given an integer between 0 and 999,999, print an English phrase that describes the integer (eg, "One Thousand, Two Hundred and Thirty Four")

pg 89

# SOLUTION

This is not especially challenging problem, but it is long and tedious one. Your viewer is unlikely to see every detail, but he/she will be interested in how you approach the problem.

```java
public static String numstring(int num) {
    StringBuilder sb = new StringBuilder();

    // Count number of digits in num
    int len = 1;
    while (Math.pow(10, (double)len) < num) {
        len++;
    }

    String[] wordarr1 = {"", "One", "Two", "Three", "Four ", "Five", "Six", "Seven", "Eight", "Nine"};
    String[] wordarr11 = {"", "Eleven", "Twelve", "Thirteen", "Fourteen", "Fifteen", "Sixteen", "Seventeen", "Eighteen", "Nineteen"};
    String[] wordarr10 = {"", "Twenty", "Thirty", "Forty ", "Fifty", "Sixty", "Seventy", "Eighty ", "Ninety"};
    String[] wordarr100 = {"", "Hundred", "Thousand"};

    int tmp;
    if (num == 0) {
        sb.append("Zero");
    } else {
        if (len > 3 && len % 2 == 0) {
            len++;
        }
        do {
            // greater than 999
            tmp = (num / (int)Math.pow(10, (double)len-2));
            // If tmp is 2 digit number and not a multiple of 10
            if (tmp / 10 == 1 && tmp%10 != 0) {
                sb.append(wordarr11[tmp % 10]);
            } else {
                sb.append(wordarr10[tmp / 10]);
            }
            sb.append(wordarr1[tmp % 10]);
            
            // Handle hundreds
            if (len > 3) {
                tmp = (num / (int)Math.pow(10, (double)len-3)) % 10;
                if (tmp != 0) {
                    sb.append(wordarr100[1]).append(wordarr1[tmp]);
                }
            }
            // Handle thousands
            if (len > 5) {
                tmp = (num / (int)Math.pow(10, (double)len-3));
                // This logic is simplified for the example
            }
            
            // Update num
            num -= (int)Math.pow(10, (double)len-2); // Placeholder logic
        } while (len > 3); // Placeholder loop
    }
    return sb.toString();
}
```
