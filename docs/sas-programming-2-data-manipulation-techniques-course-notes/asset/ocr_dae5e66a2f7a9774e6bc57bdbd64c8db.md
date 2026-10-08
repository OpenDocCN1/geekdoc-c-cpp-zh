# 3.04 Multiple Answer Poll – Correct Answer

What must happen in the DATA step to summarize data by groups? (Circle all that apply.)

+   a Sort the input data.
b. Set the accumulating variable to zero at the start of each BY group.
c. Increment the accumulating variable.
d. Output only the last observation of each BY group.

Choice a. does not apply because sorting is done with PROC SORT, not in the DATA step.

# 3.05 Short Answer Poll – Correct Answer

What are the values for First. and Last. variables when the DATA step is processing the observation indicated by the arrow?

| Proj | Dept | First.Proj |
|---|---|---|
| A | ADMIN | 0 |
| A | ADMIN | First.Dept 0 |
| A | ADMIN | |
| B | ADMIN | |
| B | ENGINR | Last.Proj 1 |
| B | ENGINR | |
| C | ENGINR | |
| C | SALES | Last.Dept 1 |
| C | SALES | |