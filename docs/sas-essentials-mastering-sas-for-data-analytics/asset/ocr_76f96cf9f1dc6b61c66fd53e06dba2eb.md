# 10

# ANALYZING COUNTS AND TABLES

# LEARNING OBJECTIVES

+   - To be able to use PROC FREQ to create one-way frequency tables
- To be able to use PROC FREQ to create two-way (cross-tabulation) tables
- To be able to use two-by-two contingency tables to calculate relative risk measures
- To be able to use Cohen's kappa to calculate inter-rater reliability

Data that are collected as counts require a specific type of treatment. It doesn't make sense to calculate means and standard deviations on this type of data. Instead, categorical data (also called qualitative data) are often analyzed using frequency and cross-tabulation tables. The primary procedure within SAS® for this type of analysis is PROC FREQ.

# 10.1 USING PROC FREQ

PROC FREQ is a multipurpose SAS procedure for analyzing count data. It can be used to obtain frequency counts for one or more individual variables or to create two-way tables (cross-tabulations) from two variables.(Tables using three variables are discussed later in the chapter.)

PROC FREQ can also be used to perform statistical tests on count data. The syntax for PROC FREQ and commonly used options and statements that are discussed in this chapter is as follows: