# 1012	Chapter 23	Asynchronous Programming with async and await

+   * Class HttpClient.GetStringAsync method uses the URL specified as the method's string argument to request information from a web server and returns a Task<string>representing a promise to return a string.

# Section 23.6.3 Processing the XML Response

+   * XML represents data as elements, attributes and text.
* XML delimits elements with start tags and end tags.
* A start tag consists of the element name, followed by attributeName=value pairs, all enclosed in angle brackets.
* An end tag consists of the element name preceded by a forward slash (/) in angle brackets.
* An element start and end tag enclose a piece of data or nested elements.
* If an element is—that is, it does not contain or nested elements between its start and end tags—the element can be represented by a start tag that uses /> rather than.
* Namespace System.Xml.Linq contains the classes used to parse XML using LINQ to XML.
* LINQ to query an XDocument to extract data from the XML.
* XDocument method Descendants returns a list of XElement objects representing the elements with the name specified as an argument.
* XElement method Attribute returns XAttributes representing an attributes.
* XAttribute property returns the value of a given attribute.

# Section 23.6.4 Binding the Title to the ListBox

+   * You cannot bind a LINQ query directly to a ListBox. You must first convert the result to a List with ToList or to ToArray.
* A ListBox’s DataSource property indicates the source of data that populates the ListBox’s Items collection. A ListBox’s DisplayMember property indicates which property of each item in the data source should be displayed in the ListBox.

# Section 23.6.5 Asynchronously Downloading Image’s Bytes

+   * HttpClient.GetByteArrayAsync method launches in a separate thread a Task<byte[]> that gets a byte[] from the URL specified as the argument.

# Section 23.7 Displaying an Asynchronous Task’s Progress

+   * ProgressBar property Minimum gets or sets a ProgressBar’s minimum value.
* ProgressBar property Maximum gets or sets a ProgressBar’s maximum value.
* ProgressBar property Value gets or sets a ProgressBar’s current value. As this number increases, a ProgressBar fills with color.
* Enumerable static method Repeat creates a list of elements containing the first argument’s value. The length of the list is specified by the second argument. Repeat is a generic method—the type of the list it is determined by the first argument’s type.

# Terminology

async method Attribute method of class XElement
asynchronous call await expression
nasynchronous programming await multiple Tasks
asynchronous task await operator *