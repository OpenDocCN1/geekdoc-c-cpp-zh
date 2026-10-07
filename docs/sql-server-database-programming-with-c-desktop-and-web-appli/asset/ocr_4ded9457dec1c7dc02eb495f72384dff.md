# SQL Server Database Programming with C#

Entity is represented by a rectangular box.

![](bbox=[0.579, 0.087, 0.696, 0.131])

A weak entity is represented by a double rectangular box.

![](bbox=[0.587, 0.193, 0.687, 0.237])

An attribute is represented by an oval

![](bbox=[0.573, 0.303, 0.706, 0.342])

Relationship is represented by a diamond with lines connecting the entities involved

![](bbox=[0.573, 0.393, 0.715, 0.462])

Cardinality is indicated by placing 1, N, or M near the entity it is associated with

| 1 | M |

A line links entities to attributes and relationships

![](bbox=[0.443, 0.563, 0.733, 0.572])

FIGURE 2.14 Commonly used symbols for ER notation.

# 2.6 ER NOTATION

There are a number of ER notations available, including Chen’s, Bachman, Crow’s foot and a few others. There is at present no consensus on the symbols and the styles used to draw ERDs. A number of drawing tools are available to draw ERDs. These include ER Assistant, Microsoft Visio, and Smart Draw, many others. The commonly used notations are shown in Figure 2.14.

# 2.7 DATA NORMALIZATION

After identifying tables, attributes, and relations the next logical step in database design is to make sure that the database structure is optimal. The optimum structure is achieved by eliminating redundancies, unnecessary inefficiencies, and deletion anomalies that usually occur in normalized or partially normalized databases. Data normalization is a progressive process. The steps in the normalization process are called normal forms. Each normal form progressively improves the database and makes it more efficient. In other words, a database that is in second normal form is better than the one in the first normal form, and one in third normal form is better than in second normal form. To be in the third normal form a database has to be in both the first and second normal