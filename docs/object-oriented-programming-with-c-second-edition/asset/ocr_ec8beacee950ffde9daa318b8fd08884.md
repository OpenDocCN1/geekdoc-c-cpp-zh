# Data Structures 327

| | |
| :--- | :--- |
| 325 | val |
| 7912 | next |

| | |
| :--- | :--- |
| 5287 | val |
| NULL | next |

Figure 9.42 The structure of the list prior to the delBeg() function

The delBeg() function has been called at this point in the program. At the end of its execution, we will expect the list to look like Figure 9.43.

| | |
| :--- | :--- |
| 5287 | val |
| NULL | next |

| | |
| :--- | :--- |
| 7912 | list1 |

Figure 9.43 Expected effect of the delBeg() function

Let us review the function and see whether it has been defined correctly or not. When the delBeg() function starts, the expression of the if statement gets evaluated. It checks the value of the head pointer is NULL or not. At this point, the value of the head pointer is 320 (points at first of two nodes that are currently in the list). Therefore, the test expression returns true and the if block executes.

The first statement in the if block declares a temporary pointer and copies the value of the head pointer to it. Figure 9.44 depicts the resulting situation.

| | |
| :--- | :--- |
| 325 | val |
| 7912 | next |

| | |
| :--- | :--- |
| 5287 | val |
| NULL | next |

Figure 9.44 Making a temporary pointer point at the node to be deleted