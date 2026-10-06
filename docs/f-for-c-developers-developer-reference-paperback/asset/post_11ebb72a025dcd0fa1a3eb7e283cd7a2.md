
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

```sharp
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

```fsharp
// generate pass letter using OpenXML SDK
let generatePassLetter record =
let name, course = record
let filePath = sprintf@"%s.docx" name
let myDoc = WordProcessingDocument.Create(filePath, WordProcessingType.Document)

// Add a new main document part.
let mainPart = myDoc.AddMainDocumentPart()

// Create Document tree
mainPart.Document << Document()

// Create Body
let body = Body()

// Create paragraph
let createParagraph text =
let paragraph = Paragraph()
let run_paragraph = Run()

// put text
let text_paragraph = Text text

// Append elements.
ignore < run_paragraph.AppendChild(text_paragraph)
ignore < paragraph.AppendChild(run_paragraph)

// return paragraph
paragraph

// create a paragraph with text
let paragraph0 =
  createParagraph
  (sprintf "Dear %s" name)
let paragraph1 =
  createParagraph
  (sprintf "Congratulations! You passed %s" course)

[paragraph0; paragraph1]
|> List.iter(body.AppendChild(body))>ignore

// Save changes
mainPart.Document.Save()

// close the document and save all changes
myDoc.Close()

// generate letters for all passing students
passedCandidates
|> Seq.iter generatePassLetter
```

> Note You need to add a reference to DocumentFormat.OpenXml.dll, FSharp.Data.TypeProviders.dll, System.Data.dll, System.Data.Linq.dll, System.Xml.dll, and WindowsBase.dll to make the project compile.

List.iter requires that the ignore function returns unit. AppendChild returns a non-unit type. By using >> and the ignore function, you can get a new function that returns unit. If you forget how to use the |>, |, <<, and >> operators, you can refer to the “Pipeline-Forward Operator” section in Chapter 1.

CHAPTER 4 Type Providers 215

# CHAPTER 5

# Write Your Own Type Provider

There are four built-in type providers in F# 3.0. If you've wondered how to make a type provider that can be used to interpret data—such as the data in a database, in the cloud, or in an XML file—this chapter will show you how to do it.

# What Is a Type Provider?

As I mentioned at the beginning of Chapter 4, "Type Providers," the type provider is an adapter component that reads the underlying information schema and converts it to types in .NET. The information can be from data stores, services, or any other source of structured data. The typegeneration process is known as the provided type. The type generated from a type provider can be picked up by Microsoft IntelliSense. In addition to the class type and members, the type provider can provide metadata as a description of each column in a database table. These descriptions appear as tooltips. The type provider provides compile-time meta-programming support. This might seem heavy and difficult to digest. If that is the case, don't worry. And as more and more type provider samples are presented, different aspects of the type provider will be examined and theirs will clear.

You need to understand that the type provider types and methods are generated in a lazy way. The lazy generation decreases the code size. Imagine you have a complex database schema and your code accesses only one table in the database. The erased type provider generates only the code for that particular table. This allows the provided type to be large and even infinite. The built-in providers use type generation, which involves wrapping existing code-generation tools. This chapter focuses on how to write the erased type provider and the generated type. The erased type provider provides types that will be erased to others, such as System.Object. The following statement is from MSDN (http://msdn.microsoft.com/en-us/library/hh36014.aspx#BK_Erased);

Each type provider is erased to type obj, and all uses of the type will appear as type obj compiled in code. In fact, the underlying objects in these examples are strings, but the type will appear as Object in .NET compiled code. As all uses of type erasure, you can use explicit boxing, unboxing, and casting to subvert erased types. In this case, a exception that isn't valid may result when the type is used. A provider runtime can define its own private representation type to help protect against false representations. You can't define erased types in F# itself. Only provided types may be erased. You must understand the ramifications,

217

both practical and semantic, of using erased types. The type provider generates types that exist only at design time. The type-provider, which is named Provider1.fs, is the backbone of the project. It contains the type-provider, named TestScript.fsx is a script file that can be used to test the type provider. The generated project is shown in Figure 5-2.

# Setting Up the Development Environment

F# provides an API that you can use to write your type providers. The type-provider template is available.

 Note It is highly recommended that you use Visual Studio 2012 to author type providers.

As an alternative to performing a manual setup of Visual Studio solution, you can use Visual Studio template package published to http://visualstudallery.microsoft.com/43d0ffd0-1b9a-4581-a942-da85b6a8b3c. After the package is installed, the type project can be created via the New Project dialog as shown in Figure 5-1.

**FIGURE 5-1** Type-provider project

218 PART II F#'s Unique Features

The type-provider project is a class library, and it contains four files. The type-provider, which is named Provider1.fs, is the backbone of the project. It contains the type-provider, named TestScript.fsx is a script file that can be used to test the type provider. The generated project is shown in Figure 5-2.

**FIGURE 5-2** Generated files from the Type Provider template

Listing 5-1 contains the code needed to define a type provider. The type-provider type is denoted as the provided type, and method and property. The first line adds a reference to the Type Provider dynamic-link library (DLL). After the reference is ready, the second and third lines create the provided type and assign it to the value named t.

It is a good practice to design how an user will invoke the type provider. TPTestSuite have a parameterless constructor that does not require any special initialization code. Also, it has a property Property1.

# LISTING 5-1 Type-provider test file

```fsharp
# r "@\bin\Debug\TypeProviderTemplate9.dll"

type T = Samples.Info.TPTest.TPDebugType
let t = T())

let c = t.Property1
t.Property1 <- "aa"
printfn "methodName() = %A" (t.methodName())
```

Execution result
setter code
methodName() = 2
