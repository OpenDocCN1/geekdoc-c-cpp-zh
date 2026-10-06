
I'll use the SQL Entity provider in the sample code. All the code is written on the assumption you already created a SQL Entity type provider and assigned it to a value named db. Because some query operations are not supported in the SQL Entity provider, I'll use AsEnumerable or array to create an in-memory data structure. The code is shown in Listing 4-14.

# **LISTING 4-14** Creating an in-memory student table

```fsharp
open System
open System.Linq
open Microsoft.Fsharp.Linq.NullableOperators

// define a student class
type Student() =
  member val ID = 0 with get, set
  member val Name = "" with get, set
  member val Age = Nullable(0) with get, set

// define the general show result function
let showResult query |> Seq.iter (printf "%A")
// set the in-memory student table
let studentTable = [
  Student(ID = 1, Name = "Anita", Age = Nullable(22));
  Student(ID = 1, Name = "Kate", Age = Nullable(22));
  Student(ID = 1, Name = "Brent", Age = Nullable(23));
  Student(ID = 1, Name = "Lisa", Age = Nullable(23));
  Student(ID = 1, Name = "Mark", Age = Nullable(24))].AsQueryable()
```

## Using the select Operator

The code in Listing 4-15 is a simple select example. You can think of the select operator as being the yield keyword in sequence generation or the select extension method in LINQ. The compiler will return the value. The for...in...do code iterates through the data, and the select operator specifies what needs to be inserted into the final result. I'll use the code let showResult query = query |> Seq.iter (printf "%A") to show the query.

# **LISTING 4-15** Simple select example

```fsharp
// Code for the example select
// simple select
let internal q0 = query {
  for n in db.Course do
    select n.CourseName
}

// general function to show the query result
let showResult query = query |> Seq.iter (printf "%A")
showResult q0
```

Execution result

```
"Math"
"Physics"
"Biology"
"English"
```

If the query can be translated to the server-side code, it will be executed on the server side. Unfortunately, not all computations can be translated to the server-side code. Listing 4-16 uses AsEnumerable() to specify that the computation should be performed on the client side, because printf cannot be translated to server-side code. Once the data is local, you are free to use any .NET function or pipeline operator.

# LISTING 4-16 Selection code with transform code

```fsharp
// Code for select with transform
let internal db = query {
  for n in db.Course.AsEnumerable() do
    select (printf "course name = %s" n.CourseName)
}
```

Execution result

```
"course name = 'Math'"
"course name = 'Physics'"
"course name = 'Biology'"
"course name = 'English'"
```

You can also create more complex queries that involve multiple select statements. Listing 4-17 shows how to print out all the value pairs where the first value is less than the second value. For example, a value pair is formed from two data sources.

# LIST 4-17 Selecting from different sources

```fsharp
let A = [0; 2; 4; 5; 6; 8; 9]
let B = [1; 3; 5; 7; 8]

query {
  for a in A do
  for b in B do
    where (a < b)
    select (a, b)
}
| Seq.iter(fun (n, e) -> printf "%d is less than %d" n e)
```

Execution result

```
0 is less than 1
0 is less than 3
0 is less than 5
0 is less than 7
0 is less than 8
2 is less than 3
2 is less than 5
2 is less than 7
2 is less than 8
4 is less than 5
4 is less than 7
4 is less than 8
5 is less than 7
5 is less than 8
6 is less than 7
6 is less than 8
```

## Using the where Operator

The where operator is used to filter data according to given conditions. Like the select operator, the computation can be executed either on the server or client side. Listing 4-18 shows how to filter the student names length is greater than 4 characters long. Because the result is filtered on the server, only three items are transferred over the wire.

**LISTING 4-18** *A where example*

```fsharp
// Code for the where example
let internal q2 = query {
  for n in db.Student do
    where (n.Name.Length > 4)
    select n.Name
}

showResult q2
```

Execution result

```
"Brent"
"Anita"
"Cathy"
```

Although performing the filter action on the client side is not a recommended approach, especially if the resulting data set is large, I still list the sample code here in case complex filtering is needed on the client side. See Listing 4-19.

# LISTING 4-19 The *where* function performed on the client side

```fsharp
// where function performed on the client side
let internal q3 = query {
  for n in db.Student
  select n.Name
} // filter on client side
let q3_2 = q3 | Seq.filter(fun n -> n.Length > 4)

showResult q3_2
```

Execution result

```
"Brent"
"Anita"
"Cathy"
```

Listing 4-20 is another example of filtering data on the client side. The code gives each element ID and filters the results later according to this client-generated ID.

**LISTING 4-20** Filter on a client-generated value

```fsharp
let internal myQuery = query {
  for n in db.Student do
  select n.Name
} // filter on client side based on ID
let result = myQuery
| Seq.map(fun i -> (i, n))
| Seq.filter(fun (i, n) -> i % 2 = 0)
showResult result
```

Execution result

```
(0, 'Lisa')
(2, 'Anita')
(4, 'Cathy')
(6, 'Mary')
(8, 'John')
```

**Note** The actual result might be different depending on the targeted data.

## Using the join Operator

The join example in Listing 4-21 shows how to join data scattered across different tables. In the join statement, the order of the keys is significant. The table db.Student, which is the main table, must be present first in the on part. The example lists the course ID and student name as a result.

LISTING 4-21 A join example

```fsharp
// Code for the join example
let q5 = query {
  for student in db.Student do
    join course in db.CourseSelection on (student.StudentID = course.StudentID)
    select (course.CourseID, student.Name)
}

showResult q5
```

Execution result

```
(3, 'Anita')
(1, 'Lisa')
(2, 'Anita')
(2, 'Brent')
(3, 'Brent')
(1, 'Anita')
(1, 'Brent')
```

The CourseID in the result from Listing 4-21 is not user-friendly. If the student name can be shown, that will be better. In Listing 4-22, groupJoin operator is used to show a more user-friendly result. Because CourseID is a nullable integer, you are to use = in the Microsoft.Fsharp.Linq.NullableOperators module to perform the comparison.

LISTING 4-22 Using a group join

```fsharp
let q6 = query {
  for student in db.Student do
    groupJoin course in db.CourseSelection on (student.StudentID = courseSelection.StudentID) into g
    for courseSelection in g do
      join course in db.Course on (courseSelection.CourseID = course.CourseID)
      select (student.Name, course.CourseName)
}

showResult q6
```

Execution result

```
("Anita", "Biology")
("Lisa", "Math")
("Anita", "Physics")
("Brent", "Physics")
("Brent", "Biology")
("Anita", "Math")
("Brent", "Math")
```

There is another join scenario called an outer join. The F# outer join operator is similar to SQL's outer join, but it supports only the left outer join. The right outer join functionality can be achieved by switching the two tables. Listing 4-23 shows how to use leftOuterJoin to show the outer join.

# LISTING 4-23 Using the left outer join

```fsharp
let internal qS = query {
  for student in db.Student do
    leftOuterJoin selection in db.CourseSelection on (student.StudentID = selection.CourseID) into result
    for selection in result do
      select (student.Name, selection.CourseName)
}

showResult qS
```

Execution result

```
("Lisa", "Math")
("Lisa", "Math")
("Lisa", "Math")
("Brent", "Physics")
("Brent", "Physics")
("Anita", "Biology")
("Anita", "Biology")
("Ken", null)
("Cathy", null)
("Tom", null)
("Mary", null)
("Mark", null)
("John", null)
```

**Note** Because CourseId is a Nullable<int>, you need to use =? to perform the equality operation. You need to use open Microsoft.Fsharp.Linq.NullableOperators. Both = and != are valid operators. If the nullable value is on the left side of the operator, != is applied; however, =? is used if the nullable value is on right side.

Using the Value property in a Nullable<T> type does not work in the query. This is by design, because using it here may lead to a Null exception when the Nullable<T> value is NULL.

## Using the sortBy Operator

Listing 4-24 shows how to use the sortBy operator to show the sorted names whose name length is greater than 4. By default, sortBy sorts the result in ascending order. The sortByDescending operator performs the sorting of results in a descending manner.

**LISTING 4-24** Using the sort code

```fsharp
// Sort code
let internal q4 = query {
  for n in db.Student do
  sortBy n.Name
  where (n.Name.Length > 4)
  select n.Name
}

Execution result

```
"Anita"
"Brent"
"Cathy"
```

You can sort a second criterion by using thenBy or thenByDescending. Listing 4-25 sorts the result by a student's name and then by the student's age.

**LISTING 4-25** Using the thenBy keyword

```fsharp
let internal q4_2 = query {
  for student in db.Student do
  sortBy student.Age.Value
  thenBy student.Name
  select (student.Name, student.Age) }

showResult q4_2
```
