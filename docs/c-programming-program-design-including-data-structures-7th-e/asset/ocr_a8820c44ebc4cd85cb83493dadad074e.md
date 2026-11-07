22. Suppose that score is an int variable. Consider the following if statements: (3)

+   i.
+           if (score == 70)
+               cout << "Grade is C." << endl;
+   ii.
+           if (score = 70)
+               cout << "Grade is C." << endl;

Answer the following questions:

+   a. What is the output in (i) and (ii) if the value of score is 70? What is the value of score after the if statement executes?
+   b. What is the output in (i) and (ii) if the value of score is 80? What is the value of score after the if statement executes?

23. Rewrite the following expressions using the conditional operator. (Assume that all variables are declared properly.) (9)

+   a.
+           if (x >= y)
+               z = x - y;
+           else
+               z = y - x;
+   b.
+           if (hours >= 40.0)
+               wages = 40 * 7.50 + 1.5 * 7.5 * (hours - 40);
+           else
+               wages = hours * 7.50;
+   c.
+           if (score >= 60)
+               str = "pass";
+           else
+               str = "Fail";

24. Rewrite the following expressions using an if...else statement. (Assume that all variables are declared properly.) (9)

+   a. `(x < 5) ? y = 10 : y = 20;`
+   b. `(fuel >= 10) ? drive = 150 : drive = 30;`
+   c. `(booksBought >= 3) ? discount = 0.15 : discount = 0.0;`

25. Suppose that you have the following conditional expression. (Assume that all the variables are properly declared.) (9)

```
        (0 < backyard && backyard <= 5000) ? fertilizingCharges = 40.00
            : fertilizingCharges = 40.00 + (backyard - 5000) * 0.01;
```

+   a. What is the value of fertilizingCharges if the value of backyard is 3000?
+   b. What is the value of fertilizingCharges if the value of backyard is 5000?
+   c. What is the value of fertilizingCharges if the value of backyard is 65000?