```
printf("Amount to be paid after discount of %0.2f(%)",f_discount*100);
printf(" is %0.2f\n", f_payment);
return;
}
/* End of main function */
```

# Output 1:

Enter premium: 25000
Had accident last year Y/y for yes: Y
Enter gender F/f for Female: F
Amount to be paid after discount of 0.00(%) is 25000.00

# Output 2:

Enter premium: 15000
Had accident last year Y/y for yes: N
Enter gender F/f for Female: F
Amount to be paid after discount of 35.00(%) is 9750.00

Program 7 was designed to calculate the premium to be paid to an insurance company based on certain criteria. Figure 6 shows the problem of dangling else problem and its solution.

![](bbox=[0.35, 0.58, 0.78, 0.73])

▲ Figure 6: Dangling Else Statement

It can be observed in Figure 6 that the use of scope removes the problem of dangling else. In most cases, the user has to be careful and avoid dangling else by using proper scope of statements.

For small set of available alternatives, the two-way selections work fine. As the number of alternatives increases, the use of two-way selection becomes complex. If we have more number of alternatives, then we have to go for multiway selection. The next subsection discusses how multiway selection is implemented in C.