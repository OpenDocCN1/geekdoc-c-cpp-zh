```
let news = latestNews |> Seq.Array

// get the range tuple as "A1", "A10"
let getRangeStrings columnName news =
  let start = sprintf "%cd" columnName 1
  let 'end' = sprintf "%cd" columnName (news |> Seq.length)
start, 'end'
```

let len = news.Length

```
// get range tuple, which contains start and end
let range0=(getRangeStrings 'B') news
let range1=(getRangeStrings 'C') news
```

```
// insert title to B8 column
(worksheet.Range (fst range0, snd range0)).Value2 <- Array2D.init len 1 (fun x _ ->
ews.[x].Title)
```

```
// insert summary to C column
(worksheet.Range (fst range1, snd range1)).Value2 <- Array2D.init len 1 (fun x _ ->
ews.[x].Summary)
```

> Note A reference to the Microsoft.Excel.Interop.dll is needed to invoke the Excel function.

# Generating a Word Document

In addition to an Excel file, you can also export data to a Microsoft Word file using the Office OpenXML SDK, which can be downloaded from http://www.microsoft.com/en-us/download/details.aspx?id=5124. The sample presented in this section is used to generate a notification letter for students who pass an exam. The pass/fail information is stored in the database. The type provider queries the database and filters the students who have passed the exam. The students' information is then passed to various OpenXML methods to generate the Word documents. Listing 4-56 creates the table in a SQL Server database. The table has three columns:

+   * Name Student name, which is also the key
* Course Course name
* Passed Boolean value to indicate whether the student passed the exam