# Compare Performance of Similar Logic Structures

The test described above could be performed using either a case statement or if-then-elses. Depending on the environment, either approach might work better. Here is the data from the preceding two tables reformatted to present the “code-tuned” times comparing if-then-else and case performance:

| Language | case | if-then-else | Time Savings | Performance Ratio |
|---|---|---|---|---|
| C# | 0.260 | 0.330 | -27% | 1:1 |
| Java | 2.56 | 0.460 | 82% | 6:1 |
| Visual Basic | 0.260 | 1.00 | 258% | 1:4 |

These results defy any logical explanation. In one of the languages, case is dramatically superior to if-then-else, and in another, if-then-else is dramatically superior to case. In the third language, the difference is relatively small. You might think that because C# and Java share similar syntax for case statements, their results would be similar, but in fact their results are opposite each other.

This example clearly illustrates the difficulty of performing any sort of “rule of thumb” or “logic” to code tuning—there is simply no reliable substitute for measuring results.

# Substitute Table Lookups for Complicated Expressions

Cross-Reference For details on using table lookups to replace complicated logic, see Chapter 18, “Table-Driven Methods.”

In some circumstance, a table lookup might be quicker than traversing a complicated chain of logic. The point of a complicated chain is usually to categorize something and then to take an action based on its category. As an abstract example, suppose you want to assign a category number to something based on which of three groups—Groups A, B, and C—it falls into:

![](bbox=[0.22, 0.68, 0.45, 0.8])