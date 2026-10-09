Suppose you label the rows with indices $i \in \{0, 1, 2, 3\}$ and the columns with indices $j \in \{0, 1, 2, 3\}$—then the entry at $(i, j)$ is $4i + j$. It is obvious how this formula generalises to higher dimensional data structures than matrices.

Let’s repeat the exercise where we now count from 1. We would label the entries of the matrix as:

![](bbox=[0.368, 0.212, 0.64, 0.289])

We now label the rows with indices $i' \in \{1, 2, 3, 4\}$ and similarly label the columns with $j' \in \{1, 2, 3, 4\}$. The entry at $(i, j)$ is now $4(i' - 1) + (j' - 1) + 1 = 4i' + j' - 3$. This is a much less elegant formula than before and it doesn’t generalise as straightforwardly to higher dimensions.

Note that there is another kind of **for** loop in C++, which has a simpler syntax but which is compensatingly less flexible. See Chapter 18 for details.

# 4.4 break, continue, return

In the middle of a loop, you can decide that you want to jump out of the loop and start executing the statements after the loop using the **break** keyword.

For example, this code keeps adding up the numbers typed by the user until they enter a negative number. At this point, the software prints out the total of the positive numbers.

```
```
cout << "Enter positive numbers followed ";
cout << "by a negative number to quit\n";
int total = 0;
while (true) {
    int next;
    cin >> next;
    if (next < 0) {
        break;
    }
    total += next;
}
cout << "The total is " << total << "\n";
```
```

The **continue** keyword means skip the rest of the code in the body of the