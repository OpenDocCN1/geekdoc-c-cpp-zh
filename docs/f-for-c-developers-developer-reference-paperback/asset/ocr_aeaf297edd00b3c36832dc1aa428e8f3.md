# Using the group Operator

The **group** operator is often used with an aggregate function. Listing 4-27 counts the number of students in each age group.

**LISTING 4-27** A *groupBy* example

```
The code for a *groupBy* query
let internal q7 = query {
  for student in db.Student do
    groupBy student.Age into g
    select (g.Key, g.Count())
}

showResult q7
```

Execution result

(null, 1)
(20, 2)
(21, 2)
(22, 3)
(23, 1)

Again, the result is not user friendly because the result does not show the student names in the result. To show the student names, you can use *groupValBy* to select a value with the group. The full code is shown in Listing 4-28. It shows a student name sequence in each age group.

**LISTING 4-28** A *groupValBy* example

```
Code for using groupValBy
let internal q8 = query {
  for student in db.Student do
    groupValBy student.Name student.Age into g
    select (g, g.Key, g.Count())
}

showResult q8
```

Execution result

(seq["John", null, 1)
(seq["Anita", "Tom", 20, 2)
(seq["Lisa", "Zeoy", 21, 2)
(seq["Brent", "Ken", "Cathy", 22, 3)
(seq["Mark", 23, 1)