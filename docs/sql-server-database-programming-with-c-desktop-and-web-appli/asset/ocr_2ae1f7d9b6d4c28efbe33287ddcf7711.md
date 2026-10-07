# SQL Server Database Programming with C#

```
A from in faculties.Elements("faculty")
where (string) f.Element("office") == "MTC-3,*"
orderby (string) f.Element("faculty_name")
select (string) f.Element("faculty_name");
```

```
B from in faculties.Elements("faculty"), p in faculties.Elements("phone")
where (string) f.Element("faculty_id") == "B"&& p.Value.StartsWith("750")
orderby (string) f.Element("faculty_name")
select f;
```

```
C from in students.Elements("student"), average = students.Elements("student")
Average(x) => (int) x.Element("gpa")
where (int) s.Element("gpa") > average
select s;
```

**FIGURE 4.57** A sample code to perform the query query using XML.

The query shown in section A in Figure 4.57 retrieves all of the offices from the faculties, by faculty_name, and returns them as string (the result of this query is IEnumerable<string>).

The query shown in section B in Figure 4.57 retrieves all members from faculty that have the faculty_id that starts from B and have a code of 750 ordered by the faculty_name. The result of this query is IEnumerable<XElement>.

Another example shown in section C in Figure 4.57 retrieving the students that have a GPA greater than the average GPA.

# 4.8.4.4 Using XPath with XSLT in LINQ to XML

LINQ to XML supports a set of "bridge classes" to allow it to work with existing capabilities in the System namespace, including XPath and XSLT. A point to be noticed is that System.Xml provides the 1.0 version of these specifications in "Oras."

Extension methods supporting XPath are enabled by referencing the System.Xml.XPath namespace by adding this namespace: using System.Xml.XPath; in the namespace declaration section on the code window of each project.

This brings into scope Navigator overloads to create XPathNavigator objects, XPathEvaluate overloads to evaluate an XPath expression, and XPathSelectElement[s] overloads that work like SingleNode and XPathSelectNodes in the System.Xml DOM API. It is necessary to pass in a NamespaceResolver object, just with DOM.

For example, to display all elements with the name "phone", the following codes can be developed:

```
foreach (var phone in faculties.XPathSelectElements("phone")
    Console.WriteLine(phone);
}
```

Likewise, Xsl is enabled by referencing the System.Xml namespace by typing: using System.Xml namespace declaration on the code window of each project. This allows you to create a XPathNavigator using the XDocumentCreate method and pass it to the Transform().

# 4.8.4.5 Mixing LINQ and Other Data Models

LINQ provides a consistent query experience across different datas via standard query operators and the use of Lambda Expressions that will be discussed in the next section. It also provides the ability to match and match LINQ-enabled data models/APIs within a single query, this