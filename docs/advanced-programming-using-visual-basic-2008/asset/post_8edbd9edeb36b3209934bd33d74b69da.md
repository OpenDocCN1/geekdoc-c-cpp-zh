
- In the IDE's Solution Explorer, rename the solution and the project. The best way to do this is to right-click on the name and choose the *Rename* command from the shortcut menu. To rename the solution, you must display the solution name. Select *Tools / Options / Projects and Solutions / General / Always show solution*.
- Rename the forms, if desired. If you rename the startup form, you must open the Project Designer (*Project / ProjectName Properties*) and set the Startup Object.
- Open the *Project Properties* dialog and change the assembly name to match your new project name.

*Warning:* Do not try to copy a project that is open using the *Save As* command, attempting to place a copy in a new location.

## Refresh the Database in an Update Program

When you write a database update program, you must test all options, including adding records, deleting records, and modifying records. With a little caution, you can delete the modified version of the database and replace it with an unchanged version.

## How Windows Applications Handle the Database File

When you set up a new data source, the wizard asks you whether you want to add the database file to the project folder. To make your projects portable, you should always say Yes. But when you run the application, another copy is made, into the bin\Debug (or bin\Release) folder. Your program actually updates the copy in bin\Debug.

The version of the file that you retrieve for each program run depends on a property of the database file. Select the file in the Solution Explorer and set the property for Copy to Output Directory to Copy if newer. By default, the property is set to Copy always, which means that, for every program run, you get a new, fresh copy of the file and cannot see changes made on the last program run. With the Copy if newer setting, each time you run the application, VS checks the timestamp on the two copies of the database: if they are the same or the file in bin\Debug is newer, no copy is performed. But if the file in bin\Debug is older or no file exists in bin\Debug, then the file from the project folder is copied as the application begins to run.

You can easily return to the original version of the data file by deleting the copy in bin\Debug. In addition to the .mdf file (the main database file), you also must delete the log.ldf file, which holds the index and timestamp information.

You may not be able to see the database files in the Solution Explorer initially. Select Show All Files and click the Refresh button; then expand the bin\Debug folder nodes to see the .mdf and .ldf files. You can delete the files directly in the Solution Explorer by right-clicking and selecting Delete.

## Use Code Snippets and Samples

## Code Snippets

Code snippets are small samples of code that can show you how to accomplish many programming tasks. The Insert Snippet menu option is available on the context menu (right-click) of the Editor window.

When you select a snippet type, the editor places the code right in your program, where you can study it and/or modify and use it. You can learn many useful techniques by opening snippets.

## Sample Projects

Visual Studio includes many sample projects (all editions except the Express Edition) that you can use to learn new techniques. From the Help menu, select Contents. Expand the nodes for Development Tools and Languages / Visual Studio / Visual Basic to find the Samples node.

The walkthroughs in Help are another avenue for pursuing your study of VB. These tutorials give step-by-step introductions to many techniques and controls.

## Glossary

### A
abstract class Used only to create derived classes; cannot have an object instantiated from the class.
abstraction A model of an object, for the purpose of determining the characteristics (properties) and the behaviors (methods) of the object.
AcceptChanges method Resets a dataset to indicate that no changes have been made. Usually used after an Update method, which commits the changes to the original data source.
accessibility (classes, variables, and procedures) Used to determine which classes can use the element. Examples: Public, Private, Protected, Friend, and Protected Friend.
accessibility (software) Program design that allows a disabled person to use your application.
Active Server Pages (ASP) A platform for developing server-based Web applications.
ActiveX Data Objects (ADO) .NET A standard set of objects that Visual Studio programmers can use to retrieve and modify data from any source.
AddNew method Used to begin the Add operation for adding a new record to a dataset.
AdRotator control A Web control that randomly selects from a collection of advertisements each time the page is displayed.
AJAX (Asynchronous JavaScript and XML) Tools for creating interactive Web pages that can rapidly update part of a page.
AllowPaging property Adds pagination to a DataGrid Web control.
AllowSorting property Allows the user to sort the data grid by clicking on a column heading.
Application object Stores state information as long as the application is running.
assembly A basic unit of code that may be a single PE file or multiple files; built and deployed as a single implementation unit.
assembly information Information about a program stored in the AssemblyInfo.vb file.
assembly manifest A file that contains metadata about the version, a table describing all of the files needed by the assembly, and a reference list that specifies all of the external files needed, such as DLLs created by someone else.
asynchronous Task or operation running independently in the background.
attributes A keywordlike tag used to add information about elements.
author The programmer that creates the control used by the developer.

### B
BackGroundWorker Class for instantiating thread objects for asynchronous processing.
base class The parent class of the current class, from which the current class is inherited.
BeginEdit method Binding source method that starts the edit process.
BindingNavigator Toolbar in a database application with buttons for navigation and updating.
BindingSource object An object that controls binding controls to a form; handles currency management, navigation, sorting, filtering, and updating.
block-level scope A variable that is visible and accessible only within the block of code in which it is declared.
business rules The logic performed by an application, including validation, calculations, and updating rules.
business services tier One segment of a multiter application; the class or classes that perform the business rules.

### Button
A control that the user can click to perform an action. Windows Button control: fires a Click event; Web Button control: fires a Click event and causes a postback to occur.

### code separation model
Web page code design that separates the VB code into a separate file from the HTML.

### CancelEdit method
Cancels the current edit or add and returns to the original version of the data.

### collection
An object used to hold and manage the references to a group of related objects.

### ContextMenuStrip component
A menu component used to create context (right-mouse) menus.

### C

### D
data access tier The component in a multitier database project that holds the table adapters.

### event handler
A procedure that executes automatically when an event occurs.

### event provider
An object that generates or raises an event. Also called event source.

### event sink
The object that responds to a raised event. Also called event consumer.

### event source
An object that generates or raises an event. Also called event provider.

### Event statement
Must appear at the module level in order for your class to raise an event.

### Extensible Application Markup Language (XAML)
Source code language used to create a WPF application.

### F
Field Explorer A section of the toolbox that displays while Crystal Reports is active; holds elements that can be added to a report.
fields The elements represented in columns of a table; also used to refer to variables.
FIFO First-in, first-out. The organization used to store items in a queue.
filter Criteria used to select specific records.
flexibility The ability of an application to adapt to changes in the database or user interface; a feature facilitated by multiter applications.
foreign key The field in a child table that links a record to the corresponding record in the parent table.
foreign-key constraints Ensures that if the primary key in the parent table is modified or deleted, the corresponding record(s) in the child table are modified to match.
FormView control Web database control used to display a single record; provides for flexible layout by using a template.

### G
garbage collection The process in which the .NET Framework destroys unused objects and reclaims memory.
generic class A class that contains methods that can be instantiated using different data types.
generic collection A collection with a single type of object that is declared at design time.
generics Ability to create code, methods, or classes, without specifying the data type.
GetChanges method Used to retrieve only the rows with the specified row state.
GetChildRows method Retrieves an array of rows that are linked to the parent row.
GetParentRow method Retrieves the parent row of a child row.
globalization Designing your application for multiple languages, cultures, and locations.
GridView control Web database control for displaying records in rows and columns.
Group Footer A section of a Crystal Reports object that appears at the end of each group and generally displays subtotals.
Group Header A section of a Crystal Reports object that appears in the report at the top of a new group, based on the field that you selected for grouping.

### H
HasChanges method Used to determine if any changes have been made to a dataset.
hash table The fastest type of collection for searching. Based on a key/value pair where the key is calculated using an algorithm.
Help topic A single HTML page in HTML Help; each screen that displays in the Contents pane.
Help Viewer Part of the HTML Help Workshop that provides a way to view Help topics, screens, and HTML references.
HelpKeyword property A property of a control that appears when a HelpProvider is added to the form; used to specify the exact topic to display.
HelpNamespace property A property of a HelpProvider control; specifies the path and name of the Help file.
