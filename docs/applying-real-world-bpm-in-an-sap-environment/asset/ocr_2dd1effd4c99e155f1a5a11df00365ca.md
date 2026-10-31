The action is the "Then" part of a rule. These are the steps to be taken when a rule is satisfied. There are six types of actions: assert, assign, execute, reevaluate, retract, and evaluate decision table. Whereas execute and assign relate to the application, assert, retract, and reevaluate affect the way other rules are evaluated. Figure 14.42 shows the rule Approve Platinum Card with a condition (If) and action (Then).

![](bbox=[0.18, 0.3, 0.88, 0.7])

Figure 14.42 A Rule in the Rule Composer

# Decision Tables

A decision table is a tabular representation of related rules. Instead of maintaining a list of rules with conditions and actions operating on the same definitions, the rules are better converted into a decision table. Figure 14.43 shows a decision table with many eligibility rules. Instead of the well-organized tabular format, the rules could also be written with the condition and action pattern such as:

+   - "If Credit History of Application is GOOD and Annual Income of Applicant <50000 and Total Assets of Applicant <100000 Then Credit Score = 42"