# NOTE

When you import text files with Date-type data, you must have a separator between the month, day, and year. Access reports an error if the field is specified as a Date/Time type and no delimiter is used. When you're exporting date fields, the separator is not needed.

With the Time Delimiter option, you can specify a separator (usually a colon) between the parts of time values in a text file. To change the separator, simply enter another in the Time Delimiter box.

Select the Four Digit Years check box to specify that the year portion of a date field is formatted with four digits. By checking this box, you can import dates that include the century (such as in 1981 or 2001). The default setting is to use four-digit years.

The Leading Zeros in Dates option specifies that date values include leading zeros. This means that date formats include leading zeros (as in 02/04/03), if needed.

# Importing and exporting XML documents

Importing XML documents is easy with Microsoft Access. XML is often used to transfer information between disparate platforms, databases, operating systems, applications, or companies. XML is used for raw data, metadata (data that describes other data), and even processing data. It's safe to say that most Access developers eventually import or export data in XML format.

Presenting XML in Access needs to be done in an odd way. You could easily import a simple XML document in your Access database, but the best way to find out how well Access uses XML is to begin by exporting something into XML.

Follow these steps to export data from Access to an XML file:

+   1. Open the Chapter06_1.accdb database.
+   2. Open tblDepartments in Datasheet view.
+   3. Select the External Data tab, and click XML File in the Export section.
+   4. Name the XML file tblDepartments.xml, and click OK. The Export XML dialog box (shown in Figure 6.16) appears.

# FIGURE 6.16

The Export XML dialog box.

![](bbox=[0.22, 0.95, 0.58, 1.0])

5. Click OK to complete the export process.