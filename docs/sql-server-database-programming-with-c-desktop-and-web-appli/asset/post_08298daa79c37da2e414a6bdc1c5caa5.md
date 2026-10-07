
# viii Contents

- 2.8.3 Oracle Databases ................................................................................ 27
- 2.8.3.1 Data Files ................................................................................ 27
- 2.8.3.2 Tables ....................................................................................... 28
- 2.8.3.3 Views ........................................................................................ 28
- 2.8.3.4 Stored Procedures ................................................................ 28
- 2.9 Create Microsoft SQL Server 2019 Express Sample Database........................................... 30
- 2.9.1 Create the Login Table ...................................................................... 31
- 2.9.2 Create the Faculty Table ................................................................. 33
- 2.9.3 Create Other Tables ...................................................................... 34
- 2.9.4 Create Relationships Among Tables ........................................................ 37
- 2.9.4.1 Create Relationship between the Login and the Faculty Tables ................................................................................... 38
- 2.9.4.2 Create Relationship between the Login and the Student Tables ................................................................................... 40
- 2.9.4.3 Create Relationship between the Faculty and the Course Tables ................................................................................... 42
- 2.9.4.4 Create Relationship between the Student and the Student Courses ................................................................................... 43
- 2.9.4.5 Create Relationship between the Course and the Student Tables ................................................................................... 43
- 2.9.5 Store Images to the SQL Server 2019 Express Database....................................... 44
- 2.10 A Short-Cut: How to Use the Sample Database without Building It ........................ 53
- 2.11 Chapter Summary ....................................................................................... 53
- Homework ............................................................................................ 53

# Chapter 3 Introduction to ADO.NET ............................................................ 57

- 3.1 The ADO and ADO.NET ........................................................................ 57
- 3.2 Overview of the ADO.NET 2.0 ................................................................. 58
- 3.3 The Architecture of the ADO.NET 2.0 ........................................................ 59
- 3.4 The Components of ADO.NET 2.0 ............................................................ 60
- 3.4.1 The Data Provider ............................................................................ 60
- 3.4.1.1 The ODBC Data Provider ......................................................... 61
- 3.4.1.2 The OLEDB Data Provider ................................................................ 62
- 3.4.1.3 The SQL Server Data Provider ...................................................... 62
- 3.4.1.4 The Oracle Data Provider ............................................................ 62
- 3.4.2 The Connection Class ..................................................................... 63
- 3.4.2.1 The Open(t) Method of the Connection Class ................................... 65
- 3.4.2.2 The Close(t) Method of the Connection Class ............................... 66
- 3.4.2.3 The Dispose(t) Method of the Connection Class ............................. 66
- 3.4.3 The Command and the Parameter Classes ............................................ 66
- 3.4.3.1 The Properties of the Command Class ......................................... 67
- 3.4.3.2 The Constructors and Properties of the Parameter Class .............................................................................................. 67
- 3.4.3.3 Parameter Mapping ........................................................... 68
- 3.4.3.4 The Methods of the ParameterCollection Class ........................ 69
- 3.4.3.5 The Constructor of the Command Class ................................... 71
- 3.4.3.6 The Methods of the Command Class ...................................... 72
- 3.4.4 The DataAdapter Class ............................................................ 74
- 3.4.4.1 The Constructor of the DataAdapter Class................................ 74
- 3.4.4.2 The Properties of the DataAdapter Class ........................ 74
- 3.4.4.3 The Methods of the DataAdapter Class ................................................ 75
- 3.4.4.4 The Events of the DataAdapter Class ................................................ 75
- 3.4.5 The DataReader Class ....................................................................... 76
- 3.4.6 The DataSet Component ....................................................... 78
- 3.4.6.1 The DataSet Constructor ................................................... 80
- 3.4.6.2 The DataSet Properties ...................................................... 80
- 3.4.6.3 The DataSet Methods ...................................................... 81
- 3.4.6.4 The DataSet Events ........................................................ 81
- 3.4.7 The DataTable Component ................................................... 83
- 3.4.7.1 The DataTable Constructor ........................................ 83
- 3.4.7.2 The DataTable Properties ................................... 84
- 3.4.7.3 The DataTable Methods ....................................... 84
- 3.4.7.4 The DataTable Events ...................................... 85
- 3.4.8 ADO.NET 4 Entity Framework ................................... 87
- 3.4.8.1 The ADO.NET 5 Entity Data Model .......................... 89
- 3.4.8.2 Using the ADO.NET 3.5 Entity Data Model Wizard 92
- 3.5 Chapter Summary ................................................... 99

Homework ................................................................ 101

# Chapter 4 Introduction to Language Integrated Query (LINQ)...

- 4.1 Overview of Language Integrated Query ............... 105
- 4.1.1 Some Interfaces Used in LINQ ...................... 105
- 4.1.1.1 The IEnumerable and IEnumerable<T> Interfaces... 106
- 4.1.1.2 The IQueryable and IQueryable<T> Interfaces... 107
- 4.1.2 Standard Query Operators ................... 108
- 4.1.3 Deferred Standard Query Operators...... 108
- 4.1.4 Non-Deferred Standard Query Operators... 113
- 4.2 Introduction to LINQ ................ 115
- 4.3 The Architecture and Components of LINQ .... 118
- 4.3.1 Overview of LINQ to Objects ........ 119
- 4.3.2 Overview of LINQ to DataSet ........ 119
- 4.3.3 Overview of LINQ to SQL ................ 119
- 4.3.4 Overview of LINQ to Entities ........ 120
- 4.3.5 Overview of LINQ to XML .............. 121
- 4.4 LINQ to Objects ................ 121
- 4.4.1 LINQ and ArrayList ................ 122
- 4.4.2 LINQ and Strings ................ 123
- 4.4.2.1 Query a String to Determine the Type of Numeric Digits... 124
- 4.4.2.2 Sort Lines of Structured Text by Any Field in the Line... 125
- 4.4.3 LINQ and File Directories............... 127
- 4.4.3.1 Query the Contents of Files in a Folder... 128
- 4.4.4 LINQ and Reflection ............ 130
- 4.5 LINQ to DataSet ................ 131
- 4.5.1 Operations to DataSet Objects ... 132
- 4.5.1.1 Query Expression Syntax... 133
- 4.5.1.2 Method-Based Query Syntax... 134
- 4.5.1.3 Query the Single Table... 136
- 4.5.1.4 Query the Single Table... 138
- 4.4.2.1 Query a String to Determine the Type of Numeric Digits... 124
- 4.4.2.2 Sort Lines of Structured Text by Any Field in the Line... 125
- 4.4.3.1 Query the Contents of Files in a Folder... 128
- 4.5.1.1 Query Expression Syntax... 133
- 4.5.1.2 Method-Based Query Syntax... 134
- 4.5.1.3 Query the Single Table... 136
- 4.5.1.4 Query the Single Table... 138
- 4.5.2 Operations to DataSet............................... 141
- 4.5.3 Operations to DataSet..................................... 144
- 4.6 LINQ to SQL...................................................... 148
- 4.6.1 LINQ to SQL............................................... 148
- 4.7 LINQ to Entities...................................................... 149
- 4.7.1 The ObjectContext......................................... 149
- 4.7.2 The ObjectContext..................................................... 150
- 4.7.3 The ObjectQuery............................................... 150
- 4.7.4 LINQ to Entities Flow............................................... 150
- 4.7.4.1 Construct an ObjectQuery............................................... 151
- 4.7.4.2 Compose a LINQ to Entities......................................... 151
- 4.7.4.3 Convert the Query to Command Trees................................................ 151
- 4.7.4.4 Execute the Query...................................................... 152
- 4.7.4.5 Materialize the Query...................................................... 152
- 4.8 LINQ to XML.................................................................... 153
- 4.8.1 LINQ to XML Hierarchy......................................... 154
- 4.8.2 Manipulate XML............................................................... 155
- 4.8.2.1 Creating XML from Scratch................................................ 155
- 4.8.2.2 Insert XML...................................................... 156
- 4.8.2.3 Update XML................................................................ 157
- 4.8.2.4 Delete XML........................................................................... 158
- 4.8.3 Manipulate XML Attributes...................................................... 158
- 4.8.3.1 Add XML Attributes....................................................... 158
- 4.8.3.2 Get XML Attributes..................................................... 159
- 4.8.3.3 Delete XML Attributes.................................................. 159
- 4.8.4 Query XML with LINQ to XML............................................... 159
- 4.8.4.1 Standard Query Operators and XML............................... 160
- 4.8.4.2 XML Query Extensions.................................................. 160
- 4.8.4.3 Using Query Expressions with XML............................... 161
- 4.8.4.4 Using XPath and XSLT with LINQ to XML................................ 162
- 4.8.4.5 Mixing XML and Other Data Models............................................... 162
- 4.9 C# 3.0 Language Enhancement for LINQ.................................. 164
- 4.9.1 Lambda Expressions.................................................. 165
- 4.9.2 Extension Methods...................................................... 166
- 4.9.3 Implicitly Typed Variables..................................... 167
- 4.9.4 Query Expressions...................................................... 168
- 4.10 Chapter Summary....................................................... 169

Homework........................................................................... 170

# Chapter 5 Data Query with Visual C#.NET.................................. 175

PART I DATA QUERY WITH VISUAL DESIGN TOOLS AND WIZARDS..................................................................... 176

- 5.1 Visual Studio Design Tools and Wizards.............................. 176
- 5.1.1 Data Design Tools in the Toolbox Window......................... 176
- 5.1.1.2 DataSet............................................................. 176
- 5.1.1.3 DataGridView....................................................... 178
- 5.1.1.4 BindingSource..................................................... 178
- 5.1.1.4 BindingNavigator............................................... 179
- 5.1.1.5 TableAdapter.................................................. 179
