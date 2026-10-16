characterizes sequential execution and indicates clearly that the statements are executed in the order in which they are given with each statement being executed exactly once.

![](bbox=[0.38, 0.17, 0.62, 0.52])

Although sequence is a fundamental control structure, it is not powerful enough to solve all problems. Some problems require selecting one of several alternative actions, which means that programs for solving them will need a selection structure. In this chapter we will consider one selection structure that C++ provides: the if statement. Another, the switch statement, is described in Chapter 8.

For some problems, however, another control structure besides sequence and selection is needed, one that makes it possible to execute one or more statements repeatedly—a repetition structure. We will consider two such repetition structures provided in C++, the for and while statements, in the last part of this chapter.

Sequence, selection, and repetition are the only control structures needed. A fundamental result of theoretical computer science states that any problem solvable by a computer program can be solved by one that is made up of sequence, selection, and repetition structures.¹

# 5.1 INTRODUCTORY EXAMPLE: AIR QUALITY INDEX (AQI)

# 5.1.2 Problem

Pollution levels are measured at three locations in a city and the Air Quality Index (AQI), also known as the Air-Pollution Index (API), is the integer average of these three readings. An index of less than 50 parts per million indicates a safe condition, whereas indexes of 50 parts per million or greater indicate a hazardous condition.² The city’s environmental

> ¹ This theorem is usually credited to a 1966 paper by Corrado Böhm and Giuseppe Jacopini.

> ² Here we are considering a simplified AQI that has only two categories, but in practice, there are usually more than two. For example, as we will see in Chapter 8 where we consider selection structures with more than two alternatives, there are 6 categories for the United States AQI.