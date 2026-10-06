# Using the head, last, and nth Operators

Sometimes you need one element in the sequence. The head, last, and nth operators are designed for this purpose. You use the head operator on the SQL storage and the other operators with the in-memory structure. Listing 4-33 shows the first student's name. Listing 4-34 shows how to get the last and nth elements.

**LISTING 4-33** A head example

```
// return internal q5
let internal q5 = query {
for student in db.Student do
select student.Name
head }

showResult [ q5 ]

// get the first element; if there is no first element returned, returns default
let internal q16 = query {
for student in db.Student do
select student.Name
headOrFault }

showResult [ q16 ]
```

**LISTING 4-34** Example that uses last and nth

```
open System
open System.Linq
open Microsoft.Fsharp.Linq.NullableOperators

type Student() = =
member Val ID = 0 with get, set
member Val Name = "" with get, set
member Val Age = Nullable(0) with get, set

let showResult query = query > Seq.iter (printf "%A")

let studentTable = [
Student(ID = 1, Name = "Anita", Age = Nullable(22));
Student(ID = 1, Name = "Kate", Age = Nullable(22))
Student(ID = 1, Name = "Brent", Age = Nullable(23))
Student(ID = 1, Name = "Lisa", Age = Nullable(24))
Student(ID = 1, Name = "Mark", Age = Nullable(24))].AsQueryable()

// take the last student
let internal q15 = query {
for student in studentTable do
select student.Name
last }
```