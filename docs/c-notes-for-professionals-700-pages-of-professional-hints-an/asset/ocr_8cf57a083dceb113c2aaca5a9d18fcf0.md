# Chapter 67: LINQ to XML

# Section 67.1: Read XML using LINQ to XML

```
<?xml version="1.0" encoding="utf-8" ?>
<Employees>
<Employee>
<EmpId>1</EmpId>
<Name>Sam</Name>
<Sex>Male</Sex>
<Phone Type="Home">423-555-0124</Phone>
<Phone Type="Work">424-555-0565</Phone>
<Address>
<Street>7A Cox Street</Street>
<City>Acampo</City>
<State>CA</State>
<Zip>95220</Zip>
<Country>USA</Country>
</Address>
</Employee>
<Employee>
<EmpId>2</EmpId>
<Name>Lucy</Name>
<Sex>Female</Sex>
<Phone Type="Home">143-555-0763</Phone>
<Phone Type="Work">434-555-0567</Phone>
<Address>
<Street>Jess Bay</Street>
<City>Alta</City>
<State>CA</State>
<Zip>95701</Zip>
<Country>USA</Country>
</Address>
</Employee>
</Employees>
```

To read that XML file using LINQ

```
XDocument xdocument = XDocument.Load("Employees.xml");
IEnumerable<XElement> employees = xdocument.Root.Elements();
foreach (var employee in employees)
{
    Console.WriteLine(employee);
}
```

To access single element

```
XElement xelem = XElement.Load("Employees.xml");
IEnumerable<XElement> employees = xelem.Root.Elements();
Console.WriteLine("List of all Employee Names :");
foreach (var employee in employees)
{
    Console.WriteLine(employee.Element("Name").Value);
}
```

To access multiple elements

```
XElement xelem = XElement.Load("Employees.xml");
```