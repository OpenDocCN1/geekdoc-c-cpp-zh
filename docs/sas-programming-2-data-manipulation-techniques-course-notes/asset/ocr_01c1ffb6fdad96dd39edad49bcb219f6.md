# Solutions to Student Activities (Polls/Quizzes)

# 10.01 Multiple Choice Poll – Correct Answer

Which program should be more efficient?

+   a. Program 1
b. Program 2
c. They should be equally efficient.

+   - The RETAIN statement assigns an initial value at compilation time.
- The RENAME= option renames the variables in the new data set at compilation time.

# Using the NOFMTERR System Option

By default, the FMTERR system option is in effect. If you use a format that SAS cannot load, SAS issues an error message and stops processing the step.

To prevent the default action, change the system option FMTERR to NOFMTERR.

```
OPTIONS FMTERR | NOFMTERR;
```