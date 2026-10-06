Note Because CourseId is a Nullable<int>, you need to use =? to perform the equality operation. You need to use open Microsoft.Sharp.Linq.NullableOperators. Both = and != are valid operators. If the nullable value is on left side of the operator, != is applied; however, =? is used if the nullable value is on right side.

Using the Value property in a Nullable<T> type does not work in the query. This is by design, because using it in this may lead to a NULL exception when the Nullable<T> value is NULL.

# Using the sortBy Operator

Listing 4-24 shows how to use the sortBy operator to show the sorted names whose name length is greater than 4. By default, sortBy sorts the result in ascending order. The sortByDescending operator performs the sorting of results in a descending manner.

**LISTING 4-24** Using the sort code

```
Sort code
let internal q4 = query {
for n in db.Student do
sortBy n.Name
where (n.Name.Length > 4)
select n.Name

Execution result
"Anita"
"Brent"
"Cathy"
```

You can sort a second criterion by using thenBy or thenByDescending. Listing 4-25 sorts the result by a student's name and then by the student's age.

**LISTING 4-25** Using the thenBy keyword

```
let internal q4_2 = query {
for student in db.Student do
sortBy student.Age.Value
thenBy student.Name
select (student.Name, student.Age) }

showResult q4_2
```

188 PART II F#s Unique Features