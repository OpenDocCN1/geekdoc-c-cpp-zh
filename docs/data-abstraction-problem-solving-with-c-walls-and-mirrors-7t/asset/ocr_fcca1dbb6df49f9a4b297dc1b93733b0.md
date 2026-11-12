# FIGURE 2-9 Box trace of writeBackward2("cat") in pseudocode

The initial call is made, and the function begins execution:

![](bbox=[0.113, 0.164, 0.242, 0.184])

Output stream:

Enter writeBackward2 with string: cat

Point A is reached, and the recursive call is made. The new invocation begins execution:

![](bbox=[0.113, 0.286, 0.393, 0.312])

Output stream:

Enter writeBackward2 with string: cat
Enter writeBackward2 with string: at

Point A is reached, and the recursive call is made. The new invocation begins execution:

![](bbox=[0.113, 0.435, 0.574, 0.456])

Output stream:

Enter writeBackward2 with string: cat
Enter writeBackward2 with string: at
Enter writeBackward2 with string: t

Point A is reached, and the recursive call is made. The new invocation begins execution:

![](bbox=[0.113, 0.58, 0.726, 0.601])

This invocation completes execution, and a return is made.

Output stream:

Enter writeBackward2 with string: cat
Enter writeBackward2 with string: at
Enter writeBackward2 with string: t
Enter writeBackward2 with string: 
Leave writeBackward2 with string:

![](bbox=[0.113, 0.764, 0.726, 0.795])

This invocation completes execution, and a return is made.

Output stream:

Enter writeBackward2 with string: cat
Enter writeBackward2 with string: at
Enter writeBackward2 with string: t