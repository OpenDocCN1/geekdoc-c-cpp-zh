# Figure 10-17 Fields in a record

| Record |
|---|---|---|
| Ingrid Virgo | 4587 | Engineering |

Name field\ID number field\Department field

# # Writing Records

In pseudocode, we will write an entire record using a single Write statement. For example, assume the variables name, idnumber, and department contain data about an employee, and employeeFile is the file we will write the data to. We can write the contents of these variables to the file with the following statement:

Write employeeFile name, idNumber, department
In the statement we simply listed the variables, separated by commas, after the file's internal name. The pseudocode in Program 10-7 shows how this statement might be used in a complete program.

# Program 10-7

```
1 // Variables for the fields
2 Declare String name
3 Declare Integer idNumber
4 Declare String department
5
6 // A variable for the number of employee records.
7 Declare Integer numEmployees
8
9 // A counter variable for the loop
10 Declare Integer counter
11
12 // Declare an output file.
13 Declare OutputFile employeeFile
14
15 // Get the number of employees.
16 Display "How many employee records do "
17 "you want to create?"
18 Input numEmployees
19
20 // Open a file named employees.dat.
21 Open employeeFile "employees.dat"
22
23 // Get each employee's data and write it
24 // to the file.
```