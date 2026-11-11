NOTE: The system identifier URL of a DTD may not actually be working, or be purposefully slowed down. An example for the latter is the system identifier of the XHTML 1.0 Strict DTD, http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd. If you parse an XHTML file, it may take a minute or two for the DTD to be served.

The remedy is to use an entity resolver that maps public identifiers to local files. Prior to Java 9, you had to provide an object of a class that implements the EntityResolver interface and provides a resolveEntity method.

Nowadays, you can use XML catalogs to manage the mapping. Provide one or more catalog files of the form

```
```xml
<?xml version="1.0"?>
<!DOCTYPE catalog PUBLIC  "-//OASIS//DTD XML Catalogs V1.0//EN"
    "http://www.oasis-open.org/committees/entity/release/1.0/catalog.dtd">
<catalog xmlns="urn:oasis:names:tc:entity:xmlns:xml:catalog" prefer="public">
    <public publicId="..." uri="..."/>
    ...
</catalog>
```
```

Then construct and install a resolver like this:

```
```java
builder.setEntityResolver(CatalogManager.catalogResolver(
    CatalogFeatures.defaults(),
    Paths.get("catalog.xml").toAbsolutePath().toUri()));
```
```

See Listing 3.6 for a complete example.

Instead of setting the catalog file locations in your program, you can specify them on the command line with the java.xml.catalog.files system property. Provide absolute file URLs separated by semicolons.

Now that you have seen how the parser locates the DTD, let us consider the various kinds of rules.

The ELEMENT rule specifies what children an element can have. Use a regular expression, made up of the components shown in Table 3.1.

Here are several simple but typical examples. The following rule states that a menu element contains 0 or more item elements:

```
```xml
<!ELEMENT menu (item)*>
```
```

This set of rules states that a font is described by a name followed by a size, each of which contain text:

```
```xml
<!ELEMENT font (name,size)>
<!ELEMENT name (#PCDATA)>
<!ELEMENT size (#PCDATA)>
```
```