```
456$$$$$$$$$$
23.455*********
Manipulator&&&&
====================
DEMO FINISH
=====================
```

# EXPLANATION : The following cout statement

```
cout << setfill('$') << setw(15) << setiosflags(ios :: left)
    << x << endl;
```

Sets the width 15, setfill character to ‘$’ and sets the output left justified which causes value of x to be printed.

![](bbox=[0.17, 0.4, 0.83, 0.54])

Figure 11.15. Implementation of built in manipulator

The next cout statement is given as :

```
cout << setfill('*') << setw(15) << setiosflags(ios :: left)
    << setprecision(3) << y << endl;
```

![](bbox=[0.17, 0.67, 0.83, 0.81])

Figure 11.16. Demo of setprecision and setiosflags (ios :: left)

The next cout statement