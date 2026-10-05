
Chap. 17 Limits to Computation

we cannot analyze. This comes as a result of the fact that the Halting Problem is unsolvable.

### 17.3.1 Uncountability

Before proving that the Halting Problem is unsolvable, we first prove that not all functions can be implemented as a computer program. This must be so because the number of programs is much smaller than the number of possible functions.

A set is said to be countable (or countably infinite) if it is a set with an infinite number of members) if every member of the set can be uniquely assigned to a positive integer. A set is said to be uncountable (or uncountably infinite) if it is not possible to assign every member of the set to its own positive integer.

To understand what we mean when say "assigned to a positive integer," imagine there is an infinite row of bins, labeled 1, 2, 3, and so on. We take a set and start placing members of the set into bins, with at most one member per bin. If we can find a way to assign all of the members to bins, then the set is countable. For example, consider the set of positive integers 2, 4, and so on. We can assign an integer $i$ to bin $i/2$ (if we are not skipping some bins, then we can assign even number $i$ to bin $i$). Thus, the set of even integers is countable. There will be no surprise, because intuitively there are "fewer" positive integers than positive integers, though both are infinite sets. But there are not really more positive integers than there are even integers, because we can uniquely assign even integer $i$ to positive integer by simply assigning positive integer $i$ to positive integer $2i$.

On the other hand, all integers are countable, even though this set appears to be "bigger" than the set of positive integers. We assign 0 to positive integer 1, -1 to positive integer 2, 3 to positive integer 4, -2 to positive integer 5, and so on. In general, assign positive integer $i$ to positive value $2i$, and negative integer value $-i$ to positive value $2i+1$. We will never run out of positive integers to assign, and we know exactly which positive integer is assigned to. Because every integer gets an assignment, the set of integers is countably infinite.

Are the number of programs countable or uncountable? A program can be viewed as a string of characters (including special punctuation, spaces, and line breaks). Let us consider the number of characters that can appear in a program $P$. (Using the ASCII character set, $P$ must be less than 128, but the actual number does not matter). If the number of strings is countable, then surely the number of programs is also countable. We can assign strings to the bins as Assign the null string to the first bin. Now, take all strings of one character, and assign them to the next $P$ bins in "alphabetic" or ASCII order. Next, take all strings of two characters, and assign them to the next $P^2$ bins, again in ASCII order working from left to right. Strings of three characters are likewise assigned to bins, strings of length four, and so on. In this way, a string of any given length can be assigned to some bin.

By this process, any string of finite length is assigned to some bin. So any program, which is merely a string of finite length, is assigned to some bin. Because all programs are assigned to some bin, the set of all programs is countable. Naturally most of the strings in the bins are not legal programs, but this is irrelevant. All that matters is that the strings that do correspond to programs are also in the bins.

Now we consider the number of possible functions. To keep things simple, assume that all functions take a single integer as input and yield a single integer as output. We will call such integer functions. A function is simply a mapping from input values to output values. Of course, not all programs literally take inputs and yield integers as output. However, everything that computers read and yield is essentially a series of numbers, which may be interpreted as letters or something else. Any useful computer program's input and output can be coded as integer values, so our simple model of computer input and output is simply general to cover all possible programs.

Now we see if it is possible to assign all of the integers to the infinite set of bins. If so, then the number of integers is countable, and it might be possible to assign every integer to a program. If the set of integer functions cannot be assigned to bins, then there will be integers that must have no corresponding program.

Imagine each integer function as a table with two columns and an infinite number of rows. The first column lists the positive integers starting at 1. The second column lists the output of the function when given the value in the first column as input. Thus, the table explicitly describes the mapping from input to output for each function. Each we call a function.

Next we try to assign function tables to bins. To do so we must order the functions, but it does not matter what we choose. For example, Bin 1 could store the function that always returns 1 regardless of the value of input. Bin 2 could store the function that returns its input. Bin 3 could store the function that doubles its input and adds 5. Bin 4 could store a function for which we can see no simple relationship between input and output. These four functions as assigned to the first four bins are in Figure 17.

Can we assign every to a bin? The answer is no, because there is always a way to create a new function that is not in any of the bins. Suppose somebody finds a way of assigning functions to bins that they claim includes all of the functions. We can build a new function that has not been assigned

> There is no requirement for a function to have any discernible relationship between input and output. A function is simply a mapping of inputs to outputs, with no constraint on how the mapping is determined.

| | $f_1(x)$ | $f_2(x)$ | $f_3(x)$ | $f_4(x)$ |
|---|---|---|---|---|
| 1 | 1 | 1 | 7 | 15 |
| 2 | 1 | 2 | 3 | 12 |
| 3 | 1 | 3 | 11 | 7 |
| 4 | 4 | 4 | 13 | 13 |
| 5 | 5 | 5 | 15 | 2 |
| 6 | 6 | 6 | 17 | 7 |

Figure 17.7 An illustration of assigning functions to bins.

| | $f_1(x)$ | $f_2(x)$ | $f_3(x)$ | $f_4(x)$ | $f_{new}(x)$ |
|---|---|---|---|---|
| 1 | 1 | 1 | 7 | 15 | 1 |
| 2 | 1 | 2 | 3 | 12 | 2 |
| 3 | 1 | 3 | 11 | 7 | 3 |
| 4 | 4 | 4 | 13 | 13 | 4 |
| 5 | 5 | 5 | 15 | 2 | 5 |
| 6 | 6 | 6 | 17 | 7 | 6 |

Figure 17.8 Illustration for the argument that the number of integer functions is uncountable. Because of the construction $F_{new}(i) = F_i(i) + 1$, the new function is different from any function $F_i$ at least at one $i$. This procedure is called **diagonalization**.

## 17.3 Impossible Problems

### 17.3.2 The Halting Problem Is Unsolvable

While there might be a intellectual appeal to knowing that there exists some function that cannot be computed by a computer program, does this mean that there is any useful function? After all, does it really matter if no program can compute a “nonsense” function as shown in Bin 4 of Figure 17.7? We will now prove that the Halting Problem cannot be computed by any computer program. The proof is by contradiction.

```
boolean halt(string prog, string input) {
    if (PROGRAM_HALTS(prog, input)) {
        return true;
    else
        return false;
}
```

```
// Return the reverse of what selfhalt returns on "prog"
void contrary(char *prog) {
    if (selfhalt(prog)) {
        while (true); // Go into an infinite loop
    }
}
```

What happens if we make a program whose sole purpose is to execute the function contrary and run that program with itself as input? One possibility is that the call to selfhalt returns true; selfhalt claims contrary will halt run on itself. In that case, contrary goes into an infinite loop (and thus does not halt). On the other hand, if selfhalt returns false, then halt is proclaiming that contrary does not halt on itself, and contrary returns,
