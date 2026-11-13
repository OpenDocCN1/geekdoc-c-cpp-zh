primary indexing.

| Primary key Value | Block Pointer |
|---|---|
| R1 | |
| R2 | |
| R3 | |
| R4 | |
| R5 | |
| R6 | |
| R7 | |
| R8 | |

| Student_Roll | Student_Name | Student_Dept |
|---|---|---|
| R1 | Rahul | Information Technology |
| R2 | Smita | Computer Science |
| R3 | Ajay | Electrical Engineering |
| R4 | Raj | Information Technology |
| R5 | Vikas | Information Technology |
| R6 | Bina | Computer Science |
| R7 | Puja | Electrical Engineering |
| R8 | Amit | Computer Science |

# Figure 12.3: Dense Primary Index

In the figure 12.3, the dense primary index is explained. In dense primary index, all primary key values are present in the index file. Each record of relation is pointed by each block pointer.

| Primary key Value | Block Pointer |
|---|---|
| R1 | |
| R4 | |
| R7 | |

| Student_Roll | Student_Name | Student_Dept |
|---|---|---|
| R1 | Rahul | Information Technology |
| R2 | Smita | Computer Science |
| R3 | Ajay | Electrical Engineering |
| R4 | Raj | Information Technology |
| R5 | Vikas | Information Technology |
| R6 | Bina | Computer Science |
| R7 | Puja | Electrical Engineering |
| R8 | Amit | Computer Science |

# Figure 12.4: Sparse Primary Index