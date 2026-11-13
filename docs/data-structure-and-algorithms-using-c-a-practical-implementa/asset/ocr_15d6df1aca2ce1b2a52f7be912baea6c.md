PUSH(145)
"OVERFLOW"
(top = size -1 Condition for OVERFLOW)

POP
| 5 | 25 | 53 | 78 | |
|---|---|---|---|---|
| 0 | 1 | 2 | 3 | 4 |
top = 3

POP
| 5 | 25 | 53 | | |
|---|---|---|---|---|
| 0 | 1 | 2 | 3 | 4 |
top = 2

POP
| 5 | 25 | | | |
|---|---|---|---|---|
| 0 | 1 | 2 | 3 | 4 |
top = 1

POP
| 5 | | | | |
|---|---|---|---|---|
| 0 | 1 | 2 | 3 | 4 |
top = 0

POP
| | | | | |
|---|---|---|---|---|
| 0 | 1 | 2 | 3 | 4 |
top = -1

POP
"UNDERFLOW"
(top = -1 Condition for UNDERFLOW)

# 5.3 ALGORITHMS

# ALGORITHM FOR PUSH OPERATION

```
PUSH(STACK[SIZE], NO, TOP)       [STACK[SIZE] is the Stack]
                                         [NO is the Number to Insert]
                                         [Top is the position of the stack]
STEP-1 : IF (TOP = SIZE - 1) THEN :
               WRITE : 'OVERFLOW'
               RETURN
[END OF IF]
```