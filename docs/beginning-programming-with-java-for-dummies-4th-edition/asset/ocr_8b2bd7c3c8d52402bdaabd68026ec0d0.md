Figure 7-10 shows a close-up view of the postincrement operator's action. In Figure 7-10, the computer encounters the System.out.println(gumballs++) statement. First, the computer executes System.out.println, using the old value of gumballs (28). Then the computer adds 1 to gumballs (raising the value of gumballs to 29).

# Figure 7-10: The postincrement operator in action.

![](bbox=[0.25, 0.28, 0.82, 0.55])

Look at the bold line of code in Figure 7-11. The computer prints the old value of gumballs (28) on the screen. Only after printing this old value does the computer add 1 to gumballs (raising the gumballs value from 28 to 29).

# Figure 7-11: Using postincrement.

![](bbox=[0.25, 0.65, 0.82, 0.9])

```
class AddEvenMoreGumballs { public static void main(String args[]) { int gumballs=27; gumballs++; System.out.println(gumballs); System.out.println(gumballs++); System.out.println(gumballs); } }
```

# REMEMBER

With System.out.println(gumballs++), the computer adds 1 to gumballs after printing the old value that gumballs already had.