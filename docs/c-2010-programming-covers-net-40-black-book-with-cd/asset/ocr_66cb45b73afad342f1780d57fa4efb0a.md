+   - Introduction of object services, that is, Application Programming Interface (API) improvements, to enable N-tier and self-tracking entities. This implies that now you can access the updated data to eastablish the original state of an entity by using the ObjectStateEntry.GetUpdatableOriginalValues method.
+   - Introduction of improvements in using SQL satetements when querying Entity Framework such as removal of joins and elimination of constants used for internal purposes.
+   - Introduction of navigation property management that would now help the developers to delete and add navigation property, and also enables the creation of one-way associations.
+   - Introduction of support for Microsoft SQL Server Compact (SQL CE) edition. This will help in simplifying customization of database generation.
+   - Introduction of extensibility APIs that will help in adding custom properties to any object in the model.
+   - Introduction of model first development technique, which implies that a developer can start from EDM and then generate the associated T-SQL and customized code from the model.
+   - Introduction of testing applications that use the Entity Framework, which includes an interface that helps in better testing of applications that use Entity Framework.
+   - Introduction of persistence ignorance that helps the developers to use their own classes in an Entity Framework application, without introducing interfaces or elements that are specificto Entity Framework.

Let’s now understand the entity data model.

# Understanding the Entity Data Model

A data model is usually designed in the analysis or planning phase of a project. This is done since the relationships among data types, their attributes, and the constraints in the data must be organized conceptually before they can be implemented in the application code. EDM is used to extend models that application designers use to describe data during the development process. These models provide a specification to define data used by an application. An application based on EDM defines the entities and relationships in the domain of the application in the design schema used to generate programmable classes that are further used by the application code.

In EDM, mapping specification connects the design schema and storage schema. The storage structure that contains data for the application is represented in a storage schema. The storage schema is mapped to the design schema so that the mapping specification effectively connects programmable classes to storage structures. Now, let’s understand the following concepts related to the design of EDM:

+   - Data modeling
+   - CSDL
+   - SSDL
+   - MSL
+   - The EDM types
+   - Type constraints
+   - Data model tools

Let’s now learn about these concepts one by one in detail.

# Data Modeling

Data modeling is a technique to structure and organize data that are needed to support an application. For example, an entity in an application must be represented by data, such as customers, orders, and products, whereas, a relationship specifies the logical connection among the entities. Defining entities and relationships can be a very complex process. It might require unexpected amount of detail, for example, an order might be a telephone order, a catalogue order, or an Internet order, which is quite confusing. To overcome this problem, EDM defines entities and uses data readers to read entities in a serialized form or as materialized objects.

An object model represents the classes that are programmable in Common Language Runtime (CLR) and can be built from the conceptual model defined in the design schema. An EDM conceptual model is a specification for