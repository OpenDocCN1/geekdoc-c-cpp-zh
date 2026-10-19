The sentinel technique can be applied to virtually any situation in which you use a linear search—to linked lists as well as arrays. The only caveats are that you must choose the sentinel value carefully and that you must be careful about how you put the sentinel value into the data structure.

# Putting the Busiest Loop on the Inside

When you have nested loops, think about which loop you want on the outside and which you want on the inside. Following is an example of a nested loop that can be improved:

```
Java Example of a Nested Loop That Can Be Improved
for ( column = 0; column < 100; column++ ) {
    for ( row = 0; row < 5; row++ ) {
        sum = sum + table[ row ][ column ];
    }
}
```

The key to improving the loop is that the outer loop executes much more often than the inner loop. Each time the loop executes, it has to initialize the loop index, increment it on each pass through the loop, and check it after each pass. The total number of loop executions is 100 for the outer loop and 100 * 5 = 500 for the inner loop, for a total of 600 iterations. By merely switching the inner and outer loops, you can change the total number of iterations to 5 for the outer loop and 5 * 100 = 500 for the inner loop, for a total of 505 iterations. Analytically, you'd expect to save about (600 – 505) / 600 = 16 percent by switching the loops. Here’s the measured difference in performance:

| Language | Straight Time | Code-Tuned Time | Time Savings |
|---|---|---|---|
| C++ | 4.75 | 3.19 | 33% |
| Java | 5.39 | 3.56 | 34% |
| PHP | 4.16 | 3.65 | 12% |
| Python | 3.48 | 3.33 | 4% |

The results vary significantly, which shows once again that you have to measure the effect in your particular environment before you can be sure your optimization will help.

# Strength Reduction

Reducing strength means replacing an expensive operation such as multiplication with a cheaper operation such as addition. Sometimes you'll have an expression inside a loop that depends on multiplying the loop index by a factor. Addition is usually faster than multiplication, and if you can compute the same number by adding the amount on each iteration of the loop rather than by multiplying, the code will typically run faster. Here’s an example of code that uses multiplication: