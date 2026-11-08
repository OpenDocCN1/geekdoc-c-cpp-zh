|  |  |
|---|---|
| Op: 2 [-1, -1, -1, 2, 0, 0, 0] | Op: 2 [1, 0, 6, 4, 5, 2, 3] |
| Op: 2 [-1, -1, -1, 2, 0, 0, 0] | Op: 2 [1, 2, 6, 4, 5, 0, 3] |
| Op: 3 [-1, -1, -1, -1, 0, 0, 0] | Op: 3 [0, 1, 2, 3, 4, 5, 6] |
| Op: 3 [-1, -1, -1, -1, 0, 0, 0] | Op: 3 [6, 1, 2, 3, 4, 5, 0] |
| Op: 3 [-1, -1, -1, -1, 0, 0, 0] | Op: 3 [6, 1, 2, 3, 4, 0, 5] |
| Op: 3 [-1, -1, -1, -1, 1, 1, 0] | Op: 3 [5, 6, 1, 2, 3, 0, 4] |
| Op: 3 [-1, -1, -1, -1, 2, 1, 0] | Op: 3 [5, 6, 1, 2, 0, 3, 4] |

# State table: 2

|  |  |
|---|---|
| Op: 0 [0, 0, -1, 0, -1, -1, -1] | Op: 0 [0, 1, 2, 3, 4, 5, 6] |
| Op: 0 [1, 0, -1, 0, -1, -1, -1] | Op: 0 [5, 1, 2, 3, 4, 0, 6] |
| Op: 0 [1, 0, -1, 0, -1, -1, -1] | Op: 0 [5, 1, 2, 0, 4, 3, 6] |
| Op: 0 [0, 0, -1, 0, -1, -1, -1] | Op: 0 [3, 6, 5, 0, 2, 1, 4] |
| Op: 0 [0, 0, -1, 0, -1, -1, -1] | Op: 0 [3, 0, 5, 6, 2, 1, 4] |
| Op: 1 [0, 0, 0, -1, 0, -1, -1] | Op: 1 [0, 1, 2, 3, 4, 5, 6] |
| Op: 1 [1, 0, 0, -1, 0, -1, -1] | Op: 1 [4, 1, 2, 3, 0, 5, 6] |
| Op: 1 [1, 0, 0, -1, 0, -1, -1] | Op: 1 [4, 0, 2, 3, 1, 5, 6] |
| Op: 1 [0, 0, 0, -1, 0, -1, -1] | Op: 1 [1, 0, 6, 4, 5, 2, 3] |
| Op: 1 [1, 0, 0, -1, 0, -1, -1] | Op: 1 [1, 2, 6, 4, 5, 0, 3] |
| Op: 2 [-1, -1, -1, 0, 0, 0, 0] | Op: 2 [0, 1, 2, 3, 4, 5, 6] |
| Op: 2 [-1, -1, -1, 0, 0, 0, 0] | Op: 2 [0, 1, 2, 3, 4, 5, 6] |
| Op: 2 [-1, -1, -1, 0, 0, 0, 0] | Op: 2 [0, 1, 2, 3, 4, 5, 6] |
| Op: 2 [-1, -1, -1, 1, 0, 0, 2] | Op: 2 [0, 1, 2, 3, 4, 5, 6] |
| Op: 2 [-1, -1, -1, 1, 0, 0, 0] | Op: 2 [0, 1, 2, 3, 4, 5, 6] |
| Op: 3 [-1, -1, -1, -1, 0, 0, 0] | Op: 3 [0, 1, 2, 3, 4, 5, 6] |
| Op: 3 [-1, -1, -1, -1, 0, 0, 0] | Op: 3 [5, 1, 2, 3, 4, 0, 6] |
| Op: 3 [-1, -1, -1, -1, 0, 0, 0] | Op: 3 [5, 1, 2, 0, 4, 3, 6] |
| Op: 3 [-1, -1, -1, -1, 1, 0, 0] | Op: 3 [3, 6, 5, 0, 2, 1, 4] |
| Op: 3 [-1, -1, -1, -1, 2, 0, 0] | Op: 3 [3, 0, 5, 6, 2, 1, 4] |

Fig. 4. CA changes for the 10 consecutive states

The numbers in the left column of the tables stand for the number of the machine in a group, and their indexes (i.e. allocation in the table) are the numbers of the parts. The numbers in the right column of the tables stand for the sequence of individual parts in a given operation and their indexes (i.e. allocation in the table) are the numbers of the parts. Value (-1) in the left column of the tables stands for lack of machine participation in a given operation with a given part. Value (-1) in the right column would stand for lack of processing of a part in a given operation. All the (-1) values are ignored in the state change