![](bbox=[0.055, 0.095, 0.86, 0.236])

**FIGURE 7.19:** Basic Structure of the Three-rule Washing Machine

+   - IF amount_of_dirt is More AND type_of_dirt is Greasy THEN washing_time is Too_Long
+     item IF amount_of_dirt is Medium AND type_of_dirt is Greasy THEN washing_time is Long
+   - IF amount_of_dirt is Less AND type_of_dirt is Greasy THEN washing_time is Long
+   - IF amount_of_dirt is More AND type_of_dirt is Medium THEN washing_time is Long
+   - IF amount_of_dirt is Medium AND type_of_dirt is Medium THEN washing_time is Medium
+   - IF amount_of_dirt is Less AND type_of_dirt is Medium THEN washing_time is Medium
+   - IF amount_of_dirt is More AND type_of_dirt is Non_Greasy THEN washing_time is Medium
+   - IF amount_of_dirt is Medium AND type_of_dirt is Non_Greasy THEN washing_time is Short
+   - IF amount_of_dirt is Less AND type_of_dirt is Non_Greasy THEN washing_time is Too_Short

For simplicity we consider three rules and the basic structure of the three-rule with two-input, one-output, is shown in Figure 7.19.

All the information streams from left to right, that is from two inputs to a single output. The rules of fuzzy logic systems are parallel processed. Rather than sharp flipping between manners based on breakpoints, we will glide smoothly from areas where the system’s behavior is dominated by either one rule or another.