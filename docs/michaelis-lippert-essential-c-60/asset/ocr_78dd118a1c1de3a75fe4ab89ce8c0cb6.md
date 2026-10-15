# BEGINNER TOPIC

# Extensible Markup Language

The Extensible Markup Language (XML) is a simple and flexible text format frequently used within Web applications and for exchanging data between applications. XML is extensible because included within an XML document is information that describes the data, known as **metadata**. Here is a sample XML file.

```
```xml
<?xml version="1.0" encoding="utf-8" ?>
<body>
    <book title="Essential C# 6.0">
        <chapters>
            <chapter title="Introducing C#"/>
            <chapter title="Operators and Control Flow"/>
            ...
        </chapters>
    </book>
</body>
```
```

The file starts with a header indicating the version and character encoding of the XML file. After that appears one main “book” element. Elements begin with a word in angle brackets, such as `<body>`. To end an element, place the same word in angle brackets and add a forward slash to prefix the word, as in `</body>`. In addition to elements, XML supports attributes. `title="Essential C# 6.0"` is an example of an XML attribute. Note that the metadata (book title, chapter, and so on) describing the data (“Essential C# 6.0”, “Operators and Control Flow”) is included in the XML file. This can result in rather bloated files, but it offers the advantage that the data includes a description to aid in interpreting it.

# Application Programming Interface

All the methods (or more generically, the members) found on a data type like `System.Console` are what define the System.Console’s **application programming interface (API)**. The API defines how a software program interacts with a component. As such, it is found not just with a single data type, but more generally the combination of all the APIs for a set of data types are said to create an API for the collective set of components. In .NET, for example, all the types (and the members within those types) in