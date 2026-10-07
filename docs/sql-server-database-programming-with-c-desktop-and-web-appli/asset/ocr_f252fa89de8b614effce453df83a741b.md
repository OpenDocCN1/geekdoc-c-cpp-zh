# Introduction to Databases

# 15

# Database

Table

![](bbox=[0.243, 0.116, 0.756, 0.313])

Record

| ID | Name | Ages | Address | Phone |
|---|---|---|---|--|
| 1000 | Tom | 36 | 220 Ave | 549-0507 |
| 1002 | Jim | 58 | 101 Main | 678-1002 |
| 2010 | Jeff | 49 | 25 Court | 678-3211 |
| 3090 | Kim | 23 | 43 Route | 202-5587 |

**FIGURE 2.6** Records and fields in a table.

# 2.3.2 Entity-RELATIONSHIP MODEL (ER)

The Entity-Relationship (ER) model was first proposed and developed by Peter Chen in 1976. Then Charles Bachman and James Martin added some refinements. The model was designed to communicate the database design in the form of a conceptual schema. It is based on the perception that the real world is made of entities, their attributes, and relationships. The ER model is graphically depicted in terms of Entity-Relationship diagrams (ERD). ERDs are a major modeling tool; they graphically describe the logical structure of the database. They can be used with to construct the relational tables and are a good vehicle for communicating the database design to either the end user or a developer. The three major components of ER are entities, relationships, and attributes.

**Entities:** An entity is a data object, either real or abstract, about which we want to collect information. For example, we want to collect information about a person, a place, or a thing. An entity in an ER translates into a table. It shouldpreferably be referred to as an entity set. Some common examples are departments, courses, students. A single occurrence of an entity is an instance. There are four entities in the CSE Dept database: Login, Faculty, Course, and Student. Each entity is translated into a table with the same name. For example, an instance of the Faculty entity is Alice Brown and her attributes.

**Relationships:** A database is made up of related entities. There is a natural association between the entities; they are referred to as relationships. For example,

+   * Students take courses
* Departments offer certain courses
* Employees are assigned to departments

The number of occurrences of one entity associated with single occurrence of a related entity is referred to as _cardinality.

**Attributes:** Each entity has properties or values called attributes associated with it. The attributes of an entity map into fields in. Database Processing is one attribute of an entity called Courses. The domain of an attribute is a set of all possible values from which an attribute can derive its value.