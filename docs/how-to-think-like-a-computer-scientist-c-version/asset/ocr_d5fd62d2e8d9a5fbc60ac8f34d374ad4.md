# 4.7. RECURSION

For example, look at the following function:

```
void countdown (int n) {
  if (n == 0) {
    cout << "Blastoff!" << endl;
  } else {
    cout << n << endl;
    countdown(n-1);
  }
}
```

The name of the function is countdown and it takes a single integer as a parameter. If the parameter is zero, it outputs the word "Blastoff!" Otherwise, it outputs the parameter and then calls a function named countdown—itself—passing n-1 as an argument.

What happens if we call this function like this:

```
void main () {
  countdown(3);
}
```

The execution of countdown begins with n=3, and since n is not zero, it outputs the value 3, and then calls itself...

The execution of countdown begins with n=2, and since n is not zero, it outputs the value 2, and then calls itself...

The execution of countdown begins with n=1, and since n is not zero, it outputs the value 1, and then calls itself...

The execution of countdown begins with n=0, and since n is zero, it outputs the word "Blastoff!" and returns.

The countdown that got n=1 returns.

The countdown that got n=2 returns.

The countdown that got n=3 returns.

And you're back in main (what a trip). So the total output looks like:

+   3
2
1
Blastoff!

As a second example, let's look again at the functions newLine and threeLine.