![](bbox=[0.186, 0.102, 0.912, 0.619])

**FIGURE 14-31**  Use the Query Builder to modify the SelectCommand CommandText

You could type the SQL statement shown in Example 14-27 in the **Query Builder SQL** pane or select the additional fields from the Department table to be displayed using the **Diagram** pane. The SQL statement shown in Figure 14-31 looks slightly different from what is shown in Example 14.27. The Query Builder fully qualifies all field name references. Instead of displaying student_ID as shown in Example 14.27, the field name is preceded by the table name and a dot (i.e. Student.student_ID).

# EXAMPLE 14.27

```
SELECT student_ID, student_FirstName, student_LastName, major_ID,
       student_Phone, major_Name, major_Chair, major_Phone
FROM Student
INNER JOIN Department ON Student.major_ID = Department.major_ID
```