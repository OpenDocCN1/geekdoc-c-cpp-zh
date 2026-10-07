# Introduction to Language Integrated Query (LINQ)

| Standard Query Operator | Purpose | Deferred |
|---|---|---|
| All | Quantifiers | No |
| Any | Quantifiers | No |
| AsEnumerable | Conversion | Yes |
| Average | Aggregate | No |
| Cast | Conversion | Yes |
| Distinct | Set | Yes |
| ElementAt | Element | No |
| First | Element | No |
| Join | Join | Yes |
| Last | Element | No |
| OType | Conversion | Yes |
| OrderBy | Ordering | Yes |
| Select | Projection | Yes |
| Single | Element | No |
| Sum | Aggregate | No |
| ToArray | Conversion | No |
| ToList | Conversion | No |
| Where | Restriction | Yes |

FIGURE 4.4 Most often used query operators.

```
FacultyDataAdapter.SelectCommand = accCommand;
FacultyDataAdapter.Fill(ds, "Faculty");
var facultyinfo = (from fi in ds.Tables("Faculty").AsEnumerable()
    where fi.Field<string>("faculty_name").Equals(ComboName.Text))
foreach (var row in facultyinfo)
{
//Display selected row elements...
}
```

FIGURE 4.5 An example code for the operator AsEnumerable.

The key point for this query structure is the operator AsEnumerable(). Since different database systems use different collections and query operators, those must be converted to the type of IEnumerable<T> in order to use the data operations in LINQ using a Standard Query Operator that can perform complex data queries on an IEnumerable<T> sequence. Compiling an error would be encountered without this operator.

# Cast (Conversion Purpose)

A Cast operator provides a method for explicit conversion of the type of an object in an input sequence to an output sequence with specific type. The compiler treats cast-expression as type-name after the cast has been made. A point to be noted that the Cast operator works on the IEnumerable interface, but not the IEnumerable<T> interface, and it can convert any object with an IEnumerable type to IEnumerable<T>. An example of using this is shown in Figure 4.6.

# Join(Join Purpose)

A join of two data sources is the association of objects in one data source with objects that share a common attribute in another data source.
Joining is an important operation in queries whose relationships to each other cannot be followed directly. In object-oriented programming, this could mean a correlation between objects that is not modeled, such as the backwards direction of a