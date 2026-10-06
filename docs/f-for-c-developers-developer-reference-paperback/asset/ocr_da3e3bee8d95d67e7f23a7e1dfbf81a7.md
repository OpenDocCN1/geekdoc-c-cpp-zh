```
Execution result
("John", null)
("Anita", 20)
("Tom", 20)
("Lisa", 21)
("Zeoy", 21)
("Brent", 22)
("Cathy", 22)
("Ken", 22)
("Mark", 23)
```

In Listing 4-25, Age is a nullable value, so you have to reference the Value property in order to sort. The F# query feature provides a set of operators that can handle nullable values. Listing 4-26 shows how to use sortByNullableDescending.

+   - sortByNullable Sorts elements in ascending order by a given nullable value
- sortByNullableDescending Sorts elements in descending order by a given nullable value
- thenByNullable Like the thenBy operator, performs subsequent ordering of the elements in ascending order by a given nullable key
- thenByNullableDescending Like the thenByDescending operator, performs subsequent ordering of the elements in descending order by a given nullable key

LISTING 4-26 Using `sortByNullableDescending = query`

```
let internal q4_3 = query {
    for student in db.Student do
    sortByNullableDescending student.Age
    thenBy student.Name
    select (student.Name, student.Age)
}
showResult q4_3
```

```
Execution result
("Mark", 23)
("Brent", 22)
("Cathy", 22)
("Ken", 22)
("Lisa", 21)
("Zeoy", 21)
("Anita", 20)
("Tom", 20)
("John", null)
```