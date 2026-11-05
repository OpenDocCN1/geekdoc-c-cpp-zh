"XSD" is currently the de facto standard for describing XML documents. There are 2 versions in use 1.0 and 1.1, which are on the whole the same. An XSD schema is itself an XML document, there is even an an XSD schema to describe the XSD standard.

It is often useful to examine the schema of the XML stream that is generated when instances of a class (or classes) are serialized. For example, one might publish the schema for others to use, or might compare it to a schema with which one is trying to achieve conformity.

# 9. To generate an XML Schema document from a set of classes

+   1. Compile the class or classes into a DLL.
+   2. Open a command prompt.
+   3. Pass the DLL as an argument to Xsd.exe, for example:
+   4. xsd MyFile.dll
+   5. The schema (or schemas) will be written, beginning with the name schema0.xsd".

# Example

| Sample XSD | Sample XML |
|---|---|
| 1. <xs:element name=" Author _dob">  
2. type="xs:date"/> | 1. <Author_dob>  
2. 2000-01-12T12:13:14Z  
3. </Author_dob> |
| 1. <xs:element name=" Author _address">  
2. type="xs:string"/> | 1. < Author _address>  
2. 1,MG Marg Camp  
3. </ Author _address> |
| 1. <xs:element name="AuthorID">  
2. type="xs:int"/> | 1. <AuthorID>  
2. 2610  
3. </AuthorID> |
| 1. <xs:element name="Content">  
2. type="xs:string"/> | 1. <Content>  
2. (a type can be defined as  
3. a string but not have any  
4. content; this is not true  
5. of all data types, however).  
6. </Content> |