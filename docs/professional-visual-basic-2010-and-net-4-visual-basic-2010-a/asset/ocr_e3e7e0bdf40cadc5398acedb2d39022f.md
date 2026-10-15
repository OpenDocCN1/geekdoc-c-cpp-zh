Atom is an XML format that was initially proposed as a “better RSS,” but it has grown into a flexible format for defining objects of any syntax. Figure 12-35 shows an example of this format. The `<content>` element holds the actual data, while the rest of the XML is used to provide metadata (data about the data).

![](bbox=[0.094, 0.167, 0.749, 0.594])

**FIGURE 12-35**

The root element of Atom is either a `<feed>` node, or an `<entry>` node. Feed elements are used to contain multiple entry elements, whereas an entry element represents a single item.

JSON is a subset of JavaScript that has become a popular syntax for passing data across the Internet (see Figure 12-36). It is a very concise format for describing data. Individual objects are wrapped in braces ({}); and within an object, the properties are defined using name:value pairs, each in quotes. Collections are defined by wrapping the child objects with brackets ([]).

![](bbox=[0.094, 0.748, 0.535, 0.826])

**FIGURE 12-36**

The benefit of JSON over Atom is this conciseness. For the single author shown in Figures 12-35 and 12-36, the JSON version is 459 bytes, whereas the Atom format is 1,300 bytes. Obviously, the more objects you have here, the more the XML format would increase this difference. Conversely, the Atom format retains more information about the record than the bare-bones JSON format.