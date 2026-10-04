# Chapter 12 679

One unique feature of pointers is offsets can be included in expressions using pointers. For example, the  in the expression * (gPtr + 1) is an offset. The expression represents the integer that goes beyond the variable pointed to by gPtr. Similarly, as illustrated in Figure 12.12, the expression * (gPtr + 3) references the variable that three integers beyond the variable pointed to gPtr: the variable grade[3].

![](bbox=[0.223, 0.215, 0.776, 0.378])

Figure 12.12 shows the correspondence between elements referenced by subscripts and by pointers and offsets. Figure 12.13 illustrates the relationships listed in Table 12.1.

# Table 12.1 Array Elements Can Be Referenced in Two Ways

| Array Element | Subscript Notation | Pointer Notation |
|---|---|--|
| Element 0 | grade[0] | *gPtr or (gPtr + 0) |
| Element 1 | grade[1] | *(gPtr + 1) |
| Element 2 | grade[2] | *(gPtr + 2) |
| Element 3 | grade[3] | *(gPtr + 3) |
| Element 4 | grade[4] | *(gPtr + 4) |

![](bbox=[0.223, 0.646, 0.776, 0.853])

Figure 12.13 The relationship between array elements and pointers