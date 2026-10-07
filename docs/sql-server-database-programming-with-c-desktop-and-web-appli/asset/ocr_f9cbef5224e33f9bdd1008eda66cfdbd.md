# SQL Server Database Programming with C#

J. The system method Exists() is executed to find all files whose contain the keyword 'Visual Studio'. All of the matched files will be opened and the contents will be read back by the method ReadAllText(), assigned to the string object fileContents.

K. The read out fileContents is returned to the calling method.

L. The body of the method GetFiles() starts from here with the path as the argument of this method. The point is that this method must be defined as a static method and the returned data type is IEnumerable<T>.

M. An exception will be thrown out if the desired path did not exist in the current system.

N. A new non-generic, collection List<T> is created with a Cast to it to the IEnumerable<T>.

O. The system method GetFiles() is executed to find the names of all files that are under the current path, and assign them to the string array fileNames.

P. A foreach loop is executed to find all searched files into the non-generic List<T> object files.

Q. All of those files are returned to the calling method.

Now you can build and run the project by clicking on the Debug | Starting Debug menu item. All files that have an extension .html and under the path C:\Program Files\Microsoft Visual Studio\ whose name contains the keyword 'Visual Studio' are found and displayed as this project. Press any key from the keyboard to execute this project.

A complete Console query QueryContentsLINQ be found from a Class DB Projects Chapter 4 is located under the Students at the CRC press fit (refer to 1.2 in Chapter 1). Next let's have a discussion about another query related to LINQ to Objects, the LINQ and Reflection.

# 4.4.4 LINQ AND Reflection

.NET 3.5 class library APIs can be used to examine the metadata in a .NET assembly and create collections of types, type members, parameters, and so on that are in that assembly. these collections support the generic IEnumerable interface, they can be queried by using LINQ to Objects query.

To make simple and easy, in this example we use one project to illustrate how LINQ can be used with reflection to retrieve specific metadata about a method that matched a specific criterion. In this case, the query will find the names of all the methods in the assembly that return enumerable types such as arrays.

Create new C# Console project QueryReflectionLINQ. Open the code of the C# Program.cs in the Solution explorer and edit the codes in Figure 4.31 into this window to replace all original codes. Let's have a closer look at this piece of code.

A. The namespace System.Reflection is added to the namespace declaration part of this project since we need to use some components defined in this namespace in coding.

B. An Assembly object is created with the Load[] method is executed to load and assign this Assembly to the instance assembly.

C. The LINQ query is created and initialized with three clauses. The GetType() method is used to obtain the data type of all queried methods. The first where clause is used to filter methods in the Public type. The second from clause is used to get the desired methods based on the data type criteria: 1) the returning type of the method is array, 2) those methods should have a valid interface and 3) the returning type of those methods should not be System.string. Also the queried methods' names are converted to string.