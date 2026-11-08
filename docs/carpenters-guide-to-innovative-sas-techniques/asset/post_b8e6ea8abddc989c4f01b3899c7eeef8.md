
#### 1.5.2 Pass-Through Efficiencies

When using PROC SQL to create and pass database-specific code to a database other than SAS, such as Oracle or DB2, it is important that you be careful with how you program the particular problem. Depending on how it is coded, SQL can be very efficient or very inefficient, and this can be an even more important issue when you use pass-through techniques to create a data subset.

Passing information back from the server is usually slower than processing on the server. Design the pass-through to minimize the amount of returned information. Generally the primary database will be stored at a location with the maximum processing power. Take advantage of that power. At the very least, minimizing the amount of information that has to be transferred back to you will help preserve your bandwidth.

In SQL, data sets are processed in memory. This means that large data set joins should be performed where available memory is maximized. When a join becomes memory bound, subsetting the data before the join can be helpful. Know and understand your database and OS; some WHERE statements form clauses that are applied to the result of the join rather than to the incoming data set.

Even when you do not intend to write to the primary database that is being accessed using an SQL pass-through, extra process checking may be involved against that data table. These checks, which can be costly, can potentially be eliminated by designating the incoming data table as read-only. This can be accomplished in a number of ways. In DB2, using the clause *for fetch only* in the code that is being passed to the database eliminates write checks against the incoming table. In the DB2 pass-through example in Section 1.5.1, we only want to extract or fetch data. We speed up the process by letting the database know that we will not be writing any data – only fetching it.

**MORE INFORMATION**

An SQL step using pass-through code can be found in Section 5.4.2.

### 1.6 Reading and Writing to XML

Extensible Markup Language, XML, has a hierarchical structure while SAS data sets are record or observation based. Because XML is fast becoming a universal data exchange format, it is incumbent for the SAS programmer to have a working knowledge of how to move information from SAS to XML and from XML to SAS.

The XML engine (Section 1.6.2) was first introduced in Version 8 of SAS. Later the ODS XML destination was added; however, currently the functionality of the XML destination has been built into the ODS MARKUP destination (see Section 1.6.1).

Because XML is text based and each row contains its own metadata, the files themselves can be quite large.

**SEE ALSO**

A very nice overview of XML and its relationship to SAS can be found in (Pratter, 2008). Other introductory discussions on the relationship of XML to SAS include: Chapal (2003), Palmer (2003 and 2004), and in the SAS documentation on “XML Engine with DATA Step or PROC COPY”.

#### 1.6.1 Using ODS

You can create an XML file using the ODS MARKUP destination. The file can contain procedure output in XML format, and this XML file can then be passed to another application that utilizes/reads XML. By default, the MARKUP destination creates an XML file.

```sas
title1 '1.6.1 Using ODS MARKUP';
ods markup file="&path\\data\\E1_6_1Names.xml"; ❶

* create a xml file of the report; ❷
proc print data=advrpt.demog;
    var lname fname sex dob;
    run;
ods markup close; ❸
```

- ❶ The FILE= option is used to designate the name of the file to be created. Notice the use of the XML extension.

- ❷ The procedure must be within the ODS ‘sandwich.’

- ❸ The destination must be closed before the file ❶ can be used outside of SAS.

**MORE INFORMATION**

If the application that you are planning to use with the XML file is Excel, the EXCELXP tagset is a superior choice (see Section 11.2).

**SEE ALSO**

The LinkedIn thread [http://www.linkedin.com/groupItem?view=&srchtype=discussedNews&gid=70702&item=74453221&type=member&trk=eml-anet_dig-b_pdt-ttl-cn&ut=34c4-PQjofGK1](http://www.linkedin.com/groupItem?view=&srchtype=discussedNews&gid=70702&item=74453221&type=member&trk=eml-anet_dig-b_pdt-ttl-cn&ut=34c4-PQjofGK1) follows a discussion of the generation of XML using ODS.

#### 1.6.2 Using the XML Engine

The use of the XML engine is a process similar to the one shown in Section 1.6.1, and can be used to write to the XML format. XML is a markup language and XML code is stored in a text file that can be both read and written by SAS. As in the example above, an engine is used on the LIBNAME statement to establish the link with SAS that performs the conversion. A fileref is established and it is used in the LIBNAME statement.

```sas
filename xmlmst "&path\\data\\E1_6_2list.xml";
libname toxml xml xmlfileref=xmlmst; ❶

* create a xml file (E1_6_2list.xml);
data toxml.patlist; ❷
    set advrpt.demog(keep=lname fname sex dob);
    run;

* convert xml to sas;
data fromxml;
    set toxml.patlist; ❸
    run;
```

- ❶ On the LIBNAME statement that has the XML engine, the XMLFILEREF= option is used to point to the fileref either containing the XML file or, as is the case in this example, the file that is to be written.

```xml
<?xml version="1.0" encoding="windows-1252" ?>
<TABLE>
  <PATLIST> ③
    <lname>Adams</lname>
    <fname>Mary</fname>
    <sex>F</sex>
    <dob>1951-08-12</dob>
  </PATLIST>
  <PATLIST>
    <lname>Adamson</lname>
    <fname>Joan</fname>
    <sex>F</sex>
    <dob missing="." />
  </PATLIST>
    . . . the remaining observations are not shown . . . .
```

- ② The **libref** TOXML can be used to both read and write the XML file. The name of the data set (PATLIST) is recorded as a part of the XML file ③. This means that multiple SAS data sets can be written to the same XML file.

The selected variables are written to the XML file. Notice that the variables are named on each line and that the date has been re-coded into a YYYY-MM-DD form, and that the missing DOB for ‘Joan Adamson’ has been written using the `missing=` notation.

**SEE ALSO**

Hemendinger and Slaughter (2011) briefly describe the use of XML and the XML Mapper.

![](img/4b16455363806a3241267bf9f49ba5d1_65_0.png)

## Chapter 2: Working with Your Data

- **2.1 Data Set Options** 38
    - 2.1.1 REPLACE and REEMPT 40
    - 2.1.2 Password Protection 41
    - 2.1.3 KEEP, DROP, and RENAME Options 42
    - 2.1.4 Observation Control Using FIRSTOBS and OBS Data Set Options 43
- **2.2 Evaluating Expressions** 45
    - 2.2.1 Operator Hierarchy 45
    - 2.2.2 Using the Colon as a Comparison Modifier 46
    - 2.2.3 Logical and Comparison Operators in Assignment Statements 47
    - 2.2.4 Compound Inequalities 49
    - 2.2.5 The MIN and MAX Operators 50
    - 2.2.6 Numeric Expressions and Boolean Transformations 51
- **2.3 Data Validation and Exception Reporting** 52
    - 2.3.1 Data Validation 52
    - 2.3.2 Writing to an Error Data Set 55
    - 2.3.3 Controlling Exception Reporting with Macros 58
- **2.4 Normalizing - Transposing the Data** 60
    - 2.4.1 Using PROC TRANSPOSE 61
    - 2.4.2 Transposing in the DATA Step 63
- **2.5 Filling Sparse Data** 65
    - 2.5.1 Known Template of Rows 65
    - 2.5.2 Double Transpose 67
    - 2.5.3 Using COMPLETETYPES with PROC MEANS or PROC SUMMARY 70
    - 2.5.4 Using CLASSDATA 70
    - 2.5.5 Using Preloaded Formats 72
    - 2.5.6 Using the SPARSE Option with PROC FREQ 73
- **2.6 Some General Concepts** 73
    - 2.6.1 Shorthand Variable Naming 73
    - 2.6.2 Understanding the ORDER= Option 77
    - 2.6.3 Quotes within Quotes within Quotes 79
    - 2.6.4 Setting the Length of Numeric Variables 81
- **2.7 WHERE Specifics** 82
    - 2.7.1 Operators Just for the WHERE 83
    - 2.7.2 Interaction with the BY Statement 86
- **2.8 Appending Data Sets** 88
    - 2.8.1 Appending Data Sets Using the DATA Step and SQL UNION 88
    - 2.8.2 Using the DATASETS Procedure’s APPEND Statement 90
- **2.9 Finding and Eliminating Duplicates** 90
    - 2.9.1 Using PROC SORT 91
    - 2.9.2 Using FIRST. and LAST. BY-Group Processing 92
    - 2.9.3 Using PROC SQL 93
    - 2.9.4 Using PROC FREQ 93
    - 2.9.5 Using the Data Component Hash Object 94
- **2.10 Working with Missing Values** 97
    - 2.10.1 Special Missing Values 97
    - 2.10.2 MISSING System Option 98
    - 2.10.3 Using the CMISS, NMISS, and MISSING Functions 99
    - 2.10.4 Using the CALL MISSING Routine 100
    - 2.10.5 When Classification Variables Are Missing 100
    - 2.10.6 Missing Values and More Variables 101
    - 2.10.7 Imputing Missing Values 101

In SAS, the data set is central to most of our analyses and reporting. This means that it is crucial that we have the power to know all sorts of things about our data. The power that we need comes from a multitude of SAS tools and techniques. This chapter is a fairly random collection of these tools and techniques that can help us accomplish our goals of working with our data sets.

### 2.1 Data Set Options

Data set options can be used to modify how a data set is either read or written. There are over three dozen of these options, and while you will generally only make use of a handful of them, you should have a good idea of their scope.
