# # Chapter 13

Arrays of Structures

| Employee Number | Employee Name | Employee Pay Rate |
|---|---|--|
| 1st structure | 32479 | Abrams, B. | 6.72 |
| 2nd structure | 33623 | Bohm, P. | 7.54 |
| 3rd structure | 34145 | Donaldson, S. | 5.56 |
| 4th structure | 35987 | Ernst, T. | 5.43 |
| 5th structure | 36203 | Gwozd, K. | 8.72 |
| 6th structure | 38417 | Hanson, H. | 7.64 |
| 7th structure | 37634 | Monroe, G. | 5.29 |
| 8th structure | 38321 | Price, S. | 9.67 |
| 9th structure | 39435 | Robbins, L. | 8.50 |
| 10th structure | 39567 | Williams, B. | 7.20 |

**Figure 13.2** A list of structures

Declaring an array of structures is the same as declaring an array of any other variable. For example, if the data type PayRec is declared as

```
struct PayRec {int idnum; string name; double rate;};
```

then an array of 10 such structures can be defined as follows:

```
PayRec employee[10];
```

This definition statement constructs an array of 10 elements, and each element is a structure of the data type PayRec. Notice that creating an array of 10 structures has the same form as creating any other array. For example, creating an array of 10 integers named employee requires the following declaration:

```
int employee[10];
```

In this declaration, the data type is integer, and in the previous declaration for employee, the data type is PayRec.
After an array of structures, a data item is referenced by the position of its structure in the array, followed by a period and the structure member. For example, the variable employee[0].rate references the rate member of the first employee structure in the employee array. Including structures as elements of an array permits processing a list of structures by using standard array programming techniques. Program 13.3 displays the first five employee records in Figure 13.2.