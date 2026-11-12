# FIGURE 2-9 Box trace of writeBackward2("cat") in pseudocode

The initial call is made, and the function begins execution:

![](bbox=[0.11, 0.16, 0.23, 0.19])

Output stream:

Enter writeBackward2 with string: cat

Point A is reached, and the recursive call is made. The new invocation begins execution:

![](bbox=[0.11, 0.28, 0.39, 0.31])

Output stream:

Enter writeBackward2 with string: cat
Enter writeBackward2 with string: at

Point A is reached, and the recursive call is made. The new invocation begins execution:

![](bbox=[0.11, 0.42, 0.57, 0.45])

Output stream:

Enter writeBackward2 with string: cat
Enter writeBackward2 with string: at
Enter writeBackward2 with string: t

Point A is reached, and the recursive call is made. The new invocation begins execution:

![](bbox=[0.11, 0.57, 0.72, 0.6])

This invocation completes execution, and a return is made.

Output stream:

Enter writeBackward2 with string: cat
Enter writeBackward2 with string: at
Enter writeBackward2 with string: t
Enter writeBackward2 with string:
Leave writeBackward2 with string:

![](bbox=[0.11, 0.76, 0.72, 0.79])

This invocation completes execution, and a return is made.

Output stream:

Enter writeBackward2 with string: cat
Enter writeBackward2 with string: at
Enter writeBackward2 with string: t