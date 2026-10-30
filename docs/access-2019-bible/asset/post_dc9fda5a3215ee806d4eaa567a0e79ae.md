
## NOTE

When you import text files with Date-type data, you must have a separator between the month, day, and year. Access reports an error if the field is specified as a Date/Time type and no delimiter is used. When you're exporting date fields, the separator is not needed.

With the Time Delimiter option, you can specify a separator (usually a colon) between the parts of time values in a text file. To change the separator, simply enter another in the Time Delimiter box.

Select the Four Digit Years check box to specify that the year portion of a date field is formatted with four digits. By checking this box, you can import dates that include the century (such as in 1981 or 2001). The default setting is to use four-digit years.

The Leading Zeros in Dates option specifies that date values include leading zeros. This means that date formats include leading zeros (as in 02/04/03), if needed.

## Importing and exporting XML documents

Importing XML documents is easy with Microsoft Access. XML is often used to transfer information between disparate platforms, databases, operating systems, applications, or companies. XML is used for raw data, metadata (data that describes other data), and even processing data. It's safe to say that most Access developers eventually import or export data in XML format.

Presenting XML in Access needs to be done in an odd way. You could easily import a simple XML document into your Access database, but the best way to find out how well Access uses XML is to begin by exporting something into XML.

Follow these steps to export data from Access to an XML file:

- 1. Open the Chapter06_1.accdb database.
- 2. Open tblDepartments in Datasheet view.
- 3. Select the External Data tab, and click XML File in the Export section.
- 4. Name the XML file tblDepartments.xml, and click OK. The Export XML dialog box (shown in Figure 6.16) appears.

## FIGURE 6.16

The Export XML dialog box.

![](img/1e45673ab6eca9d20e67635ff5b9b318_235_0.png)

5. Click OK to complete the export process.

The Export XML dialog box includes options for specifying advanced options for the XML export process. Clicking the More Options button opens a dialog box (see Figure 6.17) with several important XML settings.

## FIGURE 6.17

Advanced XML export options.

![](img/1e45673ab6eca9d20e67635ff5b9b318_236_0.png)

The data contained in an XML file may be relational or hierarchical. For example, a single XML file might contain information on both product categories and the products themselves. A schema file is needed for complex XML to be understood by other applications. Access automatically produces a schema file (XSD extension) for data exported in XML format. Figure 6.18 shows the Schema tab of the Export XML dialog box.

The XML schema file includes information such as the data type of each field and the source table’s primary key and indexes.

A further refinement of the XML export process is to specify how the XML data should be presented in an application using the exported data. (The presentation is specified using HTML conventions.) In most cases, the XML presentation file (XSL extension) is not needed, because the application that is designed to use the XML file displays the data as required by its users. Figure 6.19 shows the Presentation tab of the Export XML dialog box. Notice that none of the options on this tab is selected by default.

## FIGURE 6.18

Exporting XML schema information.

![](img/1e45673ab6eca9d20e67635ff5b9b318_237_0.png)

## FIGURE 6.19

XML presentation options.

![](img/1e45673ab6eca9d20e67635ff5b9b318_237_1.png)

In a text editor, such as Notepad, open tblDepartments.xml. You’ll see the contents of the XML file, as shown in Figure 6.20.

The first two lines of the text file define the version of XML that was used and the schema. The exported data and structure start on the third line. XML is a hierarchy of tags that define the structure of the data, and each piece of data is within an opening and closing tag. Each record begins with a tag for the name of the table. In this example `<tblDepartments>` is the tag that defines the table. A few lines down, there is a closing tag, `</tblDepartments>`, signifying the end of the record.

> **NOTE**
>
> XML uses tags to give context to the data. Opening tags define the start of a structure and consist of text between a less-than symbol (<) and a greater-than symbol (>). Closing tags define the end of the structure. Closing tags are formatted similarly to opening tags except that a forward slash is included after the less-than symbol (<).

## FIGURE 6.20

An exported XML file in plain text.

![](img/1e45673ab6eca9d20e67635ff5b9b318_238_0.png)

In between these two tags are the fields and data for that record. The first field of the first record is recorded as `<DeptNumber>1000</DeptNumber>`. An application that understands XML will interpret that line to mean there is a field named DeptNumber, and this record has 1000 in that field. This hierarchy of tags and data continues for each field in the record and for each record in the table.

Just as Access can export to XML, it can also import it. To import the tblDepartments.xml file that you just exported, follow these steps:

- 1. Click Import & Link ▸ New Data Source ▸ From File ▸ XML File on the External Data tab.
- 2. Browse to tblDepartments.xml, click Open, and then click OK. The Import XML dialog box, shown in Figure 6.21, displays how Access interprets the XML data.
- 3. Click OK.
- 4. Click Close. You can save the import steps before closing as described earlier in this chapter.

## FIGURE 6.21

Access understands XML data.

![](img/1e45673ab6eca9d20e67635ff5b9b318_239_0.png)

Access converted the well-formed XML into a table. The `<tblDepartments>` tag determines what the imported table will be named, the tags within the `<tblDepartments>` tag and its closing tag define the fields, and the data in between the field tags will become data in the new table.

## Importing and exporting HTML documents

Access enables you to import HTML tables as easily as any other database, Excel spreadsheet, or text file. You simply select an HTML file to import and use the HTML Import Wizard. The HTML Import Wizard works exactly like the other import wizards described earlier in this chapter.

And just like we demonstrated XML in the previous section, we’ll do an HTML import in reverse. First, you export a table to generate an HTML file, and then you import the file back into Access to create a new table:

- 1. **Open the Chapter06_1.accdb database and select tblEmployees from the Navigation pane.**
- 2. **Select the External Data tab, click the More drop-down button in the Export group, and select HTML Document.**
- 3. **Specify an HTML file as the export destination in the Export – HTML Document dialog box (see Figure 6.22).**
- 4. **Select your HTML output options and click OK.** The HTML export is completed as soon as you click the OK button. Unless you check Export Data with Formatting and Layout, no options other than what you see in Figure 6.22 are available when exporting HTML data.

Exporting Data with Formatting and Layout, an option in the Export – HTML Document dialog box, presents additional exporting options. The most important option is that it allows you to specify an HTML template for your export. An HTML template is a normal HTML file, except that it includes special tags that Access recognizes. These tags instruct Access where to place certain data when exporting, allowing you to define the other aspects of the HTML document, such as styling and logos.

![](img/1e45673ab6eca9d20e67635ff5b9b318_240_0.png)

## FIGURE 6.22

The Export – HTML Document dialog box.

![](img/1e45673ab6eca9d20e67635ff5b9b318_241_0.png)

Importing the HTML is much like importing a text file shown previously in this chapter. In fact, the Import HTML Wizard has most of the same screens and options as the Import Text Wizard, such as defining data types for fields and identifying the primary key.

## Importing Access objects other than tables

You can import other Access database tables or any other object in another database, which means you can import an existing table, query, form, report, macro, or module from another Access database. You can also import custom toolbars and menus.
