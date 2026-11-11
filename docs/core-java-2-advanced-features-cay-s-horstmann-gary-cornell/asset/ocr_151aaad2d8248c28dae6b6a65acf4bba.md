> **NOTE:** We generally recommend the use of elements, not attributes, to describe data. Thus, the font style should be a separate element, such as `<font><style>plain</style>...</font>`. However, attributes have an undeniable advantage for enumerated types because the parser can verify that the values are legal. For example, if the font style is an attribute, the parser checks that it is one of the four allowed values, and supplies a default if no value was given.

The handling of a `CDATA` attribute value is subtly different from the processing of `#PCDATA` that you have seen before, and quite unrelated to the `<![CDATA[...]]>` sections. The attribute value is first *normalized*—that is, the parser processes character and entity references (such as `&#33;` or `&#x1;`) and replaces whitespace with spaces.

An `NMTOKEN` (or name token) is similar to `CDATA`, but most nonalphanumeric characters and internal whitespace are disallowed, and the parser removes leading and trailing whitespace. `NMTOKENS` is a whitespace-separated list of name tokens.

The ID construct is quite useful. An ID is a name token that must be unique in the document—the parser checks the uniqueness. You will see an application in the next sample program. An `IDREF` is a reference to an ID that exists in the same document, which the parser also checks. `IDREFS` is a whitespace-separated list of ID references.

An `ENTITY` attribute value refers to an “unparsed external entity.” That is a holdover from SGML that is rarely used in practice. The annotated XML specification at `www.xml.com/axml/axml.html` has an example.

A DTD can also define entities, or abbreviations that are replaced during parsing. You can find a good example for the use of entities in the user interface descriptions of the Firefox browser. Those descriptions are formatted in XML and contain entity definitions such as

```
```xml
<!ENTITY back.label "Back">
```
```

Elsewhere, text can contain an entity reference, for example:

```
```xml
<!menuitem label="&back.label;"/>
```
```

The parser replaces the entity reference with the replacement string. To internalize the application, only the string in the entity definition needs to be changed. Other uses of entities are more complex and less common; look at the XML specification for details.

This concludes the introduction to DTDs. Now that you have seen how to use DTDs, you can configure your parser to take advantage of them.