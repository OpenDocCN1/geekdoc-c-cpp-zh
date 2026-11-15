```
where File.GetLastWriteTime(fileName) <
DateTime.Now.AddMonths(-1);
select new FileInfo(fileName);
```

```
foreach (FileInfo file in files)
{
 // As simplification, current directory is
 // assumed to be a subdirectory of
 // rootDirectory
 string relativePath = file.FullName.Substring(
 Environment.CurrentDirectory.Length);
 Console.WriteLine("{0}({1})",
 relativePath, file.LastWriteTime);
 }
```

```
// ...
```

# OUTPUT 15.5:

```
.\TestData\Bill.cs<6/10/2007 9:33:55 PM)
.\TestData\Contact.cs<6/19/2007 11:40:30 PM)
.\TestData\Employee.cs<6/17/2007 1:33:22 AM)
.\TestData\Person.cs<10/22/2007 10:00:03 PM)
```

# Sorting

To order the items using a query expression we rely on the orderby clause (see Listing 15.7).

# LISTING 15.7: Sorting Using a Query Expression with an orderby Clause

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.IO;

 // ...
 static void ListByFileSize1(
 string rootDirectory, string searchPattern)
 {
 IEnumerable<string> fileNames =
 from fileName in Directory.GetFiles(
 rootDirectory, searchPattern)
 orderby (new FileInfo(fileName)).Length descending,
 fileName
 select fileName;
```