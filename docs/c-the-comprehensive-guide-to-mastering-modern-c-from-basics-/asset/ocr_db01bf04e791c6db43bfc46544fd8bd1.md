# 3 C++ FOR NEWCOMERS

This chapter is primarily aimed at those transitioning from Java or C#, but newcomers from other higher-level languages, especially object-oriented languages, will also benefit, as will those refreshing their C++ skills after some time. I provide a general overview of the idiosyncrasies of C++ that may surprise or pose difficulties for newcomers.

All other readers can skip this chapter; the overview and introduction follow.

The following elements are ones that many developers should recognize:

+   * Statements
  Programs are executed statement by statement, after the other—at least per thread, at least in the model. The rule of thumb is that semicolons separate statements from each other. Statements can be combined into blocks.

+   * Expressions
  An expression recursively consists of expressions down to indivisible units such as literals or variables. Arithmetic expressions contain mathematical