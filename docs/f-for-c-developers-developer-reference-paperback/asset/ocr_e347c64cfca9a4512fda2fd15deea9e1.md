# LISTING 4-56 SQL statement used to create the student course table and insert three test records

```
CREATE TABLE [dbo].[StudentScoreTable](
  [Name] [nvarchar](50) NOT NULL,
  [Course] [nchar](64) NULL,
  [Passed] [bit] NULL,
  CONSTRAINT [PK_StudentScoreTable] PRIMARY KEY CLUSTERED
  ([Name] ASC INDEX
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF,
  IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
[PRIMARY];
```

Insert test record data

```
insert into StudentScoreTable(Name,Course, Passed)
Values('Brent', 'History', 1)

insert into StudentScoreTable(Name,Course, Passed)
Values('Chris', 'Math', 1)

insert into StudentScoreTable(Name,Course, Passed)
Values('Anita', 'History', 1)

insert into StudentScoreTable(Name,Course, Passed)
Values('Andy', 'Math', 0)
```

The code in Listing 4-57 is F#. It retrieves data from the database using the SQL type provider. The generatePassLetter function is used to generate the Word document for students who pass the exam. The execution of this sample code generates three files, for the students named Anita, Chris, and Brent. Andy did not pass the exam, so there is no file for him.

# LISTING 4-57 Generating Word documents from the type provider query results

```
open System
open System.Linq
open DocumentFormat.OpenXml
open DocumentFormat.OpenXml.Packaging
open DocumentFormat.OpenXml.WordProcessing
open Microsoft.Fsharp.Data.TypeProviders
open Microsoft.Fsharp.Linq.NullableOperators

type T = SqlConnection("your connection to the database")
let t = T.GetDataContext()

let passedCandidates = query {
  for student in t.StudentScoreTable do
  where (student.Passed? = true)
  select (student.Name, student.Course) }
```