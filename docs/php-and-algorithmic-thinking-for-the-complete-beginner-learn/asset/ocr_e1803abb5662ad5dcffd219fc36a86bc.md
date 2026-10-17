```
echo "Pi ~ ", $pi;
?>
```

> Notice: Please note the way in which variable $sign toggles between the values -1 and +1 in each iteration.

If you reduce the value of the constant ACCURACY, π will be calculated more and more accurately. Depending on how fast your computer is, you can calculate the first six digits of π fairly quickly. However, the time it takes to calculate each succeeding digit of π goes up exponentially. To calculate 30 digits of π on a modern computer using this method could take years!

# Exercise 31.4-9 Approximating a Real with a Fraction

Write a PHP script that prompts the user to enter a real between 1 and 100 and then tries to find the fraction N/M that better approximates it, where N is an integer between 0 and 100 and M is an integer between 1 and 100. Moreover, the script should validate data input, allowing the user to enter only numeric values between 0 and 100. There is no need to display any error messages.

# Solution

The solution is simple. All you need to do is iterate through all possible combinations of variables $n and $m and check which one better approximates the real given.

To iterate through all possible combinations of variables $n and $m, you can use a nested loop control structure, that is, two counted loop structures, one nested within the other, as follows.

```
for ($n = 0; $n <= 100; $n++) {
for ($m = 1; $m <= 100; $m++)
...
}
}
```

> Notice: The total number of iterations is 101 × 100 = 10100. Quite a big number but, for a modern computer, this is peanuts!

The following criteria

minimum of (|N/M − real given|)

can evaluate how “good” an approximation is.

Confused? Let’s try to approximate the value 0.333 with a fraction, iterating through all possible combinations of N and M.

+   ➤ For N = 1, M = 1 the criteria equals to |1/1 − 0.333| = 0.6670