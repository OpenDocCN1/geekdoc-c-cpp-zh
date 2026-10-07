114 Learning SAS by Example: A Programmer's Guide, Second Edition

# Program 8.14: Demonstrating that DO UNTIL Loop Always Executes at Least Once

```
data Double;
  Interest = .0375;
  Total = 300;
  do until (Total gt 200);
    Year + 1;
    Total = Total + Interest*Total;
    output;
  end;
  format Total dollar10.2;
run;

proc print data=double noobs;
  title "Listing of Double";
run;
```

The condition is true even before the loop starts, but because the condition is tested at the bottom of the loop, this program outputs one observation (as shown here):

Figure 8.11: Output from Program 8.14

![](bbox=[0.095, 0.427, 0.303, 0.529])

An alternative to DO UNTIL is DO WHILE. As you might expect, a DO WHILE loop iterates as long as the condition following WHILE is true. There is no difference between DO WHILE and DO UNTIL—the WHILE condition is tested at the top of the loop rather than at the bottom.

Unlike a DO UNTIL block that always iterates at least once, a DO WHILE block does not execute even if the condition is false. You can rewrite Program 8.13 using a DO WHILE statement, like this:

# Program 8.15: Demonstrating a DO WHILE Statement

```
data Double;
  Interest = .0375;
  Total = 100;
  do while (Total le 200);
    Year + 1;
    Total = Total + Interest*Total;
    output;
  end;
  format Total dollar10.2;
run;

proc print data=double noobs;
  title "Listing of Double";
run;
```