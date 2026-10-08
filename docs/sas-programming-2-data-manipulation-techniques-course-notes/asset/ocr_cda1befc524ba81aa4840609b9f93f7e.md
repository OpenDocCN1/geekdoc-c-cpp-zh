# 3.2 Accumulating Totals for a Group of Data

# Business Scenario

Each employee listed in orion.projsals is assigned to a special project. A business analyst would like to see the salary totals from each department for each special project.

# Partial orion.projsals

| Employee ID | Salary | Proj | Dept |
|---|---|---|--|
| 110004 | 42000 | EZ | HUMRES |
| 110009 | 34000 | WIN | ENGINR |
| 110011 | 27000 | WIN | FINANC |
| 110036 | 20000 | WIN | ENGINR |
| 110037 | 19000 | EZ | ENGINR |
| 110045 | 19000 | EZ | FINANC |
| 110077 | 27000 | CAP1 | ADMIN |
| 110097 | 20000 | EZ | ADMIN |
| 110107 | 31000 | EZ | ENGINR |

# Business Scenario: Desired Output

Create a new data set, pdsals, that shows the number of employees and salary totals from each department for each special project.

# Partial pdsals

| Proj | Dept | Sal | Num Emps |
|---|---|---|--|
| CAP1 | ADMIN | 70000 | 2 |
| EZ | HUMRES | 80000 | 3 |
| EZ | ENGINR | 109000 | 4 |
| EZ | FINANC | 122000 | 3 |
| EZ | HUMRES | 178000 | 5 |
| NGEN | ADMIN | 37000 | 2 |