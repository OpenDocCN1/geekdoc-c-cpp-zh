The output from the TABULATE procedure isn’t included. (Don’t complain. Didn’t you get enough of this data set in Chapter 4?)

# Display 8.28 Output from PROC PRINT for the first four observations from the nitrophen_A data set

| Animal | conc | brood | Count |
|---|---|---|---|
| 1 | 0 | 1 | 3 |
| 1 | 0 | 2 | 14 |
| 1 | 0 | 3 | 10 |
| 2 | 0 | 1 | 5 |
| 2 | 0 | 2 | 12 |
| 2 | 0 | 3 | 15 |
| 3 | 0 | 1 | 6 |
| 3 | 0 | 2 | 11 |
| 3 | 0 | 3 | 17 |
| 4 | 0 | 1 | 6 |
| 4 | 0 | 2 | 12 |
| 4 | 0 | 3 | 15 |

# 8.6 Structured Thinking about Writing Programs

Homework problems are frequently simple, and if a computer program is required for analysis, then this program might need only a few lines of code to implement a solution. These small programs can be written on the fly without a great deal of planning. This strategy of short and quick program construction fails miserably when you are faced with larger problems and when alternative solutions are required. A basic strategy is advocated in this case: modularize your code and write pseudocode that is operationalized as functioning programming statements during implementation. This strategy is outlined in this section and illustrated in the case studies that follow.

Modular programming is commonly introduced in computer science when basic programming skills are taught. The basic idea is a simple one—when faced with a large and complex task, subdivide this task into smaller components. These smaller components can be implemented and tested before they are combined in a larger program. Often, these