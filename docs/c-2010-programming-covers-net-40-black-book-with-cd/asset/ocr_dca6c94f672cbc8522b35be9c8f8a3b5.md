entities and relationships in the domain of an application. Object model and storage metadata, which consist of logical description of database structure, are mapped to the conceptual layer.

Now, let’s discuss about design and implementation of an EDM and its mapping to different platforms.

# Design and Implementation

EDM types are designed in schemas to preserve the logical integrity of data and the constraints of business and technical applications. According to EDM specifications, the following three stages of development are required to implement the data model:

+   - Entities and relationships in the domain of an application are specified in an XML file
+   - Metadata that describes the structures of the database is also specified in an XML file
+   - Mapping of entities and relationships to corresponding databases is specified in the storage metadata file

# EDM Mapping to CLR and Database Management Systems

EDM supports application scenarios across various storage models and maps to both the CLR and the database management system such as SQL Server. With the introduction of EDM, ADO.NET provides a comprehensive platform that connects application code to storage structures. It uses a store-independent view mechanism that takes advantage of the concepts of a Relational Database Management System (RDBMS) to implement mapping among schemas, programming languages, and database tables. The EDM data services are not dependent on any particular storage schema. Applications that require multiple data sources can maintain individual mappings for each data source.

Developing an application by using Entity Framework requires creating and mapping conceptual EDM and storage entity models. Entity Framework has made entity-relationship modeling executable through a combination of XML files such as Conceptual schema definition language (.csdl), Store schema definition language (.ssdl), and Mapping specification language (.msl).

# Conceptual Schema Definition Language

CSDL contains a design schema that provides a design template for an object model. An application uses the object model based on CSDL. A schema is an XML text file that describes entity and relationship types. It also defines a container that contains instances of these types in a logically organized form. CSDL is an XML syntax used to describe both the EDM types, those that are provided when Entity Framework is installed and those that are designed by the developer. The following code snippet shows the overall structure of a CSDL file:

```
<? xml version="1.0" encoding="utf-8"?>
<Schema xmlns:cg="http://schemas.microsoft.com/ado/2006/04/codegeneration" xmlns="http://schemas.microsoft.com/ado/2006/04/edm" Namespace="Humanresource.Salaryschema" Alias="Self">
<Documentation>
<Summary>Shows general Syntax of Conceptual schema (csdl) </Summary>
</Documentation>
<EntityType Name="Employee">
<Key>
<PropertyRef Name="EmployeeId" />
</Key>
<Property Name=" EmployeeId " Type="Guid" Nullable="false" />
<!-- Other properties-->
</EntityType>
<Association Name="Monthly_Salary">
<End Role="Employee" Type="Self.Employee" Multiplicity="0..1" />
</Association>
<EntityContainer Name=" Humanresource.SalarySchema ">
<EntitySet Name="Employee" EntityType="Self. Employee" />
<AssociationSet Name="Monthly_Salary">
Association="Self.Monthly_Salary">
<End Role="Employee" EntitySet="Employees" />
```